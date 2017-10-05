---
title: "자습서: 15Five와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 15Five 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="3e472-103">자습서: 15Five와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3e472-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="3e472-104">이 자습서에서는 Azure AD(Azure Active Directory)와 15Five를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e472-105">15Five를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e472-106">15Five에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="3e472-107">사용자가 해당 Azure AD 계정으로 15Five에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e472-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e472-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e472-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e472-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e472-110">Prerequisites</span></span>

<span data-ttu-id="3e472-111">15Five와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="3e472-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3e472-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e472-113">15Five Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3e472-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e472-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e472-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e472-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3e472-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e472-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e472-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3e472-118">Scenario description</span></span>
<span data-ttu-id="3e472-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e472-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e472-121">갤러리에서 15Five 추가</span><span class="sxs-lookup"><span data-stu-id="3e472-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="3e472-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e472-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="3e472-123">갤러리에서 15Five 추가</span><span class="sxs-lookup"><span data-stu-id="3e472-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="3e472-124">15Five의 Azure AD 통합을 구성하려면 갤러리의 15Five를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e472-125">**갤러리에서 15Five를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e472-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e472-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e472-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e472-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3e472-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3e472-133">검색 상자에서 **15Five**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-133">In the search box, type **15Five**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="3e472-135">결과 창에서 **15Five**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e472-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3e472-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e472-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 15Five에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e472-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 15Five 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="3e472-140">즉, Azure AD 사용자와 15Five의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="3e472-141">15Five에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e472-142">15Five에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e472-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e472-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e472-145">**[15Five 테스트 사용자 만들기](#creating-a-15five-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 15Five에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e472-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e472-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e472-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3e472-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e472-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 15Five 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="3e472-150">**15Five에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e472-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="3e472-151">Azure Portal의 **15Five** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3e472-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="3e472-155">**15Five 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="3e472-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e472-157">a.</span></span> <span data-ttu-id="3e472-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="3e472-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="3e472-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e472-159">b.</span></span> <span data-ttu-id="3e472-160">**식별자** 텍스트 상자에서 `https://<companyname>.15five.com/saml2/metadata/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e472-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-161">These values are not real.</span></span> <span data-ttu-id="3e472-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3e472-163">이러한 값을 얻으려면 [15Five 클라이언트 지원 팀](https://www.15five.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3e472-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="3e472-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="3e472-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e472-168">**15Five** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [15Five 지원 팀](https://www.15five.com/contact/)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="3e472-169">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e472-170">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e472-171">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e472-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3e472-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e472-173">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3e472-175">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="3e472-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e472-176">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e472-178">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e472-180">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e472-182">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e472-184">a.</span><span class="sxs-lookup"><span data-stu-id="3e472-184">a.</span></span> <span data-ttu-id="3e472-185">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e472-186">b.</span><span class="sxs-lookup"><span data-stu-id="3e472-186">b.</span></span> <span data-ttu-id="3e472-187">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e472-188">c.</span><span class="sxs-lookup"><span data-stu-id="3e472-188">c.</span></span> <span data-ttu-id="3e472-189">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e472-190">d.</span><span class="sxs-lookup"><span data-stu-id="3e472-190">d.</span></span> <span data-ttu-id="3e472-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="3e472-192">15Five 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3e472-192">Creating a 15Five test user</span></span>

<span data-ttu-id="3e472-193">Azure AD 사용자가 15Five에 로그인할 수 있도록 하려면 15Five로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="3e472-194">15Five의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="3e472-195">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="3e472-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="3e472-196">**15Five** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="3e472-197">**회사 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="3e472-198">![회사 관리](./media/active-directory-saas-15five-tutorial/IC784675.png "회사 관리")</span><span class="sxs-lookup"><span data-stu-id="3e472-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="3e472-199">**사람\>사람 추가**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="3e472-200">![사람](./media/active-directory-saas-15five-tutorial/IC784676.png "사람")</span><span class="sxs-lookup"><span data-stu-id="3e472-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="3e472-201">새 사람 추가 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="3e472-202">![새 사람 추가](./media/active-directory-saas-15five-tutorial/IC784677.png "새 사람 추가")</span><span class="sxs-lookup"><span data-stu-id="3e472-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="3e472-203">a.</span><span class="sxs-lookup"><span data-stu-id="3e472-203">a.</span></span> <span data-ttu-id="3e472-204">관련 텍스트 상자에 프로비전할 유효한 Azure Active Directory 계정의 **이름**, **성**, **제목**, **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="3e472-205">b.</span><span class="sxs-lookup"><span data-stu-id="3e472-205">b.</span></span> <span data-ttu-id="3e472-206">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="3e472-207">Azure AD 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크를 포함한 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e472-208">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="3e472-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e472-209">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 15Five에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3e472-211">**Britta Simon을 15Five에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e472-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="3e472-212">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3e472-214">응용 프로그램 목록에서 **15Five**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-214">In the applications list, select **15Five**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="3e472-216">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-216">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3e472-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-218">Click **Add** button.</span></span> <span data-ttu-id="3e472-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3e472-221">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e472-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e472-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e472-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3e472-224">Testing single sign-on</span></span>

<span data-ttu-id="3e472-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e472-226">액세스 패널에서 15Five 타일을 클릭할 때 15Five 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e472-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="3e472-227">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e472-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3e472-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3e472-228">Additional resources</span></span>

* [<span data-ttu-id="3e472-229">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3e472-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e472-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3e472-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

