---
title: "자습서: SD Elements와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SD Elements 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="42b08-103">자습서: SD Elements와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="42b08-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="42b08-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SD Elements를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42b08-105">SD Elements를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42b08-106">SD Elements에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="42b08-107">사용자가 해당 Azure AD 계정으로 SD Elements에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42b08-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42b08-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42b08-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42b08-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="42b08-110">Prerequisites</span></span>

<span data-ttu-id="42b08-111">SD Elements와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="42b08-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="42b08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42b08-113">SD Elements Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="42b08-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42b08-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42b08-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42b08-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="42b08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42b08-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42b08-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="42b08-118">Scenario description</span></span>
<span data-ttu-id="42b08-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42b08-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42b08-121">갤러리에서 SD Elements 추가</span><span class="sxs-lookup"><span data-stu-id="42b08-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="42b08-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="42b08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="42b08-123">갤러리에서 SD Elements 추가</span><span class="sxs-lookup"><span data-stu-id="42b08-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="42b08-124">SD Elements의 Azure AD 통합을 구성하려면 갤러리의 SD Elements를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42b08-125">**갤러리에서 SD Elements를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="42b08-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42b08-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42b08-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42b08-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="42b08-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="42b08-133">검색 상자에 **SD Elements**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-133">In the search box, type **SD Elements**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="42b08-135">결과 패널에서 **SD Elements**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42b08-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="42b08-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42b08-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 SD Elements에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42b08-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SD Elements 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="42b08-140">즉, Azure AD 사용자와 SD Elements의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="42b08-141">SD Elements에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42b08-142">SD Elements에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42b08-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42b08-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42b08-145">**[SD Elements 테스트 사용자 만들기](#creating-a-sd-elements-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 SD Elements에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42b08-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42b08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42b08-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="42b08-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42b08-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SD Elements 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="42b08-150">**SD Elements에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="42b08-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="42b08-151">Azure Portal의 **SD Elements** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="42b08-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="42b08-155">**SD Elements 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="42b08-157">a.</span><span class="sxs-lookup"><span data-stu-id="42b08-157">a.</span></span> <span data-ttu-id="42b08-158">**식별자** 텍스트 상자에서 `https://<tenantname>.sdelements.com/sso/saml2/metadata` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="42b08-159">b.</span><span class="sxs-lookup"><span data-stu-id="42b08-159">b.</span></span> <span data-ttu-id="42b08-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="42b08-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42b08-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-161">These values are not real.</span></span> <span data-ttu-id="42b08-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="42b08-163">이러한 값을 얻으려면 [SD Elements 지원 팀](mailto:support@sdelements.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="42b08-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="42b08-164">SD Elements 응용 프로그램에는 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="42b08-165">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-165">Configure the following claims for this application.</span></span> <span data-ttu-id="42b08-166">응용 프로그램의 **"사용자 특성"** 탭에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="42b08-167">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-167">The following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="42b08-169">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="42b08-170">특성 이름</span><span class="sxs-lookup"><span data-stu-id="42b08-170">Attribute Name</span></span> | <span data-ttu-id="42b08-171">특성 값</span><span class="sxs-lookup"><span data-stu-id="42b08-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="42b08-172">email</span><span class="sxs-lookup"><span data-stu-id="42b08-172">email</span></span> |<span data-ttu-id="42b08-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="42b08-173">user.mail</span></span> |
    | <span data-ttu-id="42b08-174">firstname</span><span class="sxs-lookup"><span data-stu-id="42b08-174">firstname</span></span> |<span data-ttu-id="42b08-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="42b08-175">user.givenname</span></span> |
    | <span data-ttu-id="42b08-176">lastname</span><span class="sxs-lookup"><span data-stu-id="42b08-176">lastname</span></span> |<span data-ttu-id="42b08-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="42b08-177">user.surname</span></span> |

    <span data-ttu-id="42b08-178">a.</span><span class="sxs-lookup"><span data-stu-id="42b08-178">a.</span></span> <span data-ttu-id="42b08-179">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="42b08-182">b.</span><span class="sxs-lookup"><span data-stu-id="42b08-182">b.</span></span> <span data-ttu-id="42b08-183">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="42b08-184">c.</span><span class="sxs-lookup"><span data-stu-id="42b08-184">c.</span></span> <span data-ttu-id="42b08-185">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="42b08-186">d.</span><span class="sxs-lookup"><span data-stu-id="42b08-186">d.</span></span> <span data-ttu-id="42b08-187">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="42b08-188">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="42b08-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-190">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="42b08-192">**SD Elements 구성** 섹션에서 **SD Elements 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42b08-193">**빠른 참조** 섹션에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="42b08-195">Single Sign-On을 사용하려면 [SD Elements 지원 팀](mailto:support@sdelements.com) 에 문의하고 다운로드한 인증서 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="42b08-196">다른 브라우저 창에서 SD Elements 테넌트에 관리자로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="42b08-197">위쪽의 메뉴에서 **시스템** 및 **Single Sign-On**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="42b08-199">**Single Sign-On 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="42b08-201">a.</span><span class="sxs-lookup"><span data-stu-id="42b08-201">a.</span></span> <span data-ttu-id="42b08-202">**SSO 형식**으로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="42b08-203">b.</span><span class="sxs-lookup"><span data-stu-id="42b08-203">b.</span></span> <span data-ttu-id="42b08-204">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **Identity Provider Entity ID**(ID 공급자 엔터티 ID) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="42b08-205">c.</span><span class="sxs-lookup"><span data-stu-id="42b08-205">c.</span></span> <span data-ttu-id="42b08-206">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **Identity Provider Single Sign-On Service**(ID 공급자 Single Sign-On 서비스) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="42b08-207">d.</span><span class="sxs-lookup"><span data-stu-id="42b08-207">d.</span></span> <span data-ttu-id="42b08-208">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="42b08-209">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42b08-210">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42b08-211">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42b08-212">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="42b08-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="42b08-213">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="42b08-215">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="42b08-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42b08-216">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42b08-218">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42b08-220">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42b08-222">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42b08-224">a.</span><span class="sxs-lookup"><span data-stu-id="42b08-224">a.</span></span> <span data-ttu-id="42b08-225">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42b08-226">b.</span><span class="sxs-lookup"><span data-stu-id="42b08-226">b.</span></span> <span data-ttu-id="42b08-227">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42b08-228">c.</span><span class="sxs-lookup"><span data-stu-id="42b08-228">c.</span></span> <span data-ttu-id="42b08-229">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42b08-230">d.</span><span class="sxs-lookup"><span data-stu-id="42b08-230">d.</span></span> <span data-ttu-id="42b08-231">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="42b08-232">SD Elements 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="42b08-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="42b08-233">이 섹션은 SD Elements에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="42b08-234">SD Elements의 경우 SD Elements 사용자를 만드는 작업은 수동입니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="42b08-235">**SD Elements에서 Britta Simon을 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="42b08-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="42b08-236">웹 브라우저 창에서 SD Elements 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="42b08-237">위쪽 메뉴에서 **사용자 관리**를 클릭한 다음 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![SD Elements 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="42b08-239">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-239">Click **Add New User**.</span></span>
   
    ![SD Elements 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="42b08-241">**새 사용자 추가** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![SD Elements 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="42b08-243">a.</span><span class="sxs-lookup"><span data-stu-id="42b08-243">a.</span></span> <span data-ttu-id="42b08-244">**메일** 텍스트 상자에 **brittasimon@contoso.com**과 같은 사용자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="42b08-245">b.</span><span class="sxs-lookup"><span data-stu-id="42b08-245">b.</span></span> <span data-ttu-id="42b08-246">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="42b08-247">c.</span><span class="sxs-lookup"><span data-stu-id="42b08-247">c.</span></span> <span data-ttu-id="42b08-248">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="42b08-249">d.</span><span class="sxs-lookup"><span data-stu-id="42b08-249">d.</span></span> <span data-ttu-id="42b08-250">**역할**로 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="42b08-251">e.</span><span class="sxs-lookup"><span data-stu-id="42b08-251">e.</span></span> <span data-ttu-id="42b08-252">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42b08-253">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="42b08-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42b08-254">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SD Elements에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![사용자 할당][200] 

<span data-ttu-id="42b08-256">**Britta Simon을 SD Elements에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="42b08-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="42b08-257">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="42b08-259">응용 프로그램 목록에서 **SD Elements**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-259">In the applications list, select **SD Elements**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="42b08-261">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-261">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="42b08-263">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-263">Click **Add** button.</span></span> <span data-ttu-id="42b08-264">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="42b08-266">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42b08-267">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42b08-268">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42b08-269">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="42b08-269">Testing single sign-on</span></span>

<span data-ttu-id="42b08-270">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="42b08-271">액세스 패널에서 SD Elements 타일을 클릭하면 SD Elements 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b08-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42b08-272">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="42b08-272">Additional resources</span></span>

* [<span data-ttu-id="42b08-273">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="42b08-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42b08-274">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="42b08-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

