---
title: "자습서: MaxxPoint와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 MaxxPoint 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="da932-103">자습서: MaxxPoint와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="da932-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="da932-104">이 자습서에서는 Azure AD(Azure Active Directory)와 MaxxPoint를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="da932-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da932-105">MaxxPoint를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="da932-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="da932-106">MaxxPoint에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="da932-107">사용자가 해당 Azure AD 계정으로 MaxxPoint(Single Sign-on)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da932-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="da932-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da932-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da932-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da932-110">Prerequisites</span></span>

<span data-ttu-id="da932-111">MaxxPoint와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="da932-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="da932-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da932-113">MaxxPoint Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="da932-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da932-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da932-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da932-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="da932-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da932-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="da932-118">Scenario description</span></span>
<span data-ttu-id="da932-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da932-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da932-121">갤러리에서 MaxxPoint 추가</span><span class="sxs-lookup"><span data-stu-id="da932-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="da932-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="da932-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="da932-123">갤러리에서 MaxxPoint 추가</span><span class="sxs-lookup"><span data-stu-id="da932-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="da932-124">MaxxPoint의 Azure AD 통합을 구성하려면 갤러리의 MaxxPoint를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="da932-125">**갤러리에서 MaxxPoint를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da932-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="da932-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da932-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da932-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="da932-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭하여 새 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="da932-133">검색 상자에 **MaxxPoint**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-133">In the search box, type **MaxxPoint**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="da932-135">결과 창에서 **MaxxPoint**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da932-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="da932-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da932-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 MaxxPoint에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da932-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 MaxxPoint 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="da932-140">즉, Azure AD 사용자와 MaxxPoint의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="da932-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 MaxxPoint의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="da932-142">MaxxPoint에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="da932-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="da932-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da932-145">**[MaxxPoint 테스트 사용자 만들기](#creating-a-maxxpoint-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 MaxxPoint에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da932-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="da932-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da932-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da932-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="da932-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da932-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 MaxxPoint 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="da932-150">**MaxxPoint에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da932-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="da932-151">Azure Portal의 **MaxxPoint** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="da932-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="da932-155">**MaxxPoint 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 단계를 수행하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da932-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="da932-157">**MaxxPoint 도메인 및 URL** 섹션에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="da932-159">a.</span><span class="sxs-lookup"><span data-stu-id="da932-159">a.</span></span> <span data-ttu-id="da932-160">**고급 URL 설정 표시** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="da932-161">b.</span><span class="sxs-lookup"><span data-stu-id="da932-161">b.</span></span> <span data-ttu-id="da932-162">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="da932-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="da932-163">Please note that this is not the real value.</span></span> <span data-ttu-id="da932-164">이 값은 실제 로그인 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="da932-165">이 값을 얻으려면 MaxxPoint 팀(**888-728-0950**)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="da932-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="da932-166">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="da932-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="da932-170">응용 프로그램에 대해 SSO를 구성하려면 MaxxPoint 지원 팀(**888-728-0950**)에 문의합니다. 그러면 다운로드한 **메타데이터 XML** 파일을 제공하는 방법에 대한 추가 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="da932-171">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="da932-172">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da932-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="da932-173">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da932-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da932-174">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="da932-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="da932-175">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da932-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="da932-177">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="da932-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="da932-178">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da932-180">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da932-182">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da932-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da932-184">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da932-186">a.</span><span class="sxs-lookup"><span data-stu-id="da932-186">a.</span></span> <span data-ttu-id="da932-187">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da932-188">b.</span><span class="sxs-lookup"><span data-stu-id="da932-188">b.</span></span> <span data-ttu-id="da932-189">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da932-190">c.</span><span class="sxs-lookup"><span data-stu-id="da932-190">c.</span></span> <span data-ttu-id="da932-191">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="da932-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="da932-192">d.</span><span class="sxs-lookup"><span data-stu-id="da932-192">d.</span></span> <span data-ttu-id="da932-193">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="da932-194">MaxxPoint 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="da932-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="da932-195">이 섹션에서는 MaxxPoint에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da932-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="da932-196">MaxxPoint 응용 프로그램에서 사용자를 추가하려면 MaxxPoint 지원 팀(**888-728-0950**)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="da932-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="da932-197">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="da932-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="da932-198">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 MaxxPoint에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![사용자 할당][200] 

<span data-ttu-id="da932-200">**Britta Simon을 MaxxPoint에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="da932-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="da932-201">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="da932-203">응용 프로그램 목록에서 **MaxxPoint**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="da932-205">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-205">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="da932-207">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-207">Click **Add** button.</span></span> <span data-ttu-id="da932-208">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="da932-210">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="da932-211">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da932-212">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da932-213">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="da932-213">Testing single sign-on</span></span>

<span data-ttu-id="da932-214">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="da932-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="da932-215">액세스 패널에서 MaxxPoint 타일을 클릭하면 MaxxPoint 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="da932-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="da932-216">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="da932-216">Additional resources</span></span>

* [<span data-ttu-id="da932-217">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="da932-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da932-218">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="da932-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png