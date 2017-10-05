---
title: "자습서: Directions on Microsoft과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Directions on Microsoft 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="38984-103">자습서: Directions on Microsoft과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="38984-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="38984-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Directions on Microsoft를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="38984-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38984-105">Directions on Microsoft를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="38984-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38984-106">Directions on Microsoft에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="38984-107">사용자가 해당 Azure AD 계정으로 Directions on Microsoft에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38984-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38984-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38984-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38984-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="38984-110">Prerequisites</span></span>

<span data-ttu-id="38984-111">Directions on Microsoft와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="38984-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="38984-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38984-113">Directions on Microsoft에서 Single Sign-On이 활성화된 구독</span><span class="sxs-lookup"><span data-stu-id="38984-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38984-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38984-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38984-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="38984-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38984-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38984-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="38984-118">Scenario description</span></span>
<span data-ttu-id="38984-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38984-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38984-121">갤러리에서 Directions on Microsoft 추가</span><span class="sxs-lookup"><span data-stu-id="38984-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="38984-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="38984-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="38984-123">갤러리에서 Directions on Microsoft 추가</span><span class="sxs-lookup"><span data-stu-id="38984-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="38984-124">Azure AD에 Directions on Microsoft를 통합하도록 구성하려면 갤러리의 Directions on Microsoft를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38984-125">**갤러리에서 Directions on Microsoft를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="38984-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38984-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38984-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38984-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="38984-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="38984-133">검색 상자에 **Directions on Microsoft**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="38984-135">결과 패널에서 **Directions on Microsoft**를 입력하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38984-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="38984-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38984-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Directions on Microsoft에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="38984-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD의 사용자에 해당하는 Directions on Microsoft의 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="38984-140">즉, Azure AD 사용자와 Directions on Microsoft의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="38984-141">Directions on Microsoft에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38984-142">Directions on Microsoft에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38984-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38984-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38984-145">**[Directions on Microsoft 테스트 사용자 만들기](#creating-a-directions-on-microsoft-test-user)** - Britta Simon의 Azure AD 사용자 표현과 연결되는 대응 사용자를 Directions on Microsoft에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38984-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38984-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38984-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38984-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="38984-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38984-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Directions on Microsoft 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="38984-150">**Directions on Microsoft에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="38984-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="38984-151">Azure Portal의 **Directions on Microsoft** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="38984-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="38984-155">**Directions on Microsoft 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="38984-157">a.</span><span class="sxs-lookup"><span data-stu-id="38984-157">a.</span></span> <span data-ttu-id="38984-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="38984-159">b.</span><span class="sxs-lookup"><span data-stu-id="38984-159">b.</span></span> <span data-ttu-id="38984-160">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="38984-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="38984-161">These values are not real.</span></span> <span data-ttu-id="38984-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="38984-163">이러한 값을 얻으려면 [Directions on Microsoft 클라이언트 지원 팀](mailto:service@DirectionsOnMicrosoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="38984-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="38984-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="38984-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38984-168">**Directions on Microsoft** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Directions on Microsoft 지원 팀](mailto:service@DirectionsOnMicrosoft.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="38984-169">페더레이션된 사이트 멤버 자격을 찾기 위해 Directions on Microsoft 지원팀을 활성화하려면 전자 메일에 회사 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="38984-170">Directions on Microsoft에 Single Sign-On은 [Directions on Microsoft 클라이언트 지원 팀](mailto:service@DirectionsOnMicrosoft.com)에서 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="38984-171">Single sign-on가 활성화되면 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="38984-172">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38984-173">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38984-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38984-174">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38984-175">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="38984-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="38984-176">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="38984-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="38984-178">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="38984-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38984-179">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38984-181">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38984-183">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38984-185">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38984-187">a.</span><span class="sxs-lookup"><span data-stu-id="38984-187">a.</span></span> <span data-ttu-id="38984-188">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38984-189">b.</span><span class="sxs-lookup"><span data-stu-id="38984-189">b.</span></span> <span data-ttu-id="38984-190">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38984-191">c.</span><span class="sxs-lookup"><span data-stu-id="38984-191">c.</span></span> <span data-ttu-id="38984-192">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="38984-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38984-193">d.</span><span class="sxs-lookup"><span data-stu-id="38984-193">d.</span></span> <span data-ttu-id="38984-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="38984-195">Directions on Microsoft 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="38984-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="38984-196">Directions on Microsoft을 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38984-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="38984-197">할당된 사용자가 액세스 패널을 사용하여 Directions on Microsoft에 로그인하려는 경우 Directions on Microsoft는 사용자가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="38984-198">사용할 수 있는 사용자 계정이 없으면 자동으로 Directions on Microsoft에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="38984-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38984-199">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="38984-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38984-200">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Directions on Microsoft에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![사용자 할당][200] 

<span data-ttu-id="38984-202">**Britta Simon을 Directions on Microsoft에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="38984-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="38984-203">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="38984-205">응용 프로그램 목록에서 **Directions on Microsoft**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="38984-207">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-207">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="38984-209">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-209">Click **Add** button.</span></span> <span data-ttu-id="38984-210">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="38984-212">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38984-213">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38984-214">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38984-215">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="38984-215">Testing single sign-on</span></span>

<span data-ttu-id="38984-216">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="38984-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="38984-217">액세스 패널에서 Directions on Microsoft 타일을 클릭하면 Directions on Microsoft 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="38984-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="38984-218">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38984-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="38984-219">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="38984-219">Additional resources</span></span>

* [<span data-ttu-id="38984-220">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="38984-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38984-221">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="38984-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

