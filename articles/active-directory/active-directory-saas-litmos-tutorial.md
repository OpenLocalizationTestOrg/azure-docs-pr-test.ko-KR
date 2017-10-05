---
title: "자습서: Litmos와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Litmos 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="b7566-103">자습서: Litmos와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b7566-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="b7566-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Litmos를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7566-105">Litmos를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b7566-106">Litmos에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="b7566-107">사용자가 자신의 Azure AD 계정으로 Litmos에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b7566-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b7566-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7566-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7566-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b7566-110">Prerequisites</span></span>

<span data-ttu-id="b7566-111">Litmos와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="b7566-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b7566-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7566-113">Litmos Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b7566-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7566-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7566-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7566-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b7566-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7566-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7566-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b7566-118">Scenario description</span></span>
<span data-ttu-id="b7566-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7566-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7566-121">갤러리에서 Litmos 추가</span><span class="sxs-lookup"><span data-stu-id="b7566-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="b7566-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b7566-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="b7566-123">갤러리에서 Litmos 추가</span><span class="sxs-lookup"><span data-stu-id="b7566-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="b7566-124">Litmos의 Azure AD 통합을 구성하려면 갤러리의 Litmos를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7566-125">**갤러리에서 Litmos를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b7566-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7566-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="b7566-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b7566-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="b7566-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="b7566-133">검색 상자에 **Litmos**를 입력하고 결과 패널에서 **Litmos**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b7566-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b7566-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b7566-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Litmos에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7566-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Litmos 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="b7566-138">즉, Azure AD 사용자와 Litmos의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="b7566-139">Litmos에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b7566-140">Litmos에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7566-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b7566-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7566-143">**[Litmos 테스트 사용자 만들기](#create-a-litmos-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Litmos에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7566-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7566-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b7566-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b7566-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b7566-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Litmos 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="b7566-148">**Litmos에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b7566-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="b7566-149">Azure Portal의 **Litmos** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="b7566-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="b7566-153">**Litmos 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Litmos 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="b7566-155">a.</span><span class="sxs-lookup"><span data-stu-id="b7566-155">a.</span></span> <span data-ttu-id="b7566-156">**식별자** 텍스트 상자에서 `https://<companyname>.litmos.com/account/Login` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="b7566-157">b.</span><span class="sxs-lookup"><span data-stu-id="b7566-157">b.</span></span> <span data-ttu-id="b7566-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="b7566-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b7566-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-159">These values are not real.</span></span> <span data-ttu-id="b7566-160">이러한 값을 실제 식별자와 회신 URL로 업데이트합니다. 이러한 값은 자습서의 뒷부분에 나오거나 [Litmos 지원 팀](https://www.litmos.com/contact-us/)에 문의하여 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="b7566-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="b7566-163">구성의 일부로 Litmos 응용 프로그램에 대한 **SAML 토큰 특성** 을 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![특성 섹션](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="b7566-165">특성 이름</span><span class="sxs-lookup"><span data-stu-id="b7566-165">Attribute Name</span></span>   | <span data-ttu-id="b7566-166">특성 값</span><span class="sxs-lookup"><span data-stu-id="b7566-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="b7566-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="b7566-167">FirstName</span></span> |<span data-ttu-id="b7566-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b7566-168">user.givenname</span></span> |
    | <span data-ttu-id="b7566-169">LastName</span><span class="sxs-lookup"><span data-stu-id="b7566-169">LastName</span></span>  |<span data-ttu-id="b7566-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="b7566-170">user.surname</span></span> |
    | <span data-ttu-id="b7566-171">Email</span><span class="sxs-lookup"><span data-stu-id="b7566-171">Email</span></span> |<span data-ttu-id="b7566-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="b7566-172">user.mail</span></span> |

    <span data-ttu-id="b7566-173">a.</span><span class="sxs-lookup"><span data-stu-id="b7566-173">a.</span></span> <span data-ttu-id="b7566-174">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![특성 추가](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![특성 추가 대화 상자](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b7566-177">b.</span><span class="sxs-lookup"><span data-stu-id="b7566-177">b.</span></span> <span data-ttu-id="b7566-178">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="b7566-179">c.</span><span class="sxs-lookup"><span data-stu-id="b7566-179">c.</span></span> <span data-ttu-id="b7566-180">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b7566-181">d.</span><span class="sxs-lookup"><span data-stu-id="b7566-181">d.</span></span> <span data-ttu-id="b7566-182">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="b7566-183">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-183">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b7566-185">다른 브라우저 창에서 Litmos 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="b7566-186">왼쪽의 탐색 모음에서 **계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![앱 쪽의 계정 섹션][22] 

9. <span data-ttu-id="b7566-188">**통합** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-188">Click the **Integrations** tab.</span></span>
   
    ![통합 탭][23] 

10. <span data-ttu-id="b7566-190">**통합** 탭에서 **3rd 파티 통합**에 아래로 스크롤한 다음 **SAML 2.0** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 섹션][24] 

11. <span data-ttu-id="b7566-192">**The SAML endpoint for litmos is:**(litmos에 대한 SAML 끝점:) 아래의 값을 복사하여 Azure Portal에서 **Litmos 도메인 및 URL**에 있는 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML 끝점][26] 

12. <span data-ttu-id="b7566-194">**Litmos** 응용 프로그램에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Litmos 응용 프로그램][25] 
     
     <span data-ttu-id="b7566-196">a.</span><span class="sxs-lookup"><span data-stu-id="b7566-196">a.</span></span> <span data-ttu-id="b7566-197">**SAML 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="b7566-198">b.</span><span class="sxs-lookup"><span data-stu-id="b7566-198">b.</span></span> <span data-ttu-id="b7566-199">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **SAML X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="b7566-200">c.</span><span class="sxs-lookup"><span data-stu-id="b7566-200">c.</span></span> <span data-ttu-id="b7566-201">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b7566-202">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b7566-203">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b7566-204">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b7566-205">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b7566-205">Create an Azure AD test user</span></span>

<span data-ttu-id="b7566-206">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="b7566-208">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b7566-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7566-209">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b7566-211">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b7566-213">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b7566-215">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-215">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b7566-217">a.</span><span class="sxs-lookup"><span data-stu-id="b7566-217">a.</span></span> <span data-ttu-id="b7566-218">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7566-219">b.</span><span class="sxs-lookup"><span data-stu-id="b7566-219">b.</span></span> <span data-ttu-id="b7566-220">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b7566-221">c.</span><span class="sxs-lookup"><span data-stu-id="b7566-221">c.</span></span> <span data-ttu-id="b7566-222">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b7566-223">d.</span><span class="sxs-lookup"><span data-stu-id="b7566-223">d.</span></span> <span data-ttu-id="b7566-224">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="b7566-225">Litmos 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b7566-225">Create a Litmos test user</span></span>

<span data-ttu-id="b7566-226">이 섹션은 Litmos에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="b7566-227">Litmos 응용 프로그램은 적시에 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="b7566-228">즉, 필요한 경우 액세스 패널을 사용하여 응용 프로그램에 액세스하는 동안 사용자 계정은 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="b7566-229">**Litmos에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b7566-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="b7566-230">다른 브라우저 창에서 Litmos 회사 사이트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="b7566-231">왼쪽의 탐색 모음에서 **계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![앱 쪽의 계정 섹션][22] 

3. <span data-ttu-id="b7566-233">**통합** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-233">Click the **Integrations** tab.</span></span>
   
    ![통합 탭][23] 

4. <span data-ttu-id="b7566-235">**통합** 탭에서 **3rd 파티 통합**에 아래로 스크롤한 다음 **SAML 2.0** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="b7566-237">**Autogenerate Users**(사용자 자동 생성)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-237">Select **Autogenerate Users**</span></span>
   
    ![사용자 자동 생성][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b7566-239">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b7566-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="b7566-240">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Litmos에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="b7566-242">**Britta Simon을 Litmos에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b7566-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="b7566-243">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b7566-245">응용 프로그램 목록에서 **Litmos**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-245">In the applications list, select **Litmos**.</span></span>

    ![응용 프로그램 목록의 Litmos 링크](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="b7566-247">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-247">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="b7566-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-249">Click **Add** button.</span></span> <span data-ttu-id="b7566-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="b7566-252">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b7566-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7566-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b7566-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b7566-255">Test single sign-on</span></span>

<span data-ttu-id="b7566-256">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="b7566-257">액세스 패널에서 Litmos 타일을 클릭하면 Litmos 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7566-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b7566-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b7566-258">Additional resources</span></span>

* [<span data-ttu-id="b7566-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b7566-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7566-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b7566-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

