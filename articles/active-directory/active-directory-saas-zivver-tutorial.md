---
title: "자습서: Azure Active Directory와 ZIVVER 통합| Microsoft Docs"
description: "Azure Active Directory와 ZIVVER 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d27c773baaae64922fc8ad2c8f65bab177769f67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="5a6ec-103">자습서: ZIVVER와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5a6ec-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="5a6ec-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ZIVVER를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-104">In this tutorial, you learn how to integrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a6ec-105">ZIVVER를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-105">Integrating ZIVVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5a6ec-106">ZIVVER에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-106">You can control in Azure AD who has access to ZIVVER.</span></span>
- <span data-ttu-id="5a6ec-107">사용자가 해당 Azure AD 계정으로 ZIVVER에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-107">You can enable your users to automatically get signed-on to ZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5a6ec-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5a6ec-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a6ec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5a6ec-110">Prerequisites</span></span>

<span data-ttu-id="5a6ec-111">ZIVVER와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-111">To configure Azure AD integration with ZIVVER, you need the following items:</span></span>

- <span data-ttu-id="5a6ec-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5a6ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a6ec-113">ZIVVER Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5a6ec-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a6ec-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a6ec-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a6ec-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a6ec-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a6ec-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5a6ec-118">Scenario description</span></span>
<span data-ttu-id="5a6ec-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a6ec-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a6ec-121">갤러리에서 ZIVVER 추가</span><span class="sxs-lookup"><span data-stu-id="5a6ec-121">Adding ZIVVER from the gallery</span></span>
2. <span data-ttu-id="5a6ec-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5a6ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-the-gallery"></a><span data-ttu-id="5a6ec-123">갤러리에서 ZIVVER 추가</span><span class="sxs-lookup"><span data-stu-id="5a6ec-123">Adding ZIVVER from the gallery</span></span>
<span data-ttu-id="5a6ec-124">ZIVVER의 Azure AD 통합을 구성하려면 갤러리의 ZIVVER를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-124">To configure the integration of ZIVVER into Azure AD, you need to add ZIVVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5a6ec-125">**갤러리에서 ZIVVER를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a6ec-125">**To add ZIVVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5a6ec-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="5a6ec-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5a6ec-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="5a6ec-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="5a6ec-133">검색 상자에 **ZIVVER**를 입력하고 결과 패널에서 **ZIVVER**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-133">In the search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5a6ec-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5a6ec-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5a6ec-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ZIVVER에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a6ec-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ZIVVER 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZIVVER is to a user in Azure AD.</span></span> <span data-ttu-id="5a6ec-138">즉, Azure AD 사용자와 ZIVVER의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-138">In other words, a link relationship between an Azure AD user and the related user in ZIVVER needs to be established.</span></span>

<span data-ttu-id="5a6ec-139">ZIVVER에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-139">In ZIVVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5a6ec-140">ZIVVER에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-140">To configure and test Azure AD single sign-on with ZIVVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5a6ec-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5a6ec-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a6ec-143">**[ZIVVER 테스트 사용자 만들기](#create-a-zivver-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ZIVVER에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - to have a counterpart of Britta Simon in ZIVVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a6ec-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a6ec-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5a6ec-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5a6ec-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5a6ec-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ZIVVER 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="5a6ec-148">**ZIVVER에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a6ec-148">**To configure Azure AD single sign-on with ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="5a6ec-149">Azure Portal의 **ZIVVER** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-149">In the Azure portal, on the **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="5a6ec-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="5a6ec-153">**ZIVVER 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-153">On the **ZIVVER Domain and URLs** section, perform the following steps:</span></span>

    ![ZIVVER 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="5a6ec-155">**식별자** 텍스트 상자에 URL `https://app.zivver.com/SAML/Zivver`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-155">In the **Identifier** textbox, type the URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="5a6ec-156">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="5a6ec-158">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-158">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a6ec-160">**ZIVVER** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [ZIVVER 지원 팀](https://support.zivver.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-160">To configure single sign-on on **ZIVVER** side, you need to send the downloaded **Metadata XML** to [ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="5a6ec-161">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-161">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5a6ec-162">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5a6ec-163">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5a6ec-164">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5a6ec-165">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5a6ec-165">Create an Azure AD test user</span></span>

<span data-ttu-id="5a6ec-166">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="5a6ec-168">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5a6ec-168">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5a6ec-169">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5a6ec-171">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5a6ec-173">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5a6ec-175">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-175">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5a6ec-177">a.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-177">a.</span></span> <span data-ttu-id="5a6ec-178">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-178">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a6ec-179">b.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-179">b.</span></span> <span data-ttu-id="5a6ec-180">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-180">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5a6ec-181">c.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-181">c.</span></span> <span data-ttu-id="5a6ec-182">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5a6ec-183">d.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-183">d.</span></span> <span data-ttu-id="5a6ec-184">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="5a6ec-185">ZIVVER 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5a6ec-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="5a6ec-186">이 섹션에서는 ZIVVER에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="5a6ec-187">ZIVVER 플랫폼에서 사용자를 추가하려면 [ZIVVER 지원 팀](https://support.zivver.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-187">Work with [ZIVVER support team](https://support.zivver.com) to add the users in the ZIVVER platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5a6ec-188">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5a6ec-188">Assign the Azure AD test user</span></span>

<span data-ttu-id="5a6ec-189">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ZIVVER에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZIVVER.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="5a6ec-191">**Britta Simon을 ZIVVER에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a6ec-191">**To assign Britta Simon to ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="5a6ec-192">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5a6ec-194">응용 프로그램 목록에서 **ZIVVER**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-194">In the applications list, select **ZIVVER**.</span></span>

    ![응용 프로그램 목록의 ZIVVER 연결](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="5a6ec-196">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-196">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="5a6ec-198">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-198">Click **Add** button.</span></span> <span data-ttu-id="5a6ec-199">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="5a6ec-201">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5a6ec-202">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a6ec-203">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5a6ec-204">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5a6ec-204">Test single sign-on</span></span>

<span data-ttu-id="5a6ec-205">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5a6ec-206">액세스 패널에서 ZIVVER 타일을 클릭하면 ZIVVER 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-206">When you click the ZIVVER tile in the Access Panel, you should get automatically signed-on to your ZIVVER application.</span></span>
<span data-ttu-id="5a6ec-207">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a6ec-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5a6ec-208">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5a6ec-208">Additional resources</span></span>

* [<span data-ttu-id="5a6ec-209">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5a6ec-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a6ec-210">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5a6ec-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

