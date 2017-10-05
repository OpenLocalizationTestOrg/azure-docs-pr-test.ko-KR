---
title: "자습서: Teamwork와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Teamwork 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="bd702-103">자습서: Teamwork와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="bd702-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="bd702-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Teamwork를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd702-105">Teamwork와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bd702-106">Teamwork에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="bd702-107">사용자가 해당 Azure AD 계정으로 Teamwork(Single Sign-On)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd702-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="bd702-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd702-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd702-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bd702-110">Prerequisites</span></span>

<span data-ttu-id="bd702-111">Teamwork와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="bd702-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="bd702-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd702-113">Teamwork Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="bd702-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="bd702-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="bd702-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd702-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="bd702-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="bd702-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="bd702-118">Scenario description</span></span>
<span data-ttu-id="bd702-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd702-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd702-121">갤러리에서 Teamwork 추가</span><span class="sxs-lookup"><span data-stu-id="bd702-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="bd702-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bd702-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="bd702-123">갤러리에서 Teamwork 추가</span><span class="sxs-lookup"><span data-stu-id="bd702-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="bd702-124">Azure AD에 Teamwork를 통합하도록 구성하려면 갤러리의 Teamwork를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bd702-125">**갤러리에서 Teamwork를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd702-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bd702-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd702-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bd702-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="bd702-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="bd702-133">검색 상자에 **Teamwork**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-133">In the search box, type **Teamwork**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="bd702-135">결과 창에서 **Teamwork**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd702-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bd702-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd702-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Teamwork에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd702-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Teamwork 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="bd702-140">즉, Azure AD 사용자와 Teamwork의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="bd702-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Teamwork의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="bd702-142">Teamwork에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bd702-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bd702-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-on 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd702-145">**[Teamwork 테스트 사용자 만들기](#creating-a-teamwork-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Teamwork에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="bd702-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd702-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd702-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="bd702-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd702-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Teamwork 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="bd702-150">**Teamwork에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd702-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="bd702-151">Azure 관리 포털의 **Teamwork** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="bd702-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="bd702-155">**Teamwork 도메인 및 URL** 섹션에서 **로그인 URL** 텍스트 상자에 다음 패턴을 사용하여 URL을 입력합니다.`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="bd702-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="bd702-157">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-157">Please note that this is not the real value.</span></span> <span data-ttu-id="bd702-158">이 값은 실제 로그인 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="bd702-159">이 값을 가져오려면 [Teamwork 지원 팀](mailto:support@teamwork.com)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="bd702-160">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="bd702-162">**새 인증서 만들기** 대화 상자에서 달력 아이콘을 클릭하고 **만료 날짜**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="bd702-163">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-163">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="bd702-165">**SAML 서명 인증서** 섹션에서 **새 인증서 활성화**를 선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="bd702-167">팝업 **롤오버 인증서** 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bd702-169">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="bd702-171">응용 프로그램에 대해 SSO를 구성하려면 [Teamwork 지원 팀](mailto:support@teamwork.com)에 문의하고 다운로드한 **메타데이터**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd702-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bd702-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd702-173">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="bd702-175">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="bd702-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bd702-176">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd702-178">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd702-180">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd702-182">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd702-184">a.</span><span class="sxs-lookup"><span data-stu-id="bd702-184">a.</span></span> <span data-ttu-id="bd702-185">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd702-186">b.</span><span class="sxs-lookup"><span data-stu-id="bd702-186">b.</span></span> <span data-ttu-id="bd702-187">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd702-188">c.</span><span class="sxs-lookup"><span data-stu-id="bd702-188">c.</span></span> <span data-ttu-id="bd702-189">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bd702-190">d.</span><span class="sxs-lookup"><span data-stu-id="bd702-190">d.</span></span> <span data-ttu-id="bd702-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="bd702-192">Teamwork 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bd702-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="bd702-193">이 섹션에서는 Teamwork에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="bd702-194">[Teamwork 지원 팀](mailto:support@teamwork.com)에 문의하여 Teamwork 플랫폼에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="bd702-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bd702-195">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="bd702-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bd702-196">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Teamwork에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![사용자 할당][200] 

<span data-ttu-id="bd702-198">**Britta Simon을 Teamwork에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd702-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="bd702-199">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="bd702-201">응용 프로그램 목록에서 **Teamwork**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-201">In the applications list, select **Teamwork**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="bd702-203">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-203">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="bd702-205">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-205">Click **Add** button.</span></span> <span data-ttu-id="bd702-206">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="bd702-208">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bd702-209">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd702-210">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="bd702-211">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="bd702-211">Testing single sign-on</span></span>

<span data-ttu-id="bd702-212">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bd702-213">액세스 패널에서 Teamwork 타일을 클릭하면 Teamwork 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd702-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bd702-214">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bd702-214">Additional resources</span></span>

* [<span data-ttu-id="bd702-215">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="bd702-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd702-216">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bd702-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png