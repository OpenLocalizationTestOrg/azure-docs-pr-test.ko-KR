---
title: "myPolicies와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 myPolicies 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: fcb403041cb3a8bd20ff7b34aa5cc4b7bf0c0a16
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="590b4-103">자습서: myPolicies와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="590b4-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="590b4-104">이 자습서에서는 Azure AD(Azure Active Directory)와 myPolicies을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="590b4-105">myPolicies를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="590b4-106">myPolicies에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-106">You can control in Azure AD who has access to myPolicies</span></span>
- <span data-ttu-id="590b4-107">사용자가 자신의 Azure AD 계정으로 myPolicies에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="590b4-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="590b4-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="590b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="590b4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="590b4-110">Prerequisites</span></span>

<span data-ttu-id="590b4-111">myPolicies와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-111">To configure Azure AD integration with myPolicies, you need the following items:</span></span>

- <span data-ttu-id="590b4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="590b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="590b4-113">myPolicies Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="590b4-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="590b4-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="590b4-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="590b4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="590b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="590b4-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="590b4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="590b4-118">Scenario description</span></span>
<span data-ttu-id="590b4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="590b4-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="590b4-121">갤러리에서 myPolicies 추가</span><span class="sxs-lookup"><span data-stu-id="590b4-121">Adding myPolicies from the gallery</span></span>
2. <span data-ttu-id="590b4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="590b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-the-gallery"></a><span data-ttu-id="590b4-123">갤러리에서 myPolicies 추가</span><span class="sxs-lookup"><span data-stu-id="590b4-123">Adding myPolicies from the gallery</span></span>
<span data-ttu-id="590b4-124">myPolicies가 Azure AD에 통합되도록 구성하려면 갤러리의 myPolicies를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="590b4-125">**갤러리에서 myPolicies를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="590b4-125">**To add myPolicies from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="590b4-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="590b4-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="590b4-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="590b4-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="590b4-133">검색 상자에 **myPolicies**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-133">In the search box, type **myPolicies**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="590b4-135">결과 패널에서 **myPolicies**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="590b4-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="590b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="590b4-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 myPolicies에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="590b4-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 myPolicies 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span></span> <span data-ttu-id="590b4-140">즉, Azure AD 사용자와 myPolicies의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span></span>

<span data-ttu-id="590b4-141">myPolicies에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="590b4-142">myPolicies에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="590b4-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="590b4-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="590b4-145">**[myPolicies 테스트 사용자 만들기](#creating-a-mypolicies-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 myPolicies에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="590b4-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="590b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="590b4-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="590b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="590b4-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 myPolicies 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="590b4-150">**myPolicies에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="590b4-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="590b4-151">Azure Portal의 **myPolicies** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="590b4-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="590b4-155">**myPolicies 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="590b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="590b4-157">a.</span></span> <span data-ttu-id="590b4-158">**식별자** 텍스트 상자에서 `https://<tenantname>.mypolicies.com/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="590b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="590b4-159">b.</span></span> <span data-ttu-id="590b4-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="590b4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="590b4-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-161">These values are not real.</span></span> <span data-ttu-id="590b4-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="590b4-163">이러한 값을 얻으려면 [myPolicies 지원 팀](mailto:support@mypolicies.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="590b4-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span></span>

4. <span data-ttu-id="590b4-164">myPolicies 응용 프로그램에는 특정 형식의 SAML 어설션이 필요하므로, SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="590b4-165">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-165">Configure the following claims for this application.</span></span> <span data-ttu-id="590b4-166">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="590b4-167">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-167">The following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="590b4-169">**사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="590b4-170">표시된 각 특성에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="590b4-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="590b4-171">Attribute Name</span></span> | <span data-ttu-id="590b4-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="590b4-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="590b4-173">givenname</span><span class="sxs-lookup"><span data-stu-id="590b4-173">givenname</span></span> | <span data-ttu-id="590b4-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="590b4-174">user.givenname</span></span> |
    | <span data-ttu-id="590b4-175">surname</span><span class="sxs-lookup"><span data-stu-id="590b4-175">surname</span></span> | <span data-ttu-id="590b4-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="590b4-176">user.surname</span></span> |
    | <span data-ttu-id="590b4-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="590b4-177">emailaddress</span></span> | <span data-ttu-id="590b4-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="590b4-178">user.mail</span></span> |
    | <span data-ttu-id="590b4-179">name</span><span class="sxs-lookup"><span data-stu-id="590b4-179">name</span></span> | <span data-ttu-id="590b4-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="590b4-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="590b4-181">a.</span><span class="sxs-lookup"><span data-stu-id="590b4-181">a.</span></span> <span data-ttu-id="590b4-182">특성을 클릭하여 **특성 편집** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-182">Click on the attribute to open the **Edit Attribute** dialog.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="590b4-184">b.</span><span class="sxs-lookup"><span data-stu-id="590b4-184">b.</span></span> <span data-ttu-id="590b4-185">**네임스페이스**에서 URL 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="590b4-186">c.</span><span class="sxs-lookup"><span data-stu-id="590b4-186">c.</span></span> <span data-ttu-id="590b4-187">**확인**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-187">Click **Ok** to save the setting.</span></span>
    
6. <span data-ttu-id="590b4-188">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="590b4-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-190">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="590b4-192">**myPolicies 구성** 섹션에서 **myPolicies 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span></span> <span data-ttu-id="590b4-193">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="590b4-195">**myPolicies** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서(Base64)** 및 **SAML Single Sign-On 서비스 URL**을 [myPolicies 지원 팀](mailto:support@mypolicies.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="590b4-196">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="590b4-197">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="590b4-198">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="590b4-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="590b4-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="590b4-200">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="590b4-202">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="590b4-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="590b4-203">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="590b4-205">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="590b4-207">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="590b4-209">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="590b4-211">a.</span><span class="sxs-lookup"><span data-stu-id="590b4-211">a.</span></span> <span data-ttu-id="590b4-212">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="590b4-213">b.</span><span class="sxs-lookup"><span data-stu-id="590b4-213">b.</span></span> <span data-ttu-id="590b4-214">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="590b4-215">c.</span><span class="sxs-lookup"><span data-stu-id="590b4-215">c.</span></span> <span data-ttu-id="590b4-216">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="590b4-217">d.</span><span class="sxs-lookup"><span data-stu-id="590b4-217">d.</span></span> <span data-ttu-id="590b4-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="590b4-219">myPolicies 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="590b4-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="590b4-220">이 섹션에서는 myPolicies에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="590b4-221">myPolicies 플랫폼에서 사용자를 추가하려면 [myPolicies 지원 팀](mailto:support@mypolicies.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="590b4-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span></span> <span data-ttu-id="590b4-222">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="590b4-223">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="590b4-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="590b4-224">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 myPolicies에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span></span>

![사용자 할당][200] 

<span data-ttu-id="590b4-226">**Britta Simon을 myPolicies에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="590b4-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="590b4-227">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="590b4-229">응용 프로그램 목록에서 **myPolicies**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-229">In the applications list, select **myPolicies**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="590b4-231">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-231">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="590b4-233">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-233">Click **Add** button.</span></span> <span data-ttu-id="590b4-234">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="590b4-236">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="590b4-237">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="590b4-238">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="590b4-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="590b4-239">Testing single sign-on</span></span>

<span data-ttu-id="590b4-240">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="590b4-241">액세스 패널에서 myPolicies 타일을 클릭하면 myPolicies 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="590b4-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span></span>
<span data-ttu-id="590b4-242">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="590b4-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="590b4-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="590b4-243">Additional resources</span></span>

* [<span data-ttu-id="590b4-244">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="590b4-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="590b4-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="590b4-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

