---
title: "자습서: Evidence.com과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Evidence.com 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="7276f-103">자습서: Evidence.com과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7276f-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="7276f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Evidence.com을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7276f-105">Evidence.com을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7276f-106">Evidence.com에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="7276f-107">사용자가 해당 Azure AD 계정으로 Evidence.com에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7276f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7276f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7276f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7276f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7276f-110">Prerequisites</span></span>

<span data-ttu-id="7276f-111">Evidence.com과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="7276f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7276f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7276f-113">Evidence.com Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7276f-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7276f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7276f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7276f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7276f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7276f-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7276f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7276f-118">Scenario description</span></span>
<span data-ttu-id="7276f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7276f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7276f-121">갤러리에서 Evidence.com 추가</span><span class="sxs-lookup"><span data-stu-id="7276f-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="7276f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7276f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="7276f-123">갤러리에서 Evidence.com 추가</span><span class="sxs-lookup"><span data-stu-id="7276f-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="7276f-124">Evidence.com이 Azure AD에 통합되도록 구성하려면 갤러리의 Evidence.com을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7276f-125">**갤러리에서 Evidence.com을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7276f-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7276f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="7276f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7276f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="7276f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="7276f-133">검색 상자에서 **Evidence.com**을 입력하고, 결과 패널에서 **Evidence.com**을 선택한 다음, **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7276f-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7276f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7276f-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 Evidence.com에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7276f-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Evidence.com 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="7276f-138">즉 Azure AD 사용자와 Evidence.com의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="7276f-139">Evidence.com에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7276f-140">Evidence.com에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7276f-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7276f-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7276f-143">**[Evidence.com 테스트 사용자 만들기](#create-a-evidencecom-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Evidence.com에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7276f-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7276f-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7276f-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7276f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7276f-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Evidence.com 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="7276f-148">**Evidence.com에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7276f-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="7276f-149">Azure Portal의 **Evidence.com** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="7276f-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="7276f-153">**Evidence.com 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Evidence.com 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="7276f-155">a.</span><span class="sxs-lookup"><span data-stu-id="7276f-155">a.</span></span> <span data-ttu-id="7276f-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="7276f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="7276f-157">b.</span><span class="sxs-lookup"><span data-stu-id="7276f-157">b.</span></span> <span data-ttu-id="7276f-158">**식별자** 텍스트 상자에서 `https://<yourtenant>.evidence.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7276f-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-159">These values are not real.</span></span> <span data-ttu-id="7276f-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7276f-161">이러한 값을 얻으려면 [Evidence.com 클라이언트 지원 팀](https://communities.taser.com/support/SupportContactUs?typ=LE)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7276f-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="7276f-162">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="7276f-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7276f-166">**Evidence.com 구성** 섹션에서 **Evidence.com 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7276f-167">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evidence.com 구성](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="7276f-169">별도 웹 브라우저 창에서 Evidence.com 테넌트에 관리자 권한으로 로그인하고 **관리자** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="7276f-170">**Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="7276f-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="7276f-171">**SAML 기반 Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="7276f-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="7276f-172">Azure Portal에 표시된 **SAML 엔터티 ID**, **SAML Single Sign-On 서비스 URL** 및 **로그아웃 URL** 값을 Evidence.com의 해당 필드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="7276f-173">다운로드한 인증서(Base64) 파일을 메모장에서 열고 내용을 클립보드에 복사한 다음 **보안 인증서** 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="7276f-174">Evidence.com에서 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="7276f-175">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7276f-176">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7276f-177">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7276f-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7276f-178">Create an Azure AD test user</span></span>

<span data-ttu-id="7276f-179">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="7276f-181">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7276f-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7276f-182">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7276f-184">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7276f-186">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7276f-188">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-188">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7276f-190">a.</span><span class="sxs-lookup"><span data-stu-id="7276f-190">a.</span></span> <span data-ttu-id="7276f-191">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7276f-192">b.</span><span class="sxs-lookup"><span data-stu-id="7276f-192">b.</span></span> <span data-ttu-id="7276f-193">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7276f-194">c.</span><span class="sxs-lookup"><span data-stu-id="7276f-194">c.</span></span> <span data-ttu-id="7276f-195">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7276f-196">d.</span><span class="sxs-lookup"><span data-stu-id="7276f-196">d.</span></span> <span data-ttu-id="7276f-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="7276f-198">Evidence.com 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7276f-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="7276f-199">Azure AD 사용자가 로그인할 수 있도록 Evidence.com 응용 프로그램 내 액세스를 위해 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="7276f-200">이 섹션은 Evidence.com 내에 Azure AD 사용자 계정을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="7276f-201">**Evidence.com에서 사용자 계정을 프로비전하려면:**</span><span class="sxs-lookup"><span data-stu-id="7276f-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="7276f-202">웹 브라우저 창에서 Evidence.com 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="7276f-203">**관리자** 탭에 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="7276f-204">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="7276f-205">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="7276f-206">추가된 사용자의 **전자 메일 주소** 는 액세스 권한을 부여하려는 Azure AD 사용자의 사용자 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="7276f-207">조직에서 사용자 이름 및 이메일 주소가 동일한 값이 아닌 경우 Azure Portal의 **Evidence.com > 특성 > Single Sign-On** 섹션을 사용하여 Evidence.com에 보낼 nameidenitifer를 이메일 주소로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7276f-208">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7276f-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="7276f-209">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Evidence.com에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="7276f-211">**Britta Simon을 Evidence.com에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7276f-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="7276f-212">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7276f-214">응용 프로그램 목록에서 **Evidence.com**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-214">In the applications list, select **Evidence.com**.</span></span>

    ![응용 프로그램 목록의 Evidence.com 링크](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="7276f-216">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-216">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="7276f-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-218">Click **Add** button.</span></span> <span data-ttu-id="7276f-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="7276f-221">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7276f-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7276f-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7276f-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7276f-224">Test single sign-on</span></span>

<span data-ttu-id="7276f-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7276f-226">액세스 패널에서 Evidence.com 타일을 클릭하면 Evidence.com 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="7276f-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="7276f-227">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7276f-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7276f-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7276f-228">Additional resources</span></span>

* [<span data-ttu-id="7276f-229">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7276f-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7276f-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7276f-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

