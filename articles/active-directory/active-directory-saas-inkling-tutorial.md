---
title: "자습서: Inkling과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Inkling 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="4bda7-103">자습서: Inkling과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4bda7-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="4bda7-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Inkling을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bda7-105">Inkling을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4bda7-106">Inkling에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="4bda7-107">사용자가 해당 Azure AD 계정으로 Inkling에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4bda7-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="4bda7-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bda7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bda7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4bda7-110">Prerequisites</span></span>

<span data-ttu-id="4bda7-111">Inkling과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="4bda7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4bda7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bda7-113">Inkling Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4bda7-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="4bda7-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="4bda7-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bda7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4bda7-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="4bda7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4bda7-118">Scenario description</span></span>
<span data-ttu-id="4bda7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bda7-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bda7-121">갤러리에서 Inkling 추가</span><span class="sxs-lookup"><span data-stu-id="4bda7-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="4bda7-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4bda7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="4bda7-123">갤러리에서 Inkling 추가</span><span class="sxs-lookup"><span data-stu-id="4bda7-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="4bda7-124">Inkling의 Azure AD 통합을 구성하려면 갤러리의 Inkling을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4bda7-125">**갤러리에서 Inkling을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4bda7-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4bda7-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4bda7-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4bda7-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="4bda7-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="4bda7-133">검색 상자에 **Inkling**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-133">In the search box, type **Inkling**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="4bda7-135">결과 창에서 **Inkling**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4bda7-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4bda7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4bda7-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Inkling에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4bda7-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Inkling 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="4bda7-140">즉, Azure AD 사용자와 Inkling의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="4bda7-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Inkling의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="4bda7-142">Inkling에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4bda7-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4bda7-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4bda7-145">**[Inkling 테스트 사용자 만들기](#creating-an-inkling-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Inkling에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4bda7-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4bda7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4bda7-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4bda7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4bda7-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Inkling 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="4bda7-150">**Inkling에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4bda7-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="4bda7-151">Azure 관리 포털의 **Inkling** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성][4]

2. <span data-ttu-id="4bda7-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="4bda7-155">**Inkling 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="4bda7-157">a.</span><span class="sxs-lookup"><span data-stu-id="4bda7-157">a.</span></span> <span data-ttu-id="4bda7-158">**식별자** 텍스트 상자에서 `https://api.inkling.com/saml/v2/metadata/<user-id>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="4bda7-159">b.</span><span class="sxs-lookup"><span data-stu-id="4bda7-159">b.</span></span> <span data-ttu-id="4bda7-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="4bda7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4bda7-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-161">Please note that these are not the real values.</span></span> <span data-ttu-id="4bda7-162">실제 식별자 및 회신 URL로 해당 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4bda7-163">이러한 값을 얻으려면 [Inkling 지원 팀](mailto:press@inkling.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4bda7-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="4bda7-164">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="4bda7-166">**새 인증서 만들기** 대화 상자에서 달력 아이콘을 클릭하고 **만료 날짜**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="4bda7-167">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-167">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="4bda7-169">**SAML 서명 인증서** 섹션에서 **새 인증서 활성화**를 선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="4bda7-171">팝업 **롤오버 인증서** 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="4bda7-173">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="4bda7-175">응용 프로그램에 대해 SSO를 구성하려면 [Inkling 지원 팀](mailto:press@inkling.com)에 문의하고 다운로드한 **메타데이터**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4bda7-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4bda7-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="4bda7-177">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="4bda7-179">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="4bda7-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4bda7-180">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4bda7-182">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4bda7-184">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4bda7-186">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4bda7-188">a.</span><span class="sxs-lookup"><span data-stu-id="4bda7-188">a.</span></span> <span data-ttu-id="4bda7-189">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4bda7-190">b.</span><span class="sxs-lookup"><span data-stu-id="4bda7-190">b.</span></span> <span data-ttu-id="4bda7-191">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4bda7-192">c.</span><span class="sxs-lookup"><span data-stu-id="4bda7-192">c.</span></span> <span data-ttu-id="4bda7-193">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4bda7-194">d.</span><span class="sxs-lookup"><span data-stu-id="4bda7-194">d.</span></span> <span data-ttu-id="4bda7-195">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="4bda7-196">Inkling 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4bda7-196">Creating an Inkling test user</span></span>

<span data-ttu-id="4bda7-197">이 섹션에서는 Inkling에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="4bda7-198">Inkling 플랫폼에서 사용자를 추가하려면 [Inkling 지원 팀](mailto:press@inkling.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4bda7-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4bda7-199">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4bda7-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4bda7-200">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Inkling에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4bda7-202">**Britta Simon을 Inkling에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4bda7-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="4bda7-203">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동한 후 **엔터프라이즈 응용 프로그램**으로 이동하고 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4bda7-205">응용 프로그램 목록에서 **Inkling**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-205">In the applications list, select **Inkling**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="4bda7-207">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-207">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="4bda7-209">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-209">Click **Add** button.</span></span> <span data-ttu-id="4bda7-210">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="4bda7-212">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4bda7-213">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4bda7-214">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="4bda7-215">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4bda7-215">Testing single sign-on</span></span>

<span data-ttu-id="4bda7-216">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4bda7-217">액세스 패널에서 Inkling 타일을 클릭하면 Inkling 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bda7-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4bda7-218">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4bda7-218">Additional resources</span></span>

* [<span data-ttu-id="4bda7-219">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="4bda7-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4bda7-220">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4bda7-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png