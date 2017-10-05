---
title: "자습서: Box와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Box 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="92d53-103">자습서: Box와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="92d53-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="92d53-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Box를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92d53-105">Box를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92d53-106">Box에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="92d53-107">사용자가 해당 Azure AD 계정으로 Box에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92d53-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92d53-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92d53-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92d53-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="92d53-110">Prerequisites</span></span>

<span data-ttu-id="92d53-111">Box와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="92d53-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="92d53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92d53-113">Box Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="92d53-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92d53-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92d53-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92d53-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="92d53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92d53-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92d53-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="92d53-118">Scenario description</span></span>
<span data-ttu-id="92d53-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92d53-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92d53-121">갤러리에서 Box 추가</span><span class="sxs-lookup"><span data-stu-id="92d53-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="92d53-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="92d53-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="92d53-123">갤러리에서 Box 추가</span><span class="sxs-lookup"><span data-stu-id="92d53-123">Adding Box from the gallery</span></span>
<span data-ttu-id="92d53-124">Box의 Azure AD 통합을 구성하려면 갤러리의 Box를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92d53-125">**갤러리에서 Box를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="92d53-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92d53-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92d53-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92d53-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="92d53-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="92d53-133">검색 상자에 **Box**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-133">In the search box, type **Box**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="92d53-135">결과 패널에서 **Box**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92d53-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="92d53-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92d53-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Box에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="92d53-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Box 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="92d53-140">즉, Azure AD 사용자와 Box의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="92d53-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Box의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="92d53-142">Box에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92d53-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92d53-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92d53-145">**[Box 테스트 사용자 만들기](#creating-a-box-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Box에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92d53-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92d53-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92d53-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="92d53-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92d53-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Box 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="92d53-150">**Box에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="92d53-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="92d53-151">Azure Portal의 **Box** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="92d53-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="92d53-155">**Box 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="92d53-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="92d53-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92d53-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-158">This value is not real.</span></span> <span data-ttu-id="92d53-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="92d53-160">이 값을 얻으려면 [Box 클라이언트 지원 팀](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="92d53-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="92d53-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="92d53-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92d53-165">응용 프로그램에 대해 SSO를 구성하려면 [Box 클라이언트 지원 팀](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire)에 문의하고 다운로드한 XML 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="92d53-166">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92d53-167">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92d53-168">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92d53-169">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="92d53-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="92d53-170">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="92d53-172">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="92d53-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92d53-173">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92d53-175">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92d53-177">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92d53-179">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92d53-181">a.</span><span class="sxs-lookup"><span data-stu-id="92d53-181">a.</span></span> <span data-ttu-id="92d53-182">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92d53-183">b.</span><span class="sxs-lookup"><span data-stu-id="92d53-183">b.</span></span> <span data-ttu-id="92d53-184">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92d53-185">c.</span><span class="sxs-lookup"><span data-stu-id="92d53-185">c.</span></span> <span data-ttu-id="92d53-186">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92d53-187">d.</span><span class="sxs-lookup"><span data-stu-id="92d53-187">d.</span></span> <span data-ttu-id="92d53-188">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="92d53-189">Box 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="92d53-189">Creating a Box test user</span></span>

<span data-ttu-id="92d53-190">이 섹션에서는 Box에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="92d53-191">Box는 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="92d53-192">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-192">There is no action item for you in this section.</span></span> <span data-ttu-id="92d53-193">사용자가 Box에 존재하지 않는 경우 Box에 액세스하려고 할 때 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92d53-194">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="92d53-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92d53-195">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Box에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![사용자 할당][200] 

<span data-ttu-id="92d53-197">**Britta Simon을 Box에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="92d53-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="92d53-198">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="92d53-200">응용 프로그램 목록에서 **Box**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-200">In the applications list, select **Box**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="92d53-202">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-202">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="92d53-204">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-204">Click **Add** button.</span></span> <span data-ttu-id="92d53-205">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="92d53-207">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92d53-208">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92d53-209">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92d53-210">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="92d53-210">Testing single sign-on</span></span>

<span data-ttu-id="92d53-211">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92d53-212">[액세스 패널]에서 [Box] 타일을 클릭하면 로그인 페이지가 나타나서 Box 응용 프로그램에 로그온할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d53-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92d53-213">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="92d53-213">Additional resources</span></span>

* [<span data-ttu-id="92d53-214">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="92d53-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92d53-215">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="92d53-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="92d53-216">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="92d53-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

