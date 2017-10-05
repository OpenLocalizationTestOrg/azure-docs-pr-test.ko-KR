---
title: "자습서: SuccessFactors와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory에서 SuccessFactors를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="8ea24-103">자습서: SuccessFactors와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="8ea24-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="8ea24-104">이 자습서에서는 SuccessFactors와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ea24-105">SuccessFactors를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8ea24-106">SuccessFactors에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="8ea24-107">사용자가 해당 Azure AD 계정으로 SuccessFactors에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8ea24-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8ea24-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ea24-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ea24-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8ea24-110">Prerequisites</span></span>
<span data-ttu-id="8ea24-111">SuccessFactors와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="8ea24-112">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="8ea24-112">A valid Azure subscription</span></span>
* <span data-ttu-id="8ea24-113">SuccessFactors의 테넌트</span><span class="sxs-lookup"><span data-stu-id="8ea24-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="8ea24-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8ea24-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8ea24-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8ea24-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ea24-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="8ea24-118">Scenario description</span></span>
<span data-ttu-id="8ea24-119">이 자습서는 테스트 환경에서 Azure AD Single Sign-on을 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="8ea24-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ea24-121">갤러리에서 SuccessFactors 추가</span><span class="sxs-lookup"><span data-stu-id="8ea24-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="8ea24-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8ea24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="8ea24-123">갤러리에서 SuccessFactors 추가</span><span class="sxs-lookup"><span data-stu-id="8ea24-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="8ea24-124">SuccessFactors의 Azure AD 통합을 구성하려면 갤러리의 SuccessFactors를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ea24-125">**갤러리에서 SuccessFactors를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8ea24-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ea24-126">Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Single Sign-On 구성][1]
2. <span data-ttu-id="8ea24-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8ea24-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Single Sign-On 구성][2]
4. <span data-ttu-id="8ea24-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-131">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="8ea24-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Single Sign-On 구성][4]
6. <span data-ttu-id="8ea24-135">**검색 상자**에서 **SuccessFactors**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Single Sign-On 구성][5]
7. <span data-ttu-id="8ea24-137">결과 창에서 **SuccessFactors**를 선택한 다음 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Single Sign-On 구성][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ea24-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8ea24-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ea24-140">이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 SuccessFactors에서 Azure AD Single Sign-On을 구성하고 테스트하는 방법을 보여 주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ea24-141">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SuccessFactors 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="8ea24-142">즉, Azure AD 사용자와 SuccessFactors의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="8ea24-143">이 연결 관계는 Azure AD의 **사용자 이름** 값을 SuccessFactors의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="8ea24-144">SuccessFactors에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ea24-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ea24-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ea24-147">**[SuccessFactors 테스트 사용자 만들기](#creating-a-successfactors-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 SuccessFactors에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8ea24-148">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ea24-149">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ea24-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="8ea24-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="8ea24-151">이 섹션에서는 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 SuccessFactors 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="8ea24-152">**SuccessFactors에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8ea24-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="8ea24-153">Azure 클래식 포털의 **SuccessFactors** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Single Sign-On 구성][7]
2. <span data-ttu-id="8ea24-155">**사용자가 SuccessFactors에 로그인하는 방법을 선택하십시오.** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On 구성][8]
3. <span data-ttu-id="8ea24-157">**앱 URL 구성** 페이지에서 다음 단계를 수행하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Single Sign-On 구성][9]
   
    <span data-ttu-id="8ea24-159">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-159">a.</span></span> <span data-ttu-id="8ea24-160">**로그인 URL** 텍스트 상자에서 다음 패턴 중 하나를 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="8ea24-161">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-161">b.</span></span> <span data-ttu-id="8ea24-162">**회신 URL** 텍스트 상자에서 다음 패턴 중 하나를 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="8ea24-163">c.</span><span class="sxs-lookup"><span data-stu-id="8ea24-163">c.</span></span> <span data-ttu-id="8ea24-164">**Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="8ea24-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-165">Please note that these are not the real values.</span></span> <span data-ttu-id="8ea24-166">실제 로그온 URL 및 회신 URL로 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="8ea24-167">이러한 값을 얻으려면 [SuccessFactors 지원 팀](https://www.successfactors.com/en_us/support.html)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="8ea24-168">**SuccessFactors에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭한 다음 인증서 파일을 컴퓨터에 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Single Sign-On 구성][10]

2. <span data-ttu-id="8ea24-170">다른 웹 브라우저 창에서 **SuccessFactors 관리 포털** 에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="8ea24-171">**응용 프로그램 보안**을 방문하고 **Single Sign On 기능**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="8ea24-172">**토큰 재설정**에 값을 입력하고 **토큰 저장**을 클릭하여 SAML SSO를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성][11]

    > [!NOTE] 
    > <span data-ttu-id="8ea24-174">이 값은 설정/해제 스위치로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="8ea24-175">값이 저장된 경우 SAML SSO는 ON입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="8ea24-176">빈 값이 저장된 경우 SAML SSO는 OFF입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="8ea24-177">아래 스크린샷으로 이동하고 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성][12]
   
    <span data-ttu-id="8ea24-179">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-179">a.</span></span> <span data-ttu-id="8ea24-180">**SAML v2 SSO** 라디오 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="8ea24-181">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-181">b.</span></span> <span data-ttu-id="8ea24-182">SAML 어설션 파티 이름(예: SAml 발급자 + 회사 이름)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="8ea24-183">c.</span><span class="sxs-lookup"><span data-stu-id="8ea24-183">c.</span></span> <span data-ttu-id="8ea24-184">**SAML 발급자** 텍스트 상자에서 Azure AD 응용 프로그램 구성 마법사의 **발급자 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="8ea24-185">d.</span><span class="sxs-lookup"><span data-stu-id="8ea24-185">d.</span></span> <span data-ttu-id="8ea24-186">**필수 서명 요구**로 **응답(고객 생성/IdP/AP)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="8ea24-187">e.</span><span class="sxs-lookup"><span data-stu-id="8ea24-187">e.</span></span> <span data-ttu-id="8ea24-188">**SAML 플래그 사용**으로 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="8ea24-189">f.</span><span class="sxs-lookup"><span data-stu-id="8ea24-189">f.</span></span> <span data-ttu-id="8ea24-190">**로그인 요청 서명(SF 생성/SP/RP)**으로 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="8ea24-191">g.</span><span class="sxs-lookup"><span data-stu-id="8ea24-191">g.</span></span> <span data-ttu-id="8ea24-192">**SAML 프로필**로 **브라우저/게시 프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="8ea24-193">h.</span><span class="sxs-lookup"><span data-stu-id="8ea24-193">h.</span></span> <span data-ttu-id="8ea24-194">**인증서 유효 기간 적용**으로 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="8ea24-195">i.</span><span class="sxs-lookup"><span data-stu-id="8ea24-195">i.</span></span> <span data-ttu-id="8ea24-196">다운로드한 인증서 파일의 내용을 복사한 다음 **SAML 확인 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ea24-197">인증서 내용에는 시작 인증서 및 끝 인증서 태그가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="8ea24-198">SAML V2로 이동한 후 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성][13]
   
    <span data-ttu-id="8ea24-200">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-200">a.</span></span> <span data-ttu-id="8ea24-201">**SP 시작 전역 로그아웃 지원**으로 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="8ea24-202">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-202">b.</span></span> <span data-ttu-id="8ea24-203">**전역 로그아웃 서비스 URL (LogoutRequest 대상)** 텍스트 상자에서 Azure AD 응용 프로그램 구성 마법사의 **원격 로그아웃 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="8ea24-204">c.</span><span class="sxs-lookup"><span data-stu-id="8ea24-204">c.</span></span> <span data-ttu-id="8ea24-205">**요청 SP는 모든 NameID 요소를 암호화해야 합니다.**로 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="8ea24-206">d.</span><span class="sxs-lookup"><span data-stu-id="8ea24-206">d.</span></span> <span data-ttu-id="8ea24-207">**NameID 형식**으로 **지정되지 않음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="8ea24-208">e.</span><span class="sxs-lookup"><span data-stu-id="8ea24-208">e.</span></span> <span data-ttu-id="8ea24-209">**SP 시작 로그인 사용(AuthnRequest)**으로 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="8ea24-210">f.</span><span class="sxs-lookup"><span data-stu-id="8ea24-210">f.</span></span> <span data-ttu-id="8ea24-211">**전사적 발급자로 보내기 요청** 텍스트 상자에서 Azure AD 응용 프로그램 구성 마법사의 **원격 로그인 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="8ea24-212">로그인 사용자 이름의 대/소문자를 구분하지 않으려면 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="8ea24-213">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-213">a.</span></span> <span data-ttu-id="8ea24-214">a. **회사 설정**(아래쪽)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="8ea24-215">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-215">b.</span></span> <span data-ttu-id="8ea24-216">**사용자 이름 대/소문자 구분하지 않음 사용**근처의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="8ea24-217">c. **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-217">c.Click **Save**.</span></span>
   
    ![Single Sign-On 구성][29]

    > [!NOTE] 
    > <span data-ttu-id="8ea24-219">이 기능을 사용하려고 하면 시스템에서 중복되는 SAML 로그인 이름이 만들어지는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="8ea24-220">예를 들어 고객의 사용자 이름에 User1 및 user1이 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="8ea24-221">대/소문자를 구분하지 않으면 이러한 중복 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="8ea24-222">시스템에서 오류 메시지를 제공하고 기능이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="8ea24-223">실제로 다른 철자가 되도록 고객은 사용자 이름 중 하나를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="8ea24-224">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![응용 프로그램][14]
2. <span data-ttu-id="8ea24-226">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![응용 프로그램][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ea24-228">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8ea24-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ea24-229">이 섹션의 목적은 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][16]

<span data-ttu-id="8ea24-231">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="8ea24-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ea24-232">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][17]
2. <span data-ttu-id="8ea24-234">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8ea24-235">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][18]
4. <span data-ttu-id="8ea24-237">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][19]
5. <span data-ttu-id="8ea24-239">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][20]
   
    <span data-ttu-id="8ea24-241">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-241">a.</span></span> <span data-ttu-id="8ea24-242">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="8ea24-243">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-243">b.</span></span> <span data-ttu-id="8ea24-244">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8ea24-245">c.</span><span class="sxs-lookup"><span data-stu-id="8ea24-245">c.</span></span> <span data-ttu-id="8ea24-246">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-246">Click **Next**.</span></span>
6. <span data-ttu-id="8ea24-247">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][21]
   
    <span data-ttu-id="8ea24-249">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-249">a.</span></span> <span data-ttu-id="8ea24-250">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="8ea24-251">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-251">b.</span></span> <span data-ttu-id="8ea24-252">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="8ea24-253">c.</span><span class="sxs-lookup"><span data-stu-id="8ea24-253">c.</span></span> <span data-ttu-id="8ea24-254">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="8ea24-255">d.</span><span class="sxs-lookup"><span data-stu-id="8ea24-255">d.</span></span> <span data-ttu-id="8ea24-256">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="8ea24-257">e.</span><span class="sxs-lookup"><span data-stu-id="8ea24-257">e.</span></span> <span data-ttu-id="8ea24-258">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-258">Click **Next**.</span></span>
7. <span data-ttu-id="8ea24-259">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][22]
8. <span data-ttu-id="8ea24-261">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][23]
   
    <span data-ttu-id="8ea24-263">a.</span><span class="sxs-lookup"><span data-stu-id="8ea24-263">a.</span></span> <span data-ttu-id="8ea24-264">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="8ea24-265">b.</span><span class="sxs-lookup"><span data-stu-id="8ea24-265">b.</span></span> <span data-ttu-id="8ea24-266">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="8ea24-267">SuccessFactors 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8ea24-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="8ea24-268">Azure AD 사용자가 SuccessFactors에 로그인할 수 있도록 하려면 SuccessFactors로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="8ea24-269">SuccessFactors의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="8ea24-270">SuccessFactors에서 사용자를 생성하려면 [SuccessFactors 지원 팀](https://www.successfactors.com/en_us/support.html)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ea24-271">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="8ea24-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="8ea24-272">이 섹션은 Britta Simon에게 SuccessFactors에 대한 액세스 권한을 부여하여 Single Sign-On을 사용할 수 있도록 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![사용자 할당][24]

<span data-ttu-id="8ea24-274">**Britta Simon을 SuccessFactors에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8ea24-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="8ea24-275">클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![사용자 할당][25]
2. <span data-ttu-id="8ea24-277">응용 프로그램 목록에서 **SuccessFactors**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Single Sign-On 구성][26]
3. <span data-ttu-id="8ea24-279">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-279">In the menu on the top, click **Users**.</span></span>
   
    ![사용자 할당][27]
4. <span data-ttu-id="8ea24-281">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8ea24-282">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![사용자 할당][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8ea24-284">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="8ea24-284">Testing single sign-on</span></span>
<span data-ttu-id="8ea24-285">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8ea24-286">액세스 패널에서 SuccessFactors 타일을 클릭하면 SuccessFactors 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ea24-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ea24-287">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8ea24-287">Additional resources</span></span>
* [<span data-ttu-id="8ea24-288">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="8ea24-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ea24-289">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8ea24-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
