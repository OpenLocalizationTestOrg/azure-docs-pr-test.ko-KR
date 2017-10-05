---
title: "자습서: Citrix GoToMeeting과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 Citrix GoToMeeting 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="02369-103">자습서: Citrix GoToMeeting과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="02369-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="02369-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Citrix GoToMeeting을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="02369-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02369-105">Citrix GoToMeeting을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="02369-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02369-106">Citrix GoToMeeting에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="02369-107">사용자가 해당 Azure AD 계정으로 Citrix GoToMeeting에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02369-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="02369-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02369-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02369-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02369-110">Prerequisites</span></span>

<span data-ttu-id="02369-111">Citrix GoToMeeting과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="02369-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="02369-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02369-113">Citrix GoToMeeting Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="02369-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02369-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02369-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02369-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="02369-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02369-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02369-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="02369-118">Scenario description</span></span>
<span data-ttu-id="02369-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02369-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02369-121">갤러리에서 Citrix GoToMeeting 추가</span><span class="sxs-lookup"><span data-stu-id="02369-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="02369-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="02369-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="02369-123">갤러리에서 Citrix GoToMeeting 추가</span><span class="sxs-lookup"><span data-stu-id="02369-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="02369-124">Citrix GoToMeeting의 Azure AD 통합을 구성하려면 갤러리의 Citrix GoToMeeting을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02369-125">**갤러리에서 Citrix GoToMeeting을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="02369-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02369-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02369-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02369-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="02369-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="02369-133">검색 상자에 **Citrix GoToMeeting**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="02369-135">결과 패널에서 **Citrix GoToMeeting**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02369-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="02369-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02369-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Citrix GoToMeeting에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="02369-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Citrix GoToMeeting 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="02369-140">즉, Azure AD 사용자와 Citrix GoToMeeting의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="02369-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Citrix GoToMeeting의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="02369-142">Citrix GoToMeeting에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02369-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02369-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02369-145">**[Citrix GoToMeeting 테스트 사용자 만들기](#creating-a-citrix-gotomeeting-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Citrix GoToMeeting에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02369-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="02369-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02369-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02369-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="02369-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02369-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Citrix GoToMeeting 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="02369-150">**Citrix GoToMeeting에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="02369-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="02369-151">Azure Portal의 **Citrix GoToMeeting** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="02369-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="02369-155">**Citrix GoToMeeting 도메인 및 URL** 섹션에서는 아무런 단계도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="02369-157">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="02369-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-159">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="02369-161">Citrix GoToMeeting SAML 구성 섹션에서 [Citrix GoToMeeting SAML 구성]을 클릭하여 로그온 구성 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02369-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="02369-162">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="02369-163">다른 브라우저 창에서 [Citrix 조직 센터](https://account.citrixonline.com/organization/administration/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="02369-164">**ID 공급자** 탭을 클릭한 후에 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="02369-165">![SAML 설정](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="02369-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="02369-166">a.</span><span class="sxs-lookup"><span data-stu-id="02369-166">a.</span></span> <span data-ttu-id="02369-167">**수동**</span><span class="sxs-lookup"><span data-stu-id="02369-167">Select **Manual**</span></span>

    <span data-ttu-id="02369-168">b.</span><span class="sxs-lookup"><span data-stu-id="02369-168">b.</span></span> <span data-ttu-id="02369-169">Azure Portal **Citrix GoToMeeting에서 Single Sign-On 구성** 대화 상자 페이지에서 **SAML Single Sign-On 서비스 URL** 값을 복사한 다음 **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="02369-170">c.</span><span class="sxs-lookup"><span data-stu-id="02369-170">c.</span></span> <span data-ttu-id="02369-171">Azure Portal **Citrix GoToMeeting에서 Single Sign-On 구성** 대화 상자 페이지에서 **로그아웃 URL** 값을 복사한 다음 **로그아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="02369-172">d.</span><span class="sxs-lookup"><span data-stu-id="02369-172">d.</span></span> <span data-ttu-id="02369-173">Azure Portal **Citrix GoToMeeting에서 Single Sign-On 구성** 대화 상자 페이지에서 **SAML 엔터티 ID** 값을 복사한 다음 **ID 공급자 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="02369-174">e.</span><span class="sxs-lookup"><span data-stu-id="02369-174">e.</span></span> <span data-ttu-id="02369-175">다운로드한 인증서를 업로드하려면 **인증서 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="02369-176">f.</span><span class="sxs-lookup"><span data-stu-id="02369-176">f.</span></span> <span data-ttu-id="02369-177">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="02369-178">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="02369-179">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02369-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="02369-180">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02369-181">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="02369-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="02369-182">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02369-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="02369-184">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="02369-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02369-185">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02369-187">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02369-189">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02369-191">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02369-193">a.</span><span class="sxs-lookup"><span data-stu-id="02369-193">a.</span></span> <span data-ttu-id="02369-194">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02369-195">b.</span><span class="sxs-lookup"><span data-stu-id="02369-195">b.</span></span> <span data-ttu-id="02369-196">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02369-197">c.</span><span class="sxs-lookup"><span data-stu-id="02369-197">c.</span></span> <span data-ttu-id="02369-198">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="02369-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="02369-199">d.</span><span class="sxs-lookup"><span data-stu-id="02369-199">d.</span></span> <span data-ttu-id="02369-200">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="02369-201">Citrix GoToMeeting 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="02369-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="02369-202">이 섹션에서는 Citrix GoToMeeting에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02369-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="02369-203">Citrix GoToMeeting은 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="02369-204">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02369-204">There is no action item for you in this section.</span></span> <span data-ttu-id="02369-205">Citrix GoToMeeting에 사용자가 없는 경우 Citrix GoToMeeting에 액세스하려고 시도하면 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="02369-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="02369-206">사용자를 수동으로 만들어야 하는 경우 [Citrix GoToMeeting 지원 팀에 문의](https://care.citrixonline.com/gotomeeting)하세요.</span><span class="sxs-lookup"><span data-stu-id="02369-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="02369-207">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="02369-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="02369-208">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Citrix GoToMeeting에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![사용자 할당][200] 

<span data-ttu-id="02369-210">**Citrix GoToMeeting에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="02369-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="02369-211">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="02369-213">응용 프로그램 목록에서 **Citrix GoToMeeting**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="02369-215">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-215">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="02369-217">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-217">Click **Add** button.</span></span> <span data-ttu-id="02369-218">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="02369-220">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02369-221">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02369-222">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02369-223">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="02369-223">Testing single sign-on</span></span>

<span data-ttu-id="02369-224">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="02369-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="02369-225">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02369-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="02369-226">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02369-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02369-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="02369-227">Additional resources</span></span>

* [<span data-ttu-id="02369-228">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="02369-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02369-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="02369-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="02369-230">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="02369-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

