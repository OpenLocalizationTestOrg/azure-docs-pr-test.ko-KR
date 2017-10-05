---
title: "자습서: Clever와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Clever 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="3efcf-103">자습서: Clever와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3efcf-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="3efcf-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Clever를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3efcf-105">Clever를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3efcf-106">Clever에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="3efcf-107">사용자가 해당 Azure AD 계정으로 Clever에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3efcf-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3efcf-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3efcf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3efcf-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3efcf-110">Prerequisites</span></span>

<span data-ttu-id="3efcf-111">Clever와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="3efcf-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3efcf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3efcf-113">Clever Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3efcf-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3efcf-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3efcf-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3efcf-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3efcf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3efcf-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3efcf-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3efcf-118">Scenario description</span></span>
<span data-ttu-id="3efcf-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3efcf-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3efcf-121">갤러리에서 Clever 추가</span><span class="sxs-lookup"><span data-stu-id="3efcf-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="3efcf-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3efcf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="3efcf-123">갤러리에서 Clever 추가</span><span class="sxs-lookup"><span data-stu-id="3efcf-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="3efcf-124">Clever의 Azure AD 통합을 구성하려면 갤러리의 Clever를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3efcf-125">**갤러리에서 Clever를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3efcf-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3efcf-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="3efcf-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3efcf-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="3efcf-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="3efcf-133">검색 상자에 **Clever**를 입력하고 결과 패널에서 **Clever**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3efcf-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3efcf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3efcf-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Clever에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3efcf-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Clever 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="3efcf-138">즉, Azure AD 사용자와 Clever의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="3efcf-139">Clever에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3efcf-140">Clever에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3efcf-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3efcf-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3efcf-143">**[Clever 테스트 사용자 만들기](#create-a-clever-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Clever에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3efcf-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3efcf-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3efcf-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3efcf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3efcf-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Clever 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="3efcf-148">**Clever에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3efcf-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="3efcf-149">Azure Portal의 **Clever** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="3efcf-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="3efcf-153">**Clever 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Clever 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="3efcf-155">a.</span><span class="sxs-lookup"><span data-stu-id="3efcf-155">a.</span></span> <span data-ttu-id="3efcf-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3efcf-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="3efcf-157">b.</span><span class="sxs-lookup"><span data-stu-id="3efcf-157">b.</span></span> <span data-ttu-id="3efcf-158">**식별자** 텍스트 상자에서 `https://clever.com/<companyname>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3efcf-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-159">These values are not real.</span></span> <span data-ttu-id="3efcf-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3efcf-161">이러한 값을 얻으려면 [Clever 클라이언트 지원팀](https://clever.com/about/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3efcf-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="3efcf-162">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="3efcf-164">Clever 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 **SAML 토큰 특성** 구성에 사용자 지정 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="3efcf-165">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-165">The following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="3efcf-167">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="3efcf-168">특성 이름</span><span class="sxs-lookup"><span data-stu-id="3efcf-168">Attribute Name</span></span>  | <span data-ttu-id="3efcf-169">특성 값</span><span class="sxs-lookup"><span data-stu-id="3efcf-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="3efcf-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="3efcf-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="3efcf-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="3efcf-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="3efcf-172">firstname</span><span class="sxs-lookup"><span data-stu-id="3efcf-172">Firstname</span></span>  | <span data-ttu-id="3efcf-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3efcf-173">user.givenname</span></span> |
    | <span data-ttu-id="3efcf-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="3efcf-174">Lastname</span></span>  | <span data-ttu-id="3efcf-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="3efcf-175">user.surname</span></span> |    

    <span data-ttu-id="3efcf-176">a.</span><span class="sxs-lookup"><span data-stu-id="3efcf-176">a.</span></span> <span data-ttu-id="3efcf-177">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="3efcf-180">b.</span><span class="sxs-lookup"><span data-stu-id="3efcf-180">b.</span></span> <span data-ttu-id="3efcf-181">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3efcf-182">c.</span><span class="sxs-lookup"><span data-stu-id="3efcf-182">c.</span></span> <span data-ttu-id="3efcf-183">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3efcf-184">d.</span><span class="sxs-lookup"><span data-stu-id="3efcf-184">d.</span></span> <span data-ttu-id="3efcf-185">**네임스페이스** 텍스트 상자를 비어 있는 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="3efcf-186">d.</span><span class="sxs-lookup"><span data-stu-id="3efcf-186">d.</span></span> <span data-ttu-id="3efcf-187">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="3efcf-188">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-188">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3efcf-190">**메타데이터** URL을 생성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="3efcf-191">a.</span><span class="sxs-lookup"><span data-stu-id="3efcf-191">a.</span></span> <span data-ttu-id="3efcf-192">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-192">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="3efcf-194">b.</span><span class="sxs-lookup"><span data-stu-id="3efcf-194">b.</span></span> <span data-ttu-id="3efcf-195">**끝점**을 클릭하여 **끝점** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="3efcf-197">c.</span><span class="sxs-lookup"><span data-stu-id="3efcf-197">c.</span></span> <span data-ttu-id="3efcf-198">복사 단추를 클릭하여 **페더레이션 메타데이터 문서** URL을 복사하여 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="3efcf-200">d.</span><span class="sxs-lookup"><span data-stu-id="3efcf-200">d.</span></span> <span data-ttu-id="3efcf-201">이제 **Clever**의 속성 페이지로 이동하고 **복사** 단추를 사용하여 **응용 프로그램 ID**를 복사하여 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="3efcf-203">e.</span><span class="sxs-lookup"><span data-stu-id="3efcf-203">e.</span></span> <span data-ttu-id="3efcf-204">`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 패턴을 사용하여 **메타데이터 URL**을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="3efcf-205">다른 웹 브라우저 창에서 Clever 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="3efcf-206">도구 모음에서 **인스턴트 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="3efcf-207">![인스턴트 로그인](./media/active-directory-saas-clever-tutorial/ic798984.png "인스턴트 로그인")</span><span class="sxs-lookup"><span data-stu-id="3efcf-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="3efcf-208">**인스턴트 로그인** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="3efcf-209">![인스턴트 로그인](./media/active-directory-saas-clever-tutorial/ic798985.png "인스턴트 로그인")</span><span class="sxs-lookup"><span data-stu-id="3efcf-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="3efcf-210">a.</span><span class="sxs-lookup"><span data-stu-id="3efcf-210">a.</span></span> <span data-ttu-id="3efcf-211">**로그인 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="3efcf-212">**로그인 URL** 은 사용자 지정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="3efcf-213">이 값을 얻으려면 [Clever 클라이언트 지원 팀](https://clever.com/about/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3efcf-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="3efcf-214">b.</span><span class="sxs-lookup"><span data-stu-id="3efcf-214">b.</span></span> <span data-ttu-id="3efcf-215">**ID 시스템**으로 **ADFS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="3efcf-216">c.</span><span class="sxs-lookup"><span data-stu-id="3efcf-216">c.</span></span> <span data-ttu-id="3efcf-217">**메타데이터 URL** 텍스트 상자에 **메타데이터 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="3efcf-218">d.</span><span class="sxs-lookup"><span data-stu-id="3efcf-218">d.</span></span> <span data-ttu-id="3efcf-219">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3efcf-220">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3efcf-221">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3efcf-222">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3efcf-223">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3efcf-223">Create an Azure AD test user</span></span>

<span data-ttu-id="3efcf-224">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="3efcf-226">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3efcf-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3efcf-227">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3efcf-229">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3efcf-231">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3efcf-233">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-233">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3efcf-235">a.</span><span class="sxs-lookup"><span data-stu-id="3efcf-235">a.</span></span> <span data-ttu-id="3efcf-236">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3efcf-237">b.</span><span class="sxs-lookup"><span data-stu-id="3efcf-237">b.</span></span> <span data-ttu-id="3efcf-238">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3efcf-239">c.</span><span class="sxs-lookup"><span data-stu-id="3efcf-239">c.</span></span> <span data-ttu-id="3efcf-240">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3efcf-241">d.</span><span class="sxs-lookup"><span data-stu-id="3efcf-241">d.</span></span> <span data-ttu-id="3efcf-242">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="3efcf-243">Clever 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3efcf-243">Create a Clever test user</span></span>

<span data-ttu-id="3efcf-244">Azure AD 사용자가 Clever에 로그인할 수 있도록 하려면 Clever로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="3efcf-245">Clever의 경우 Clever 플랫폼에 사용자를 추가하려면 [Clever 클라이언트 지원 팀](https://clever.com/about/contact/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="3efcf-246">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="3efcf-247">다른 Clever 사용자 계정 생성 도구 또는 Clever가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3efcf-248">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3efcf-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="3efcf-249">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Clever에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="3efcf-251">**Britta Simon을 Clever에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3efcf-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="3efcf-252">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3efcf-254">응용 프로그램 목록에서 **Clever**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-254">In the applications list, select **Clever**.</span></span>

    ![응용 프로그램 목록의 Clever 링크](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="3efcf-256">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-256">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="3efcf-258">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-258">Click **Add** button.</span></span> <span data-ttu-id="3efcf-259">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="3efcf-261">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3efcf-262">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3efcf-263">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3efcf-264">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3efcf-264">Test single sign-on</span></span>

<span data-ttu-id="3efcf-265">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3efcf-266">액세스 패널에서 Clever 타일을 클릭하면 Clever 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="3efcf-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="3efcf-267">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3efcf-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3efcf-268">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3efcf-268">Additional resources</span></span>

* [<span data-ttu-id="3efcf-269">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3efcf-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3efcf-270">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3efcf-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

