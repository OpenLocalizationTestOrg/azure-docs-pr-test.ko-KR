---
title: "자습서: InTime과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 InTime 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 4bb22c92ad7f6963be6ca15073f7f01da99ba2bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="046bb-103">자습서: InTime과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="046bb-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="046bb-104">이 자습서에서는 Azure AD(Azure Active Directory)와 InTime을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-104">In this tutorial, you learn how to integrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="046bb-105">InTime을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-105">Integrating InTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="046bb-106">InTime에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-106">You can control in Azure AD who has access to InTime.</span></span>
- <span data-ttu-id="046bb-107">사용자가 해당 Azure AD 계정으로 InTime에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-107">You can enable your users to automatically get signed-on to InTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="046bb-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="046bb-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="046bb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="046bb-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="046bb-110">Prerequisites</span></span>

<span data-ttu-id="046bb-111">InTime과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-111">To configure Azure AD integration with InTime, you need the following items:</span></span>

- <span data-ttu-id="046bb-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="046bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="046bb-113">InTime Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="046bb-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="046bb-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="046bb-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="046bb-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="046bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="046bb-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="046bb-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="046bb-118">Scenario description</span></span>
<span data-ttu-id="046bb-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="046bb-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="046bb-121">갤러리에서 InTime 추가</span><span class="sxs-lookup"><span data-stu-id="046bb-121">Adding InTime from the gallery</span></span>
2. <span data-ttu-id="046bb-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="046bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-the-gallery"></a><span data-ttu-id="046bb-123">갤러리에서 InTime 추가</span><span class="sxs-lookup"><span data-stu-id="046bb-123">Adding InTime from the gallery</span></span>
<span data-ttu-id="046bb-124">InTime의 Azure AD 통합을 구성하려면 갤러리의 InTime을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-124">To configure the integration of InTime into Azure AD, you need to add InTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="046bb-125">**갤러리에서 InTime을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="046bb-125">**To add InTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="046bb-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="046bb-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="046bb-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="046bb-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="046bb-133">검색 상자에 **InTime**을 입력하고 결과 패널에서 **InTime**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-133">In the search box, type **InTime**, select **InTime** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="046bb-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="046bb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="046bb-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 InTime에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="046bb-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 InTime 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in InTime is to a user in Azure AD.</span></span> <span data-ttu-id="046bb-138">즉, Azure AD 사용자와 InTime의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-138">In other words, a link relationship between an Azure AD user and the related user in InTime needs to be established.</span></span>

<span data-ttu-id="046bb-139">InTime에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-139">In InTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="046bb-140">InTime에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-140">To configure and test Azure AD single sign-on with InTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="046bb-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="046bb-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="046bb-143">**[InTime 테스트 사용자 만들기](#create-a-intime-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 InTime에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-143">**[Create a InTime test user](#create-a-intime-test-user)** - to have a counterpart of Britta Simon in InTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="046bb-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="046bb-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="046bb-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="046bb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="046bb-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 InTime 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="046bb-148">**InTime에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="046bb-148">**To configure Azure AD single sign-on with InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="046bb-149">Azure Portal의 **InTime** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-149">In the Azure portal, on the **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="046bb-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="046bb-153">**InTime 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-153">On the **InTime Domain and URLs** section, perform the following steps:</span></span>

    ![InTime 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="046bb-155">a.</span><span class="sxs-lookup"><span data-stu-id="046bb-155">a.</span></span> <span data-ttu-id="046bb-156">**로그온 URL** 텍스트 상자에서 URL `https://intime6.intimesoft.com/mytime/login/login.xhtml`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-156">In the **Sign-on URL** textbox, type the URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="046bb-157">b.</span><span class="sxs-lookup"><span data-stu-id="046bb-157">b.</span></span> <span data-ttu-id="046bb-158">**식별자** 텍스트 상자에 URL `https://auth.intimesoft.com/auth/realms/master`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-158">In the **Identifier** textbox, type the URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="046bb-159">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="046bb-161">InTime 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰 특성 구성에 사용자 할당 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-161">Your InTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="046bb-162">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-162">The following screenshot shows an example for this.</span></span> <span data-ttu-id="046bb-163">**사용자 ID**의 기본값은 **user.userprincipalname**이지만 InTime에는 이것이 사용자의 전자 메일 주소와 매핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-163">The default value of **User Identifier** is **user.userprincipalname** but InTime expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="046bb-164">목록에서 **user.mail** 특성을 사용하거나 조직 구성을 기반으로 적절한 특성 값을 사용할 수 있기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-164">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span> 

    ![특성 구성](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="046bb-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-166">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="046bb-168">**InTime 구성** 섹션에서 **InTime 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-168">On the **InTime Configuration** section, click **Configure InTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="046bb-169">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![InTime 구성](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="046bb-171">**InTime** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**, **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 [InTime 지원 팀](mailto:hdollard@intimesoft.com)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-171">To configure single sign-on on **InTime** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="046bb-172">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="046bb-173">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="046bb-174">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="046bb-175">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="046bb-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="046bb-176">Create an Azure AD test user</span></span>

<span data-ttu-id="046bb-177">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="046bb-179">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="046bb-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="046bb-180">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="046bb-182">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="046bb-184">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="046bb-186">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-186">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="046bb-188">a.</span><span class="sxs-lookup"><span data-stu-id="046bb-188">a.</span></span> <span data-ttu-id="046bb-189">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="046bb-190">b.</span><span class="sxs-lookup"><span data-stu-id="046bb-190">b.</span></span> <span data-ttu-id="046bb-191">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="046bb-192">c.</span><span class="sxs-lookup"><span data-stu-id="046bb-192">c.</span></span> <span data-ttu-id="046bb-193">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="046bb-194">d.</span><span class="sxs-lookup"><span data-stu-id="046bb-194">d.</span></span> <span data-ttu-id="046bb-195">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="046bb-196">InTime 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="046bb-196">Create a InTime test user</span></span>

<span data-ttu-id="046bb-197">이 섹션에서는 InTime에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="046bb-198">InTime 플랫폼에서 사용자를 추가하려면 [InTime 지원 팀](mailto:hdollard@intimesoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="046bb-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) to add the users in the InTime platform.</span></span> <span data-ttu-id="046bb-199">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="046bb-200">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="046bb-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="046bb-201">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 InTime에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InTime.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="046bb-203">**Britta Simon을 InTime에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="046bb-203">**To assign Britta Simon to InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="046bb-204">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="046bb-206">응용 프로그램 목록에서 **InTime**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-206">In the applications list, select **InTime**.</span></span>

    ![응용 프로그램 목록의 InTime 링크](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="046bb-208">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-208">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="046bb-210">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-210">Click **Add** button.</span></span> <span data-ttu-id="046bb-211">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="046bb-213">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="046bb-214">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="046bb-215">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="046bb-216">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="046bb-216">Test single sign-on</span></span>

<span data-ttu-id="046bb-217">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="046bb-218">액세스 패널에서 InTime 타일을 클릭할 때 InTime 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-218">When you click the InTime tile in the Access Panel, you should get the login page of your InTime application.</span></span> <span data-ttu-id="046bb-219">**로그인** 단추를 클릭하면 단추의 목록에 일련의 IdP가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-219">Click the **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="046bb-220">[InTime 지원 팀](mailto:hdollard@intimesoft.com)에서 제공한 **IDP 이름**을 클릭하여 InTime 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="046bb-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) to login into your InTime application.</span></span> <span data-ttu-id="046bb-221">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="046bb-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="046bb-222">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="046bb-222">Additional resources</span></span>

* [<span data-ttu-id="046bb-223">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="046bb-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="046bb-224">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="046bb-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

