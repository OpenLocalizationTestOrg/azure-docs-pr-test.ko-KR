---
title: "자습서: RunMyProcess와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 RunMyProcess 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="3b1af-103">자습서: RunMyProcess와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3b1af-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="3b1af-104">이 자습서에서는 Azure AD(Azure Active Directory)와 RunMyProcess를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b1af-105">RunMyProcess를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3b1af-106">RunMyProcess에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="3b1af-107">사용자가 해당 Azure AD 계정으로 RunMyProcess에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b1af-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3b1af-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b1af-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3b1af-110">Prerequisites</span></span>

<span data-ttu-id="3b1af-111">RunMyProcess와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="3b1af-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3b1af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b1af-113">RunMyProcess Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3b1af-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b1af-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b1af-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b1af-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3b1af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b1af-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b1af-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3b1af-118">Scenario description</span></span>
<span data-ttu-id="3b1af-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b1af-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b1af-121">갤러리에서 RunMyProcess 추가</span><span class="sxs-lookup"><span data-stu-id="3b1af-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="3b1af-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3b1af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="3b1af-123">갤러리에서 RunMyProcess 추가</span><span class="sxs-lookup"><span data-stu-id="3b1af-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="3b1af-124">RunMyProcess의 Azure AD 통합을 구성하려면 갤러리의 RunMyProcess를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3b1af-125">**갤러리에서 RunMyProcess를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b1af-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3b1af-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b1af-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3b1af-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3b1af-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3b1af-133">검색 상자에 **RunMyProcess**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-133">In the search box, type **RunMyProcess**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="3b1af-135">결과 창에서 **RunMyProcess**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b1af-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3b1af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b1af-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 RunMyProcess에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b1af-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 RunMyProcess 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="3b1af-140">즉, Azure AD 사용자와 RunMyProcess의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="3b1af-141">RunMyProcess에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3b1af-142">RunMyProcess에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3b1af-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3b1af-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b1af-145">**[RunMyProcess 테스트 사용자 만들기](#creating-a-runmyprocess-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 RunMyProcess에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b1af-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b1af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b1af-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3b1af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b1af-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 RunMyProcess 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="3b1af-150">**RunMyProcess에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b1af-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="3b1af-151">Azure Portal의 **RunMyProcess** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3b1af-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="3b1af-155">**RunMyProcess 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="3b1af-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="3b1af-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3b1af-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-158">The value is not real.</span></span> <span data-ttu-id="3b1af-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="3b1af-160">값을 얻으려면 [RunMyProcess 클라이언트 지원 팀](mailto:support@runmyprocess.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1af-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="3b1af-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="3b1af-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3b1af-165">**RunMyProcess 구성** 섹션에서 **RunMyProcess 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3b1af-166">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="3b1af-168">다른 웹 브라우저 창에서 RunMyProcess 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="3b1af-169">왼쪽 탐색 패널에서 **계정**을 클릭하고 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="3b1af-171">**인증 방법** 섹션으로 이동하고 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="3b1af-173">a.</span><span class="sxs-lookup"><span data-stu-id="3b1af-173">a.</span></span> <span data-ttu-id="3b1af-174">**메서드**로 **Samlv2를 사용한 SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="3b1af-175">b.</span><span class="sxs-lookup"><span data-stu-id="3b1af-175">b.</span></span> <span data-ttu-id="3b1af-176">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SSO 리디렉션** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3b1af-177">c.</span><span class="sxs-lookup"><span data-stu-id="3b1af-177">c.</span></span> <span data-ttu-id="3b1af-178">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 리디렉션** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3b1af-179">d.</span><span class="sxs-lookup"><span data-stu-id="3b1af-179">d.</span></span> <span data-ttu-id="3b1af-180">**이름 ID 형식** 텍스트 상자에 **이름 식별자 형식** 값을 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="3b1af-181">e.</span><span class="sxs-lookup"><span data-stu-id="3b1af-181">e.</span></span> <span data-ttu-id="3b1af-182">다운로드한 인증서 파일의 내용을 복사한 다음 **인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="3b1af-183">f.</span><span class="sxs-lookup"><span data-stu-id="3b1af-183">f.</span></span> <span data-ttu-id="3b1af-184">**저장** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="3b1af-185">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3b1af-186">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3b1af-187">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b1af-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1af-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="3b1af-189">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3b1af-191">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3b1af-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3b1af-192">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b1af-194">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b1af-196">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b1af-198">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b1af-200">a.</span><span class="sxs-lookup"><span data-stu-id="3b1af-200">a.</span></span> <span data-ttu-id="3b1af-201">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b1af-202">b.</span><span class="sxs-lookup"><span data-stu-id="3b1af-202">b.</span></span> <span data-ttu-id="3b1af-203">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b1af-204">c.</span><span class="sxs-lookup"><span data-stu-id="3b1af-204">c.</span></span> <span data-ttu-id="3b1af-205">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3b1af-206">d.</span><span class="sxs-lookup"><span data-stu-id="3b1af-206">d.</span></span> <span data-ttu-id="3b1af-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="3b1af-208">RunMyProcess 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1af-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="3b1af-209">Azure AD 사용자가 RunMyProcess에 로그인할 수 있도록 하려면 RunMyProcess로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="3b1af-210">RunMyProcess의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="3b1af-211">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b1af-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3b1af-212">RunMyProcess 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="3b1af-213">왼쪽 탐색 패널에서 **계정**을 클릭하고 **사용자**를 선택한 다음 **새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="3b1af-214">![새 사용자](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="3b1af-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="3b1af-215">**사용자 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3b1af-216">![프로필](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "프로필")</span><span class="sxs-lookup"><span data-stu-id="3b1af-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="3b1af-217">a.</span><span class="sxs-lookup"><span data-stu-id="3b1af-217">a.</span></span> <span data-ttu-id="3b1af-218">관련된 텍스트 상자에 프로비전할 유효한 Azure AD 계정의 **이름** 및 **전자 메일**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="3b1af-219">b.</span><span class="sxs-lookup"><span data-stu-id="3b1af-219">b.</span></span> <span data-ttu-id="3b1af-220">**IDE 언어**, **언어** 및 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="3b1af-221">c.</span><span class="sxs-lookup"><span data-stu-id="3b1af-221">c.</span></span> <span data-ttu-id="3b1af-222">**나에게 계정 만들기 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="3b1af-223">d.</span><span class="sxs-lookup"><span data-stu-id="3b1af-223">d.</span></span> <span data-ttu-id="3b1af-224">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="3b1af-225">RunMyProcess에서 제공하는 다른 RunMyProcess 사용자 계정 만들기 도구 또는 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3b1af-226">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3b1af-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3b1af-227">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 RunMyProcess에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3b1af-229">**Britta Simon을 RunMyProcess에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b1af-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="3b1af-230">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3b1af-232">응용 프로그램 목록에서 **RunMyProcess**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="3b1af-234">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-234">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3b1af-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-236">Click **Add** button.</span></span> <span data-ttu-id="3b1af-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3b1af-239">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3b1af-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b1af-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b1af-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3b1af-242">Testing single sign-on</span></span>

<span data-ttu-id="3b1af-243">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3b1af-244">액세스 패널에서 RunMyProcess 타일을 클릭하면 RunMyProcess 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1af-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b1af-245">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3b1af-245">Additional resources</span></span>

* [<span data-ttu-id="3b1af-246">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3b1af-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b1af-247">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3b1af-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

