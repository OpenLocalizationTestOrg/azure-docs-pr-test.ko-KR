---
title: "자습서: Pantheon과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Pantheon 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="6abe8-103">자습서: Pantheon와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6abe8-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="6abe8-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Pantheon을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6abe8-105">Pantheon을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6abe8-106">Pantheon에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="6abe8-107">사용자가 해당 Azure AD 계정으로 Pantheon에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6abe8-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6abe8-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6abe8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6abe8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6abe8-110">Prerequisites</span></span>

<span data-ttu-id="6abe8-111">Pantheon과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="6abe8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6abe8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6abe8-113">Pantheon Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6abe8-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6abe8-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6abe8-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6abe8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6abe8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6abe8-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6abe8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6abe8-118">Scenario description</span></span>
<span data-ttu-id="6abe8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6abe8-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6abe8-121">갤러리에서 Pantheon 추가</span><span class="sxs-lookup"><span data-stu-id="6abe8-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="6abe8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6abe8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="6abe8-123">갤러리에서 Pantheon 추가</span><span class="sxs-lookup"><span data-stu-id="6abe8-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="6abe8-124">Pantheon의 Azure AD 통합을 구성하려면 갤러리의 Pantheon을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6abe8-125">**갤러리에서 Pantheon을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6abe8-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6abe8-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6abe8-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6abe8-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6abe8-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6abe8-133">검색 상자에 **Pantheon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-133">In the search box, type **Pantheon**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="6abe8-135">결과 패널에서 **Pantheon**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6abe8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6abe8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6abe8-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Pantheon에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6abe8-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Pantheon 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="6abe8-140">즉, Azure AD 사용자와 Pantheon의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="6abe8-141">Pantheon에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6abe8-142">Pantheon에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6abe8-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6abe8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6abe8-145">**[Pantheon 테스트 사용자 만들기](#creating-a-pantheon-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Pantheon에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6abe8-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6abe8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6abe8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6abe8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6abe8-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Pantheon 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="6abe8-150">**Pantheon에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6abe8-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="6abe8-151">Azure Portal의 **Pantheon** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6abe8-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="6abe8-155">**Pantheon 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="6abe8-157">a.</span><span class="sxs-lookup"><span data-stu-id="6abe8-157">a.</span></span> <span data-ttu-id="6abe8-158">**식별자** 텍스트 상자에서 `urn:auth0:pantheon:<orgname>-SSO` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="6abe8-159">b.</span><span class="sxs-lookup"><span data-stu-id="6abe8-159">b.</span></span> <span data-ttu-id="6abe8-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="6abe8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6abe8-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-161">These values are not real.</span></span> <span data-ttu-id="6abe8-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6abe8-163">이러한 값을 얻으려면 [Pantheon 지원 팀](https://pantheon.io/docs/getting-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6abe8-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="6abe8-164">Pantheon 응용 프로그램에는 특정 형식의 SAML 어설션이 필요하므로, 사용자의 메일 주소를 사용하여 UserIdentifier 특성 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="6abe8-165">기본적으로 Azure AD는 UserIdentifier 특성으로 UserPrincipalName을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="6abe8-166">하지만 성공적인 통합을 위해서는 사용자의 전자 메일 주소와 일치하도록 이 값을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="6abe8-167">올바른 매핑을 수행해야만 통합이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-167">The integration will only work after doing the correct mapping.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="6abe8-169">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="6abe8-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6abe8-173">**Pantheon 구성** 섹션에서 **Pantheon 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6abe8-174">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="6abe8-176">**Pantheon** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서** 및 **SAML Single Sign-On 서비스 URL**을 [Pantheon 지원 팀](https://pantheon.io/docs/getting-support/)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="6abe8-177">이 연결을 사용하도록 설정하려는 경우 전자 메일 도메인 정보 및 날짜/시간도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="6abe8-178">[여기](https://pantheon.io/docs/sso-organizations/)에서 이에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="6abe8-179">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6abe8-180">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6abe8-181">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6abe8-182">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6abe8-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6abe8-183">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6abe8-185">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="6abe8-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6abe8-186">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6abe8-188">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6abe8-190">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6abe8-192">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6abe8-194">a.</span><span class="sxs-lookup"><span data-stu-id="6abe8-194">a.</span></span> <span data-ttu-id="6abe8-195">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6abe8-196">b.</span><span class="sxs-lookup"><span data-stu-id="6abe8-196">b.</span></span> <span data-ttu-id="6abe8-197">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6abe8-198">c.</span><span class="sxs-lookup"><span data-stu-id="6abe8-198">c.</span></span> <span data-ttu-id="6abe8-199">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6abe8-200">d.</span><span class="sxs-lookup"><span data-stu-id="6abe8-200">d.</span></span> <span data-ttu-id="6abe8-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="6abe8-202">Pantheon 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6abe8-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="6abe8-203">이 섹션에서는 Pantheon에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="6abe8-204">아래 단계에 따라 Pantheon에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="6abe8-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="6abe8-205">SSO가 작동하려면 Pantheon에서 먼저 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="6abe8-206">관리자 자격 증명으로 Pantheon에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="6abe8-207">**조직** 대시보드 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="6abe8-208">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-208">Click **People**.</span></span>

4. <span data-ttu-id="6abe8-209">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-209">Click **Add user**.</span></span>

5. <span data-ttu-id="6abe8-210">사용자의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="6abe8-211">사용자의 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-211">Choose the user's role.</span></span>

7. <span data-ttu-id="6abe8-212">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6abe8-213">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6abe8-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6abe8-214">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Pantheon에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6abe8-216">**Britta Simon을 Pantheon에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6abe8-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="6abe8-217">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6abe8-219">응용 프로그램 목록에서 **Pantheon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-219">In the applications list, select **Pantheon**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="6abe8-221">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-221">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6abe8-223">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-223">Click **Add** button.</span></span> <span data-ttu-id="6abe8-224">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6abe8-226">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6abe8-227">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6abe8-228">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6abe8-229">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6abe8-229">Testing single sign-on</span></span>

<span data-ttu-id="6abe8-230">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6abe8-231">액세스 패널에서 Pantheon 타일을 클릭하면 Pantheon 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="6abe8-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="6abe8-232">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6abe8-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6abe8-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6abe8-233">Additional resources</span></span>

* [<span data-ttu-id="6abe8-234">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="6abe8-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6abe8-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6abe8-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

