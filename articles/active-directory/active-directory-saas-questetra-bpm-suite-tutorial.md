---
title: "자습서: Questetra BPM Suite와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Questetra BPM Suite 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="76f57-103">자습서: Questetra BPM Suite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="76f57-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="76f57-104">이 자습서에서는 Questetra BPM Suite와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="76f57-105">Questetra BPM Suite를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="76f57-106">Azure AD에서 사용자의 Questetra BPM Suite에 대한 액세스 권한을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="76f57-107">사용자가 Azure AD 계정으로 Questetra BPM Suite에 자동으로 로그온(Single Sign-on)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="76f57-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="76f57-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76f57-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76f57-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="76f57-110">Prerequisites</span></span>
<span data-ttu-id="76f57-111">Questetra BPM Suite와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="76f57-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="76f57-112">An Azure AD subscription</span></span>
* <span data-ttu-id="76f57-113">[Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) Single-Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="76f57-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76f57-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="76f57-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="76f57-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="76f57-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="76f57-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="76f57-118">Scenario Description</span></span>
<span data-ttu-id="76f57-119">이 자습서는 테스트 환경에서 Azure AD Single Sign-on을 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="76f57-120">이 자습서에 설명된 시나리오는 다음 세 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="76f57-121">갤러리에서 Questetra BPM Suite 추가</span><span class="sxs-lookup"><span data-stu-id="76f57-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="76f57-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="76f57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="76f57-123">갤러리에서 Questetra BPM Suite 추가</span><span class="sxs-lookup"><span data-stu-id="76f57-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="76f57-124">Questetra BPM Suite가 Azure AD에 통합되도록 구성하려면 갤러리의 Questetra BPM Suite를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="76f57-125">**갤러리에서 Questetra BPM Suite를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="76f57-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="76f57-126">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="76f57-128">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="76f57-129">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2]

4. <span data-ttu-id="76f57-131">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-131">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]

5. <span data-ttu-id="76f57-133">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4]

6. <span data-ttu-id="76f57-135">검색 상자에 입력 **Questetra BPM Suite**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![응용 프로그램][5]

7. <span data-ttu-id="76f57-137">결과 창에서 **Questetra BPM Suite**를 선택한 다음 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76f57-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="76f57-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76f57-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Questetra BPM Suite에서 Azure AD Single Sign-on을 구성하고 테스트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76f57-140">Single Sign-On이 작동하려면 Azure AD는 Questetra BPM Suite를 사용하려는 사용자가 Azure AD의 어떤 사용자인지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="76f57-141">즉 Azure AD 사용자와 Questetra BPM Suite 사용자 간 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="76f57-142">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Questetra BPM Suite의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="76f57-143">Questetra BPM Suite에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="76f57-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="76f57-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76f57-146">**[Questetra BPM Suite 테스트 사용자 만들기](#creating-a-questetra-bpm-suite-test-user)** - Britta Simon이라는 Azure AD 사용자와 연결된 Questetra BPM Suite 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="76f57-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76f57-148">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76f57-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="76f57-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="76f57-150">이 섹션에서는 Azure 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Questetra BPM Suite에서 Single Sign-On을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="76f57-151">**Questetra BPM Suite에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="76f57-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="76f57-152">Azure 클래식 포털의 **Questetra BPM Suite** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][8]

2. <span data-ttu-id="76f57-154">**사용자가 Questetra BPM Suite에 로그인하는 방법을 선택하십시오.** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][9]

3. <span data-ttu-id="76f57-156">다른 웹 브라우저 창에서 **Questetra BPM Suite** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="76f57-157">위쪽의 메뉴에서 **System Settings**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Azure AD Single Sign-On][10]

5. <span data-ttu-id="76f57-159">**SingleSignOnSAML** 페이지를 열려면 **SSO(SAML)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD Single Sign-On][11]

6. <span data-ttu-id="76f57-161">Azure 클래식 포털의 **앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![앱 설정 구성][13]
   
    <span data-ttu-id="76f57-163">a.</span><span class="sxs-lookup"><span data-stu-id="76f57-163">a.</span></span> <span data-ttu-id="76f57-164">**Questetra BPM Suite** 회사 사이트의 [SP 정보] 섹션에서 **ACS URL**을 복사한 다음 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="76f57-165">b.</span><span class="sxs-lookup"><span data-stu-id="76f57-165">b.</span></span> <span data-ttu-id="76f57-166">**Questetra BPM Suite** 회사 사이트의 [SP 정보] 섹션에서 **Entity ID**를 복사한 다음 **발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="76f57-167">c.</span><span class="sxs-lookup"><span data-stu-id="76f57-167">c.</span></span> <span data-ttu-id="76f57-168">**Questetra BPM Suite** 회사 사이트의 [SP 정보] 섹션에서 **ACS URL**을 복사한 다음 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="76f57-169">d.</span><span class="sxs-lookup"><span data-stu-id="76f57-169">d.</span></span> <span data-ttu-id="76f57-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-170">Click **Next**.</span></span>

7. <span data-ttu-id="76f57-171">**Questetra BPM Suite에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭한 다음 인증서 파일을 컴퓨터에 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Single Sign-on 구성][14]

8. <span data-ttu-id="76f57-173">**Questetra BPM Suite** 회사 사이트에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Single Sign-On 구성][15]
   
    <span data-ttu-id="76f57-175">a.</span><span class="sxs-lookup"><span data-stu-id="76f57-175">a.</span></span> <span data-ttu-id="76f57-176">**Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="76f57-177">b.</span><span class="sxs-lookup"><span data-stu-id="76f57-177">b.</span></span> <span data-ttu-id="76f57-178">Azure 클래식 포털에서 **발급자 URL** 값을 복사한 다음 **Entity ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="76f57-179">c.</span><span class="sxs-lookup"><span data-stu-id="76f57-179">c.</span></span> <span data-ttu-id="76f57-180">Azure 클래식 포털에서 **Single Sign-On 서비스 URL** 값을 복사한 다음 **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="76f57-181">d.</span><span class="sxs-lookup"><span data-stu-id="76f57-181">d.</span></span> <span data-ttu-id="76f57-182">Azure 클래식 포털에서 **Single Sign-Out 서비스 URL** 값을 복사한 다음 **로그아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="76f57-183">e.</span><span class="sxs-lookup"><span data-stu-id="76f57-183">e.</span></span> <span data-ttu-id="76f57-184">**NameID format** 텍스트 상자에서 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="76f57-185">f.</span><span class="sxs-lookup"><span data-stu-id="76f57-185">f.</span></span> <span data-ttu-id="76f57-186">다운로드한 인증서에서 Base-64로 인코딩된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="76f57-187">자세한 내용은 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76f57-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="76f57-188">g.</span><span class="sxs-lookup"><span data-stu-id="76f57-188">g.</span></span> <span data-ttu-id="76f57-189">Base-64로 인코딩된 인증서를 메모장에서 열고 내용을 클립보드에 복사한 다음 **인증서 유효성 검사** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="76f57-190">h.</span><span class="sxs-lookup"><span data-stu-id="76f57-190">h.</span></span> <span data-ttu-id="76f57-191">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-191">Click **Save**.</span></span>

1. <span data-ttu-id="76f57-192">Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect의 정의][17]

2. <span data-ttu-id="76f57-194">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect의 정의][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76f57-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="76f57-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="76f57-197">이 섹션의 목적은 Azure 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="76f57-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="76f57-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="76f57-199">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][100] 

2. <span data-ttu-id="76f57-201">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="76f57-202">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][101] 

4. <span data-ttu-id="76f57-204">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기][102] 

5. <span data-ttu-id="76f57-206">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][103]
   
    <span data-ttu-id="76f57-208">a.</span><span class="sxs-lookup"><span data-stu-id="76f57-208">a.</span></span> <span data-ttu-id="76f57-209">**사용자 유형**에서 **조직의 새 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="76f57-210">b.</span><span class="sxs-lookup"><span data-stu-id="76f57-210">b.</span></span> <span data-ttu-id="76f57-211">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="76f57-212">c.</span><span class="sxs-lookup"><span data-stu-id="76f57-212">c.</span></span> <span data-ttu-id="76f57-213">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-213">Click Next.</span></span>

6. <span data-ttu-id="76f57-214">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기][104] 
   
    <span data-ttu-id="76f57-216">a.</span><span class="sxs-lookup"><span data-stu-id="76f57-216">a.</span></span> <span data-ttu-id="76f57-217">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="76f57-218">b.</span><span class="sxs-lookup"><span data-stu-id="76f57-218">b.</span></span> <span data-ttu-id="76f57-219">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="76f57-220">c.</span><span class="sxs-lookup"><span data-stu-id="76f57-220">c.</span></span> <span data-ttu-id="76f57-221">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="76f57-222">d.</span><span class="sxs-lookup"><span data-stu-id="76f57-222">d.</span></span> <span data-ttu-id="76f57-223">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="76f57-224">e.</span><span class="sxs-lookup"><span data-stu-id="76f57-224">e.</span></span> <span data-ttu-id="76f57-225">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-225">Click **Next**.</span></span>

7. <span data-ttu-id="76f57-226">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][105]  

8. <span data-ttu-id="76f57-228">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][106]   
   
    <span data-ttu-id="76f57-230">a.</span><span class="sxs-lookup"><span data-stu-id="76f57-230">a.</span></span> <span data-ttu-id="76f57-231">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="76f57-232">b.</span><span class="sxs-lookup"><span data-stu-id="76f57-232">b.</span></span> <span data-ttu-id="76f57-233">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="76f57-234">Questetra BPM Suite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="76f57-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="76f57-235">이 섹션에서는 Questetra BPM Suite에서 Britta Simon이라는 사용자를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="76f57-236">**Questetra BPM Suite에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="76f57-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="76f57-237">Questetra BPM Suite 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="76f57-238">**시스템 설정 > 사용자 목록 > 새 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="76f57-239">새 사용자 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![테스트 사용자 만들기][300] 
   
    <span data-ttu-id="76f57-241">a.</span><span class="sxs-lookup"><span data-stu-id="76f57-241">a.</span></span> <span data-ttu-id="76f57-242">**Name** 텍스트 상자에 Britta 사용자의 Azure AD 내 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="76f57-243">b.</span><span class="sxs-lookup"><span data-stu-id="76f57-243">b.</span></span> <span data-ttu-id="76f57-244">**메일** 텍스트 상자에 Azure AD 내에서 Britta의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="76f57-245">c.</span><span class="sxs-lookup"><span data-stu-id="76f57-245">c.</span></span> <span data-ttu-id="76f57-246">**암호** 텍스트 상자에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="76f57-247">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="76f57-248">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="76f57-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="76f57-249">이 섹션에서는 Britta Simon에게 Questetra BPM Suite에 대한 액세스 권한을 부여하여 Azure Single Sign-On을 사용할 수 있도록 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Azure AD Connect의 정의][200]

<span data-ttu-id="76f57-251">**Britta Simon을 Questetra BPM Suite에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="76f57-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="76f57-252">Azure 클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Azure AD Connect의 정의][201]
2. <span data-ttu-id="76f57-254">응용 프로그램 목록에서 **Questetra BPM Suite**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Azure AD Connect의 정의][205]
3. <span data-ttu-id="76f57-256">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-256">In the menu on the top, click **Users**.</span></span>
   
    ![Azure AD Connect의 정의][202]
4. <span data-ttu-id="76f57-258">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Azure AD Connect의 정의][203]
5. <span data-ttu-id="76f57-260">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Azure AD Connect의 정의][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="76f57-262">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="76f57-262">Testing Single Sign-On</span></span>
<span data-ttu-id="76f57-263">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="76f57-264">액세스 패널에서 Questetra BPM Suite 타일을 클릭하면 Questetra BPM Suite 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f57-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="76f57-265">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="76f57-265">Additional Resources</span></span>
* [<span data-ttu-id="76f57-266">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="76f57-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76f57-267">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="76f57-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
