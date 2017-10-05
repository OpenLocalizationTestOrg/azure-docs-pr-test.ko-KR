---
title: "자습서: People과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 People 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="7cca2-103">자습서: People과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7cca2-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="7cca2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 People을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cca2-105">People을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7cca2-106">People에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="7cca2-107">사용자가 해당 Azure AD 계정으로 People에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7cca2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7cca2-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cca2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cca2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7cca2-110">Prerequisites</span></span>

<span data-ttu-id="7cca2-111">People과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="7cca2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7cca2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cca2-113">People Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7cca2-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cca2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cca2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cca2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7cca2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cca2-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cca2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7cca2-118">Scenario description</span></span>
<span data-ttu-id="7cca2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cca2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cca2-121">갤러리에서 People 추가</span><span class="sxs-lookup"><span data-stu-id="7cca2-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="7cca2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7cca2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="7cca2-123">갤러리에서 People 추가</span><span class="sxs-lookup"><span data-stu-id="7cca2-123">Adding People from the gallery</span></span>
<span data-ttu-id="7cca2-124">People의 Azure AD 통합을 구성하려면 갤러리의 People을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7cca2-125">**갤러리에서 People을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7cca2-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7cca2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7cca2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7cca2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7cca2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7cca2-133">검색 상자에 **People**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-133">In the search box, type **People**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="7cca2-135">결과 패널에서 **People**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7cca2-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7cca2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7cca2-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 People에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7cca2-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 People 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="7cca2-140">즉, Azure AD 사용자와 People의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="7cca2-141">People에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7cca2-142">People에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7cca2-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7cca2-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cca2-145">**[People 테스트 사용자 만들기](#creating-a-people-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 People에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cca2-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cca2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7cca2-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7cca2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7cca2-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 People 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="7cca2-150">**People에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7cca2-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="7cca2-151">Azure Portal의 **People** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7cca2-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="7cca2-155">**People 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="7cca2-157">a.</span><span class="sxs-lookup"><span data-stu-id="7cca2-157">a.</span></span> <span data-ttu-id="7cca2-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="7cca2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="7cca2-159">b.</span><span class="sxs-lookup"><span data-stu-id="7cca2-159">b.</span></span> <span data-ttu-id="7cca2-160">**식별자** 텍스트 상자에서 `https://www.peoplehr.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="7cca2-161">c.</span><span class="sxs-lookup"><span data-stu-id="7cca2-161">c.</span></span> <span data-ttu-id="7cca2-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="7cca2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7cca2-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-163">These values are not real.</span></span> <span data-ttu-id="7cca2-164">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7cca2-165">이러한 값을 얻으려면 [People 클라이언트 지원 팀](mailto:customerservices@peoplehr.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7cca2-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="7cca2-166">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="7cca2-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7cca2-170">응용 프로그램에 대해 구성된 SSO를 가져오려면 관리자 권한으로 People 테넌트에 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="7cca2-171">왼쪽 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-171">In the menu on the left side, click **Settings**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="7cca2-173">**회사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-173">Click **Company**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="7cca2-175">**‘Single Sign On’ SAML 메타데이터 파일 업로드**에서 **찾아보기**를 클릭하여 다운로드한 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="7cca2-177">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7cca2-178">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7cca2-179">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7cca2-180">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7cca2-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="7cca2-181">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7cca2-183">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7cca2-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7cca2-184">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7cca2-186">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7cca2-188">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7cca2-190">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7cca2-192">a.</span><span class="sxs-lookup"><span data-stu-id="7cca2-192">a.</span></span> <span data-ttu-id="7cca2-193">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cca2-194">b.</span><span class="sxs-lookup"><span data-stu-id="7cca2-194">b.</span></span> <span data-ttu-id="7cca2-195">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7cca2-196">c.</span><span class="sxs-lookup"><span data-stu-id="7cca2-196">c.</span></span> <span data-ttu-id="7cca2-197">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7cca2-198">d.</span><span class="sxs-lookup"><span data-stu-id="7cca2-198">d.</span></span> <span data-ttu-id="7cca2-199">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="7cca2-200">People 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7cca2-200">Creating a People test user</span></span>

<span data-ttu-id="7cca2-201">이 섹션에서는 People에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="7cca2-202">People 플랫폼에서 사용자를 추가하려면 [People 클라이언트 지원 팀](mailto:customerservices@peoplehr.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7cca2-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="7cca2-203">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7cca2-204">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7cca2-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7cca2-205">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 People에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7cca2-207">**Britta Simon을 People에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7cca2-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="7cca2-208">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7cca2-210">응용 프로그램 목록에서 **People**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-210">In the applications list, select **People**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="7cca2-212">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-212">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7cca2-214">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-214">Click **Add** button.</span></span> <span data-ttu-id="7cca2-215">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7cca2-217">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7cca2-218">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cca2-219">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7cca2-220">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7cca2-220">Testing single sign-on</span></span>

<span data-ttu-id="7cca2-221">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7cca2-222">액세스 패널에서 People 타일을 클릭하면 People 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cca2-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7cca2-223">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7cca2-223">Additional resources</span></span>

* [<span data-ttu-id="7cca2-224">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7cca2-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cca2-225">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7cca2-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

