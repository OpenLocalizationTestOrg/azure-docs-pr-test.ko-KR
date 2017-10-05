---
title: "자습서: BeeLine과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 BeeLine 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="5976a-103">자습서: Beeline과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5976a-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="5976a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 BeeLine을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5976a-105">BeeLine을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5976a-106">BeeLine에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="5976a-107">사용자가 해당 Azure AD 계정으로 BeeLine에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5976a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5976a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5976a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5976a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5976a-110">Prerequisites</span></span>

<span data-ttu-id="5976a-111">BeeLine과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="5976a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5976a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5976a-113">BeeLine Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5976a-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5976a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5976a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5976a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5976a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5976a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5976a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5976a-118">Scenario description</span></span>
<span data-ttu-id="5976a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5976a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5976a-121">갤러리에서 BeeLine 추가</span><span class="sxs-lookup"><span data-stu-id="5976a-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="5976a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5976a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="5976a-123">갤러리에서 BeeLine 추가</span><span class="sxs-lookup"><span data-stu-id="5976a-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="5976a-124">BeeLine의 Azure AD 통합을 구성하려면 갤러리의 BeeLine을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5976a-125">**갤러리에서 BeeLine을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5976a-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5976a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5976a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5976a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5976a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5976a-133">검색 상자에 **BeeLine**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-133">In the search box, type **BeeLine**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="5976a-135">결과 패널에서 **BeeLine**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5976a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5976a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5976a-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 BeeLine에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5976a-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 BeeLine 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="5976a-140">즉, Azure AD 사용자와 BeeLine의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="5976a-141">BeeLine에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5976a-142">BeeLine에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5976a-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5976a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5976a-145">**[BeeLine 테스트 사용자 만들기](#creating-a-beeline-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 BeeLine에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5976a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5976a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5976a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5976a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5976a-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 BeeLine 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="5976a-150">**BeeLine에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5976a-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="5976a-151">Azure Portal의 **BeeLine** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5976a-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="5976a-155">**BeeLine 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="5976a-157">a.</span><span class="sxs-lookup"><span data-stu-id="5976a-157">a.</span></span> <span data-ttu-id="5976a-158">**식별자** 텍스트 상자에서 `https://projects.beeline.net/<instancename>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="5976a-159">b.</span><span class="sxs-lookup"><span data-stu-id="5976a-159">b.</span></span> <span data-ttu-id="5976a-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="5976a-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-161">These values are not real.</span></span> <span data-ttu-id="5976a-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5976a-163">이러한 값을 얻으려면 [BeeLine 지원 팀](https://www.beeline.com/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5976a-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="5976a-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="5976a-166">Beeline 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5976a-167">응용 프로그램에 매핑되는 올바른 사용자 ID를 식별하려면 [BeeLine 지원 팀](https://www.beeline.com/contact-us/)에 먼저 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5976a-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="5976a-168">또한 이 매핑에 사용하려는 특성에 대한 [BeeLine 지원 팀](https://www.beeline.com/contact-us/)의 지침을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="5976a-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="5976a-169">응용 프로그램의 **사용자 특성** 탭에서 이 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="5976a-170">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="5976a-171">여기서는 고유한 사용자 ID를 제공하는 **userprincipalname** 특성으로 **사용자 ID** 클레임을 매핑했으며, 성공적인 모든 SAML 응답에서 BeeLine 응용 프로그램으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="5976a-173">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-173">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5976a-175">**BeeLine 구성** 섹션에서 **BeeLine 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5976a-176">**빠른 참조 섹션**에서 **로그아웃 URL** 및 **SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="5976a-178">**BeeLine** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**, **SAML 엔터티 ID** 및 **로그아웃 URL**을 [BeeLine 지원 팀](https://www.beeline.com/contact-us/)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="5976a-179">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5976a-180">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5976a-181">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5976a-182">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5976a-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="5976a-183">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5976a-185">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5976a-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5976a-186">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5976a-188">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5976a-190">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5976a-192">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5976a-194">a.</span><span class="sxs-lookup"><span data-stu-id="5976a-194">a.</span></span> <span data-ttu-id="5976a-195">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5976a-196">b.</span><span class="sxs-lookup"><span data-stu-id="5976a-196">b.</span></span> <span data-ttu-id="5976a-197">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5976a-198">c.</span><span class="sxs-lookup"><span data-stu-id="5976a-198">c.</span></span> <span data-ttu-id="5976a-199">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5976a-200">d.</span><span class="sxs-lookup"><span data-stu-id="5976a-200">d.</span></span> <span data-ttu-id="5976a-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="5976a-202">BeeLine 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5976a-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="5976a-203">이 섹션에서는 Beeline에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="5976a-204">Beeline 응용 프로그램에서는 Single Sign On을 수행하기 전에 모든 사용자를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="5976a-205">따라서 모든 사용자를 응용 프로그램에 프로비전하려면 [BeeLine 지원 팀](https://www.beeline.com/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5976a-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5976a-206">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5976a-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5976a-207">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 BeeLine에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5976a-209">**Britta Simon을 BeeLine에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5976a-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="5976a-210">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5976a-212">응용 프로그램 목록에서 **BeeLine**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-212">In the applications list, select **BeeLine**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="5976a-214">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-214">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5976a-216">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-216">Click **Add** button.</span></span> <span data-ttu-id="5976a-217">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5976a-219">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5976a-220">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5976a-221">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5976a-222">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5976a-222">Testing single sign-on</span></span>

<span data-ttu-id="5976a-223">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="5976a-224">액세스 패널에서 Beeline 타일을 클릭하면 Beeline 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5976a-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5976a-225">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5976a-225">Additional resources</span></span>

* [<span data-ttu-id="5976a-226">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5976a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5976a-227">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5976a-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

