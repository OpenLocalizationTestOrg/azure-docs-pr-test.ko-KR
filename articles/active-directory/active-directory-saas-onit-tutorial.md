---
title: "자습서: Onit과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Onit 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 47c0055b89dbcf6a30a7f9ac5a33913e7bf463fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="211ee-103">자습서: Onit과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="211ee-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="211ee-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Onit를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="211ee-105">Onit를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="211ee-106">Onit에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="211ee-107">사용자가 해당 Azure AD 계정으로 Onit에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="211ee-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="211ee-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="211ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="211ee-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="211ee-110">Prerequisites</span></span>

<span data-ttu-id="211ee-111">Onit와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="211ee-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="211ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="211ee-113">Onit Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="211ee-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="211ee-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="211ee-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="211ee-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="211ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="211ee-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="211ee-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="211ee-118">Scenario description</span></span>

<span data-ttu-id="211ee-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="211ee-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="211ee-121">갤러리에서 Onit 추가</span><span class="sxs-lookup"><span data-stu-id="211ee-121">Adding Onit from the gallery</span></span>
2. <span data-ttu-id="211ee-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="211ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="211ee-123">갤러리에서 Onit 추가</span><span class="sxs-lookup"><span data-stu-id="211ee-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="211ee-124">Onit의 Azure AD 통합을 구성하려면 갤러리의 Onit를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="211ee-125">**갤러리에서 Onit를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="211ee-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="211ee-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="211ee-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="211ee-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="211ee-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="211ee-133">검색 상자에 **Onit**를 입력하고 결과 패널에서 **Onit**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="211ee-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="211ee-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="211ee-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Onit에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="211ee-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Onit 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="211ee-138">즉, Azure AD 사용자와 Onit의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="211ee-139">Onit에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="211ee-140">Onit에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="211ee-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="211ee-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="211ee-143">**[Onit 테스트 사용자 만들기](#create-an-onit-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Onit에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="211ee-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="211ee-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="211ee-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="211ee-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="211ee-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Onit 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="211ee-148">**Onit에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="211ee-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="211ee-149">Azure Portal의 **Onit** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="211ee-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="211ee-153">**Onit 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Onit 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="211ee-155">a.</span><span class="sxs-lookup"><span data-stu-id="211ee-155">a.</span></span> <span data-ttu-id="211ee-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="211ee-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="211ee-157">b.</span><span class="sxs-lookup"><span data-stu-id="211ee-157">b.</span></span> <span data-ttu-id="211ee-158">**식별자** 텍스트 상자에서 `https://<sub-domain>.onit.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="211ee-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-159">These values are not real.</span></span> <span data-ttu-id="211ee-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="211ee-161">이러한 값을 얻으려면 [Onit 클라이언트 지원팀](https://www.onit.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="211ee-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="211ee-162">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="211ee-164">Onit 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="211ee-165">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="211ee-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="211ee-166">응용 프로그램의 **"특성"** 탭에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="211ee-167">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-167">The following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="211ee-169">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="211ee-170">특성 이름</span><span class="sxs-lookup"><span data-stu-id="211ee-170">Attribute Name</span></span> | <span data-ttu-id="211ee-171">특성 값</span><span class="sxs-lookup"><span data-stu-id="211ee-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="211ee-172">email</span><span class="sxs-lookup"><span data-stu-id="211ee-172">email</span></span> | <span data-ttu-id="211ee-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="211ee-173">user.mail</span></span> |
    
    <span data-ttu-id="211ee-174">a.</span><span class="sxs-lookup"><span data-stu-id="211ee-174">a.</span></span> <span data-ttu-id="211ee-175">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="211ee-178">b.</span><span class="sxs-lookup"><span data-stu-id="211ee-178">b.</span></span> <span data-ttu-id="211ee-179">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="211ee-180">c.</span><span class="sxs-lookup"><span data-stu-id="211ee-180">c.</span></span> <span data-ttu-id="211ee-181">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="211ee-182">d.</span><span class="sxs-lookup"><span data-stu-id="211ee-182">d.</span></span> <span data-ttu-id="211ee-183">**네임스페이스**를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="211ee-184">e.</span><span class="sxs-lookup"><span data-stu-id="211ee-184">e.</span></span> <span data-ttu-id="211ee-185">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-185">Click **Ok**.</span></span>

7. <span data-ttu-id="211ee-186">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-186">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="211ee-188">**Onit 구성** 섹션에서 **Onit 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="211ee-189">**빠른 참조 섹션**에서 **로그아웃 URL, SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Onit 구성](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="211ee-191">다른 웹 브라우저 창에서 Onit 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="211ee-192">위쪽의 메뉴에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="211ee-193">![관리](./media/active-directory-saas-onit-tutorial/IC791174.png "관리")</span><span class="sxs-lookup"><span data-stu-id="211ee-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="211ee-194">**회사 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="211ee-195">![회사 편집](./media/active-directory-saas-onit-tutorial/IC791175.png "회사 편집")</span><span class="sxs-lookup"><span data-stu-id="211ee-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="211ee-196">**보안** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="211ee-197">![회사 정보 편집](./media/active-directory-saas-onit-tutorial/IC791176.png "회사 정보 편집")</span><span class="sxs-lookup"><span data-stu-id="211ee-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="211ee-198">**보안** 탭에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="211ee-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="211ee-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="211ee-200">a.</span><span class="sxs-lookup"><span data-stu-id="211ee-200">a.</span></span> <span data-ttu-id="211ee-201">**인증 전략**으로 **Single Sign On 및 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="211ee-202">b.</span><span class="sxs-lookup"><span data-stu-id="211ee-202">b.</span></span> <span data-ttu-id="211ee-203">**IDP 대상 URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="211ee-204">c.</span><span class="sxs-lookup"><span data-stu-id="211ee-204">c.</span></span> <span data-ttu-id="211ee-205">**IDP 로그아웃 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그아웃 URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="211ee-206">d.</span><span class="sxs-lookup"><span data-stu-id="211ee-206">d.</span></span> <span data-ttu-id="211ee-207">**IDP 인증서 지문(SHA1)** 텍스트 상자에 Azure Portal에서 복사한 인증서의 **지문** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="211ee-208">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="211ee-209">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="211ee-210">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="211ee-211">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="211ee-211">Create an Azure AD test user</span></span>

<span data-ttu-id="211ee-212">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="211ee-214">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="211ee-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="211ee-215">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="211ee-217">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="211ee-219">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="211ee-221">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-221">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="211ee-223">a.</span><span class="sxs-lookup"><span data-stu-id="211ee-223">a.</span></span> <span data-ttu-id="211ee-224">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="211ee-225">b.</span><span class="sxs-lookup"><span data-stu-id="211ee-225">b.</span></span> <span data-ttu-id="211ee-226">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="211ee-227">c.</span><span class="sxs-lookup"><span data-stu-id="211ee-227">c.</span></span> <span data-ttu-id="211ee-228">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="211ee-229">d.</span><span class="sxs-lookup"><span data-stu-id="211ee-229">d.</span></span> <span data-ttu-id="211ee-230">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="211ee-231">Onit 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="211ee-231">Create an Onit test user</span></span>

<span data-ttu-id="211ee-232">Azure AD 사용자가 Onit에 로그인할 수 있도록 하려면 Onit으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="211ee-233">Onit의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="211ee-234">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="211ee-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="211ee-235">**Onit** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-235">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="211ee-236">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="211ee-237">![관리](./media/active-directory-saas-onit-tutorial/IC791180.png "관리")</span><span class="sxs-lookup"><span data-stu-id="211ee-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="211ee-238">**사용자 추가** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="211ee-239">![사용자 추가](./media/active-directory-saas-onit-tutorial/IC791181.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="211ee-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="211ee-240">관련된 텍스트 상자에 프로비전할 유효한 Azure AD 계정의 **이름** 및 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="211ee-241">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="211ee-242">Azure Active Directory 계정 보유자는 활성화되기 전에 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="211ee-243">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="211ee-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="211ee-244">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Onit에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="211ee-246">**Britta Simon을 Onit에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="211ee-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="211ee-247">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="211ee-249">응용 프로그램 목록에서 **Onit**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-249">In the applications list, select **Onit**.</span></span>

    ![응용 프로그램 목록의 Onit 링크](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="211ee-251">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-251">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="211ee-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-253">Click **Add** button.</span></span> <span data-ttu-id="211ee-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="211ee-256">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="211ee-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="211ee-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="211ee-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="211ee-259">Test single sign-on</span></span>

<span data-ttu-id="211ee-260">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="211ee-261">액세스 패널에서 Onit 타일을 클릭하면 Onit 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="211ee-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="211ee-262">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="211ee-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="211ee-263">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="211ee-263">Additional resources</span></span>

* [<span data-ttu-id="211ee-264">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="211ee-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="211ee-265">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="211ee-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

