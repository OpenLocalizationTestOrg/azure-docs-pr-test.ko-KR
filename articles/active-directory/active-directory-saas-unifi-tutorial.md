---
title: "자습서: UNIFI와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 UNIFI 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="58933-103">자습서: UNIFI와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="58933-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="58933-104">이 자습서에서는 Azure AD(Azure Active Directory)와 UNIFI를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="58933-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58933-105">UNIFI를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="58933-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="58933-106">UNIFI에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="58933-107">사용자가 해당 Azure AD 계정으로 UNIFI에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58933-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="58933-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58933-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58933-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="58933-110">Prerequisites</span></span>

<span data-ttu-id="58933-111">UNIFI와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="58933-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="58933-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58933-113">UNIFI Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="58933-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58933-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58933-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58933-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="58933-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58933-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58933-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="58933-118">Scenario description</span></span>
<span data-ttu-id="58933-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58933-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58933-121">갤러리에서 UNIFI 추가</span><span class="sxs-lookup"><span data-stu-id="58933-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="58933-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="58933-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="58933-123">갤러리에서 UNIFI 추가</span><span class="sxs-lookup"><span data-stu-id="58933-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="58933-124">UNIFI의 Azure AD 통합을 구성하려면 갤러리의 UNIFI를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58933-125">**갤러리에서 UNIFI를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="58933-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58933-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="58933-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="58933-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="58933-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="58933-133">검색 상자에 **UNIFI**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-133">In the search box, type **UNIFI**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="58933-135">결과 패널에서 **UNIFI**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58933-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="58933-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58933-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 UNIFI에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58933-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 UNIFI 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="58933-140">즉, Azure AD 사용자와 UNIFI의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="58933-141">UNIFI에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="58933-142">UNIFI에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58933-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="58933-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58933-145">**[UNIFI 테스트 사용자 만들기](#creating-a-unifi-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 UNIFI에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58933-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="58933-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58933-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58933-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="58933-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="58933-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 UNIFI 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="58933-150">**UNIFI에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="58933-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="58933-151">Azure Portal의 **UNIFI** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="58933-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="58933-155">**UNIFI 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="58933-157">**식별자** 텍스트 상자에 해당 값으로 `INVIEWlabs`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="58933-158">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="58933-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="58933-160">**로그온 URL** 텍스트 상자에서 URL `https://app.discoverunifi.com/login`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="58933-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="58933-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="58933-165">**UNIFI 구성** 섹션에서 **UNIFI 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58933-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="58933-166">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="58933-168">다른 웹 브라우저 창에서 **UNIFI** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="58933-169">**사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-169">Click on the **Users**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="58933-171">**새 ID 공급자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-171">Click on the **Add New Identity Provider**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="58933-173">**ID 공급자 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="58933-175">a.</span><span class="sxs-lookup"><span data-stu-id="58933-175">a.</span></span> <span data-ttu-id="58933-176">**공급자 이름** 텍스트 상자에 ID 공급자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="58933-177">b.</span><span class="sxs-lookup"><span data-stu-id="58933-177">b.</span></span> <span data-ttu-id="58933-178">**공급자 URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="58933-179">c.</span><span class="sxs-lookup"><span data-stu-id="58933-179">c.</span></span> <span data-ttu-id="58933-180">Azure Portal에서 다운로드한 인증서를 메모장에서 열고 **---BEGIN CERTIFICATE---** 및 **---END CERTIFICATE---** 태그를 제거하고 나머지 내용을 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="58933-181">d.</span><span class="sxs-lookup"><span data-stu-id="58933-181">d.</span></span> <span data-ttu-id="58933-182">**is Default Provider**(기본 공급자임) 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="58933-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="58933-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58933-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="58933-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58933-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="58933-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="58933-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58933-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="58933-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="58933-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58933-190">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58933-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58933-194">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58933-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58933-198">a.</span><span class="sxs-lookup"><span data-stu-id="58933-198">a.</span></span> <span data-ttu-id="58933-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58933-200">b.</span><span class="sxs-lookup"><span data-stu-id="58933-200">b.</span></span> <span data-ttu-id="58933-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58933-202">c.</span><span class="sxs-lookup"><span data-stu-id="58933-202">c.</span></span> <span data-ttu-id="58933-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="58933-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="58933-204">d.</span><span class="sxs-lookup"><span data-stu-id="58933-204">d.</span></span> <span data-ttu-id="58933-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="58933-206">UNIFI 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="58933-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="58933-207">이 섹션에서는 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58933-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="58933-208">**UNIFI**는 자동 사용자 프로비전을 지원하므로 수동 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58933-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="58933-209">Azure AD에서 인증에 성공하면 사용자가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="58933-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="58933-210">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="58933-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="58933-211">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 UNIFI에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![사용자 할당][200] 

<span data-ttu-id="58933-213">**Britta Simon을 UNIFI에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="58933-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="58933-214">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="58933-216">응용 프로그램 목록에서 **UNIFI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-216">In the applications list, select **UNIFI**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="58933-218">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-218">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="58933-220">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-220">Click **Add** button.</span></span> <span data-ttu-id="58933-221">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="58933-223">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="58933-224">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58933-225">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="58933-226">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="58933-226">Testing single sign-on</span></span>

<span data-ttu-id="58933-227">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="58933-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="58933-228">액세스 패널에서 UNIFI 타일을 클릭하면 UNIFI 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="58933-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="58933-229">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58933-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="58933-230">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="58933-230">Additional resources</span></span>

* [<span data-ttu-id="58933-231">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="58933-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58933-232">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="58933-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

