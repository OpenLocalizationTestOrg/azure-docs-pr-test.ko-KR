---
title: "etouches와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 etouches 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="a5578-103">자습서: etouches와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a5578-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="a5578-104">이 자습서에서는 Azure AD(Azure Active Directory)와 etouches를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5578-105">etouches를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5578-106">etouches에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="a5578-107">사용자가 해당 Azure AD 계정으로 etouches에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5578-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5578-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5578-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5578-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a5578-110">Prerequisites</span></span>

<span data-ttu-id="a5578-111">etouches와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="a5578-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a5578-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5578-113">etouches Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a5578-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5578-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5578-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5578-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a5578-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5578-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5578-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a5578-118">Scenario description</span></span>
<span data-ttu-id="a5578-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5578-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5578-121">갤러리에서 etouches 추가</span><span class="sxs-lookup"><span data-stu-id="a5578-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="a5578-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a5578-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="a5578-123">갤러리에서 etouches 추가</span><span class="sxs-lookup"><span data-stu-id="a5578-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="a5578-124">etouches의 Azure AD 통합을 구성하려면 갤러리의 etouches를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5578-125">**갤러리에서 etouches를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5578-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5578-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="a5578-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5578-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="a5578-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="a5578-133">검색 상자에 **etouches**를 입력하고 결과 패널에서 **etouches**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a5578-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a5578-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a5578-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 etouches에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5578-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 etouches 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="a5578-138">즉, Azure AD 사용자와 etouches의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="a5578-139">etouches에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5578-140">etouches에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5578-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5578-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5578-143">**[etouches 테스트 사용자 만들기](#create-an-etouches-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 etouches에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5578-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5578-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a5578-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a5578-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a5578-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 etouches 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="a5578-148">**etouches에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5578-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="a5578-149">Azure Portal의 **etouches** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a5578-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="a5578-153">**etouches 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![etouches 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="a5578-155">a.</span><span class="sxs-lookup"><span data-stu-id="a5578-155">a.</span></span> <span data-ttu-id="a5578-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="a5578-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="a5578-157">b.</span><span class="sxs-lookup"><span data-stu-id="a5578-157">b.</span></span> <span data-ttu-id="a5578-158">**식별자** 텍스트 상자에서 `https://www.eiseverywhere.com/<instance name>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5578-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-159">These values are not real.</span></span> <span data-ttu-id="a5578-160">자습서 뒷부분에 설명된 실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="a5578-161">etouches 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a5578-162">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-162">Configure the following claims for this application.</span></span> <span data-ttu-id="a5578-163">응용 프로그램의 **사용자 특성**에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="a5578-164">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-164">The following screenshot shows an example for this.</span></span> 

    ![사용자 특성](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="a5578-166">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="a5578-167">특성 이름</span><span class="sxs-lookup"><span data-stu-id="a5578-167">Attribute Name</span></span> | <span data-ttu-id="a5578-168">특성 값</span><span class="sxs-lookup"><span data-stu-id="a5578-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="a5578-169">Email</span><span class="sxs-lookup"><span data-stu-id="a5578-169">Email</span></span> | <span data-ttu-id="a5578-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="a5578-170">user.mail</span></span> |    
    
    <span data-ttu-id="a5578-171">a.</span><span class="sxs-lookup"><span data-stu-id="a5578-171">a.</span></span> <span data-ttu-id="a5578-172">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![특성 추가](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![특성 추가 대화 상자](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a5578-175">b.</span><span class="sxs-lookup"><span data-stu-id="a5578-175">b.</span></span> <span data-ttu-id="a5578-176">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="a5578-177">c.</span><span class="sxs-lookup"><span data-stu-id="a5578-177">c.</span></span> <span data-ttu-id="a5578-178">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a5578-179">d.</span><span class="sxs-lookup"><span data-stu-id="a5578-179">d.</span></span> <span data-ttu-id="a5578-180">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="a5578-181">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="a5578-183">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-183">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a5578-185">응용 프로그램에 SSO를 구성하려면 etouches 응용 프로그램에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![etouches 구성](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="a5578-187">a.</span><span class="sxs-lookup"><span data-stu-id="a5578-187">a.</span></span> <span data-ttu-id="a5578-188">관리자 권한을 사용하여 **etouches** 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="a5578-189">b.</span><span class="sxs-lookup"><span data-stu-id="a5578-189">b.</span></span> <span data-ttu-id="a5578-190">**SAML** 구성으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="a5578-191">c.</span><span class="sxs-lookup"><span data-stu-id="a5578-191">c.</span></span> <span data-ttu-id="a5578-192">**일반 설정** 섹션에서 메모장에서 Azure Portal에서 다운로드한 인증서를 열고 내용을 복사한 다음 IDP 메타데이터 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="a5578-193">d.</span><span class="sxs-lookup"><span data-stu-id="a5578-193">d.</span></span> <span data-ttu-id="a5578-194">**저장 및 유지** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="a5578-195">e.</span><span class="sxs-lookup"><span data-stu-id="a5578-195">e.</span></span> <span data-ttu-id="a5578-196">SAML 메타데이터 섹션에서 **메타데이터 업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="a5578-197">f.</span><span class="sxs-lookup"><span data-stu-id="a5578-197">f.</span></span> <span data-ttu-id="a5578-198">페이지가 열리고 SSO를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="a5578-199">SSO가 작동하면 username을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="a5578-200">g.</span><span class="sxs-lookup"><span data-stu-id="a5578-200">g.</span></span> <span data-ttu-id="a5578-201">Username 필드에서 아래 이미지에서 표시한 대로 **emailaddress**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="a5578-202">h.</span><span class="sxs-lookup"><span data-stu-id="a5578-202">h.</span></span> <span data-ttu-id="a5578-203">**SP 엔터티 ID** 값을 복사하고 Azure Portal의 **etouches 도메인 및 URL** 섹션에 있는 **식별자** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="a5578-204">i.</span><span class="sxs-lookup"><span data-stu-id="a5578-204">i.</span></span> <span data-ttu-id="a5578-205">**SSO URL / ACS** 값을 복사하고 Azure Portal의 **etouches 도메인 및 URL** 섹션에 있는 **로그온 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="a5578-206">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5578-207">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5578-208">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a5578-209">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a5578-209">Create an Azure AD test user</span></span>
<span data-ttu-id="a5578-210">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="a5578-212">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a5578-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5578-213">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5578-215">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5578-217">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5578-219">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5578-221">a.</span><span class="sxs-lookup"><span data-stu-id="a5578-221">a.</span></span> <span data-ttu-id="a5578-222">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5578-223">b.</span><span class="sxs-lookup"><span data-stu-id="a5578-223">b.</span></span> <span data-ttu-id="a5578-224">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5578-225">c.</span><span class="sxs-lookup"><span data-stu-id="a5578-225">c.</span></span> <span data-ttu-id="a5578-226">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5578-227">d.</span><span class="sxs-lookup"><span data-stu-id="a5578-227">d.</span></span> <span data-ttu-id="a5578-228">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="a5578-229">etouches 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a5578-229">Create an etouches test user</span></span>

<span data-ttu-id="a5578-230">이 섹션에서는 etouches에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="a5578-231">etouches 플랫폼에서 사용자를 추가하려면 [etouches 클라이언트 지원 팀](https://www.etouches.com/event-software/support/customer-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a5578-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a5578-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a5578-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="a5578-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 etouches에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="a5578-235">**Britta Simon을 etouches에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a5578-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="a5578-236">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a5578-238">응용 프로그램 목록에서 **etouches**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-238">In the applications list, select **etouches**.</span></span>

    ![응용 프로그램 목록의 etouches 링크](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="a5578-240">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-240">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="a5578-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-242">Click **Add** button.</span></span> <span data-ttu-id="a5578-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="a5578-245">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5578-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5578-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a5578-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a5578-248">Test single sign-on</span></span>


<span data-ttu-id="a5578-249">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5578-250">액세스 패널에서 etouches 타일을 클릭하면 etouches 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5578-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5578-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a5578-251">Additional resources</span></span>

* [<span data-ttu-id="a5578-252">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a5578-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5578-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a5578-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

