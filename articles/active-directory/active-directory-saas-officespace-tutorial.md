---
title: "자습서: OfficeSpace Software와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 OfficeSpace Software 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="14cfe-103">자습서: OfficeSpace Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="14cfe-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="14cfe-104">이 자습서에서는 Azure AD(Azure Active Directory)와 OfficeSpace Software를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14cfe-105">OfficeSpace Software를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14cfe-106">OfficeSpace Software에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="14cfe-107">사용자가 해당 Azure AD 계정으로 OfficeSpace Software에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="14cfe-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="14cfe-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14cfe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14cfe-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="14cfe-110">Prerequisites</span></span>

<span data-ttu-id="14cfe-111">OfficeSpace Software와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="14cfe-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="14cfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14cfe-113">OfficeSpace Software Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="14cfe-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14cfe-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14cfe-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="14cfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14cfe-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14cfe-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="14cfe-118">Scenario description</span></span>
<span data-ttu-id="14cfe-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14cfe-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14cfe-121">갤러리에서 OfficeSpace Software 추가</span><span class="sxs-lookup"><span data-stu-id="14cfe-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="14cfe-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="14cfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="14cfe-123">갤러리에서 OfficeSpace Software 추가</span><span class="sxs-lookup"><span data-stu-id="14cfe-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="14cfe-124">OfficeSpace Software의 Azure AD 통합을 구성하려면 갤러리의 OfficeSpace Software를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14cfe-125">**갤러리에서 OfficeSpace Software를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="14cfe-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14cfe-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="14cfe-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14cfe-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="14cfe-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="14cfe-133">검색 상자에 **OfficeSpace Software**를 입력하고 결과 패널에서 **OfficeSpace Software**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="14cfe-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="14cfe-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="14cfe-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 OfficeSpace Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14cfe-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 OfficeSpace Software 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="14cfe-138">즉, Azure AD 사용자와 OfficeSpace Software의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="14cfe-139">OfficeSpace Software에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="14cfe-140">OfficeSpace Software에서 Azure AD Single Sign-on을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14cfe-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="14cfe-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14cfe-143">**[OfficeSpace Software 테스트 사용자 만들기](#create-a-officespace-software-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 OfficeSpace Software에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="14cfe-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14cfe-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="14cfe-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="14cfe-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="14cfe-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 OfficeSpace Software 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="14cfe-148">**OfficeSpace Software에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="14cfe-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="14cfe-149">Azure Portal의 **OfficeSpace Software** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="14cfe-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="14cfe-153">**OfficeSpace Software 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![OfficeSpace Software 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="14cfe-155">a.</span><span class="sxs-lookup"><span data-stu-id="14cfe-155">a.</span></span> <span data-ttu-id="14cfe-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="14cfe-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="14cfe-157">b.</span><span class="sxs-lookup"><span data-stu-id="14cfe-157">b.</span></span> <span data-ttu-id="14cfe-158">**식별자** 텍스트 상자에서 `<company name>.officespacesoftware.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14cfe-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-159">These values are not real.</span></span> <span data-ttu-id="14cfe-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="14cfe-161">[OfficeSpace Software 클라이언트 지원 팀](mailto:support@officespacesoftware.com)에 문의하여 이러한 값을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="14cfe-162">OfficeSpace Software 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="14cfe-163">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="14cfe-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="14cfe-164">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="14cfe-165">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-165">The following screenshot shows an example for this.</span></span>
    
    ![특성 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="14cfe-167">**Single sign on** 대화 상자의 **사용자 특성** 섹션에서 **사용자 식별자**로 **user.mail**을 선택하고 아래 표에 표시되는 각 행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="14cfe-168">특성 이름</span><span class="sxs-lookup"><span data-stu-id="14cfe-168">Attribute Name</span></span> | <span data-ttu-id="14cfe-169">특성 값</span><span class="sxs-lookup"><span data-stu-id="14cfe-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="14cfe-170">email</span><span class="sxs-lookup"><span data-stu-id="14cfe-170">email</span></span> | <span data-ttu-id="14cfe-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="14cfe-171">user.mail</span></span> |
    | <span data-ttu-id="14cfe-172">name</span><span class="sxs-lookup"><span data-stu-id="14cfe-172">name</span></span> | <span data-ttu-id="14cfe-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="14cfe-173">user.displayname</span></span> |
    | <span data-ttu-id="14cfe-174">first_name</span><span class="sxs-lookup"><span data-stu-id="14cfe-174">first_name</span></span> | <span data-ttu-id="14cfe-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="14cfe-175">user.givenname</span></span> |
    | <span data-ttu-id="14cfe-176">last_name</span><span class="sxs-lookup"><span data-stu-id="14cfe-176">last_name</span></span> | <span data-ttu-id="14cfe-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="14cfe-177">user.surname</span></span> |

    <span data-ttu-id="14cfe-178">a.</span><span class="sxs-lookup"><span data-stu-id="14cfe-178">a.</span></span> <span data-ttu-id="14cfe-179">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="14cfe-180">추가 구성</span><span class="sxs-lookup"><span data-stu-id="14cfe-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![특성 구성](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="14cfe-182">b.</span><span class="sxs-lookup"><span data-stu-id="14cfe-182">b.</span></span> <span data-ttu-id="14cfe-183">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="14cfe-184">c.</span><span class="sxs-lookup"><span data-stu-id="14cfe-184">c.</span></span> <span data-ttu-id="14cfe-185">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="14cfe-186">d.</span><span class="sxs-lookup"><span data-stu-id="14cfe-186">d.</span></span> <span data-ttu-id="14cfe-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="14cfe-188">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="14cfe-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-190">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="14cfe-192">**OfficeSpace Software 구성** 섹션에서 **OfficeSpace Software 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="14cfe-193">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![OfficeSpace Software 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="14cfe-195">다른 웹 브라우저 창에서 OfficeSpace Software 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="14cfe-196">**설정**으로 이동한 후 **커넥터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-196">Go to **Settings** and click **Connectors**.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="14cfe-198">**SAML 인정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-198">Click **SAML Authentication**.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="14cfe-200">**SAML Authentication** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="14cfe-202">a.</span><span class="sxs-lookup"><span data-stu-id="14cfe-202">a.</span></span> <span data-ttu-id="14cfe-203">**로그아웃 공급자 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그아웃 URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="14cfe-204">b.</span><span class="sxs-lookup"><span data-stu-id="14cfe-204">b.</span></span> <span data-ttu-id="14cfe-205">**클라이언트 IDP 대상 URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="14cfe-206">c.</span><span class="sxs-lookup"><span data-stu-id="14cfe-206">c.</span></span> <span data-ttu-id="14cfe-207">Azure Portal에서 복사한 **지문** 값을 **클라이언트 IDP 인증서 지문** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="14cfe-208">d.</span><span class="sxs-lookup"><span data-stu-id="14cfe-208">d.</span></span> <span data-ttu-id="14cfe-209">**설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="14cfe-210">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14cfe-211">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14cfe-212">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="14cfe-213">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="14cfe-213">Create an Azure AD test user</span></span>

<span data-ttu-id="14cfe-214">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="14cfe-216">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="14cfe-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14cfe-217">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="14cfe-219">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="14cfe-221">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="14cfe-223">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-223">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="14cfe-225">a.</span><span class="sxs-lookup"><span data-stu-id="14cfe-225">a.</span></span> <span data-ttu-id="14cfe-226">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14cfe-227">b.</span><span class="sxs-lookup"><span data-stu-id="14cfe-227">b.</span></span> <span data-ttu-id="14cfe-228">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="14cfe-229">c.</span><span class="sxs-lookup"><span data-stu-id="14cfe-229">c.</span></span> <span data-ttu-id="14cfe-230">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="14cfe-231">d.</span><span class="sxs-lookup"><span data-stu-id="14cfe-231">d.</span></span> <span data-ttu-id="14cfe-232">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="14cfe-233">OfficeSpace Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="14cfe-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="14cfe-234">이 섹션의 목적은 OfficeSpace Software에서 Britta Simon이라는 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="14cfe-235">OfficeSpace Software는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="14cfe-236">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-236">There is no action item for you in this section.</span></span> <span data-ttu-id="14cfe-237">새 사용자가 아직 존재하지 않는 경우 OfficeSpace Software에 액세스하는 동안 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="14cfe-238">사용자를 수동으로 만들어야 하는 경우 [OfficeSpace Software 지원 팀](mailto:support@officespacesoftware.com)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="14cfe-239">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="14cfe-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="14cfe-240">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 OfficeSpace Software에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="14cfe-242">**Britta Simon을 OfficeSpace Software에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="14cfe-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="14cfe-243">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="14cfe-245">응용 프로그램 목록에서 **OfficeSpace Software**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![응용 프로그램 목록의 OfficeSpace Software 링크](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="14cfe-247">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-247">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="14cfe-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-249">Click **Add** button.</span></span> <span data-ttu-id="14cfe-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="14cfe-252">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="14cfe-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14cfe-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="14cfe-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="14cfe-255">Test single sign-on</span></span>

<span data-ttu-id="14cfe-256">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="14cfe-257">액세스 패널에서 OfficeSpace Software 타일을 클릭하면 OfficeSpace Software 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cfe-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14cfe-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="14cfe-258">Additional resources</span></span>

* [<span data-ttu-id="14cfe-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="14cfe-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14cfe-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="14cfe-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

