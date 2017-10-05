---
title: "자습서: Datahug와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 Datahug 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="9a903-103">자습서: Datahug와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9a903-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="9a903-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Datahug를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a903-105">Datahug를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a903-106">Datahug에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="9a903-107">사용자가 해당 Azure AD 계정으로 Datahug에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a903-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a903-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="9a903-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9a903-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a903-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a903-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a903-111">Prerequisites</span></span>

<span data-ttu-id="9a903-112">Datahug와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="9a903-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9a903-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9a903-114">Datahug Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9a903-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a903-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a903-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a903-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9a903-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a903-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a903-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9a903-119">Scenario description</span></span>
<span data-ttu-id="9a903-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a903-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a903-122">갤러리에서 Datahug 추가</span><span class="sxs-lookup"><span data-stu-id="9a903-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="9a903-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9a903-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="9a903-124">갤러리에서 Datahug 추가</span><span class="sxs-lookup"><span data-stu-id="9a903-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="9a903-125">Datahug의 Azure AD 통합을 구성하려면 갤러리의 Datahug를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a903-126">**갤러리에서 Datahug를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a903-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a903-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a903-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a903-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-130">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="9a903-132">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="9a903-134">검색 상자에 **Datahug**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-134">In the search box, type **Datahug**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="9a903-136">결과 패널에서 **Datahug**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a903-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9a903-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a903-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Datahug에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9a903-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Datahug 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="9a903-141">즉, Azure AD 사용자와 Datahug의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="9a903-142">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Datahug의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="9a903-143">Datahug에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a903-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a903-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a903-146">**[Datahug 테스트 사용자 만들기](#creating-a-datahug-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Datahug에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a903-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a903-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a903-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9a903-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a903-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Datahug 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="9a903-151">**Datahug에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a903-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="9a903-152">Azure Portal의 **Datahug** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="9a903-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="9a903-156">**Datahug 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="9a903-158">a.</span><span class="sxs-lookup"><span data-stu-id="9a903-158">a.</span></span> <span data-ttu-id="9a903-159">**식별자** 텍스트 상자에서 `https://apps.datahug.com/identity/<uniqueID>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="9a903-160">b.</span><span class="sxs-lookup"><span data-stu-id="9a903-160">b.</span></span> <span data-ttu-id="9a903-161">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="9a903-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="9a903-162">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9a903-163">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="9a903-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="9a903-165">**로그온 URL** 텍스트 상자에 URL을 입력합니다. `https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="9a903-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9a903-166">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-166">These values are not the real.</span></span> <span data-ttu-id="9a903-167">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9a903-168">식별자 및 회신 URL에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="9a903-169">이러한 값을 얻으려면 [Datahug 클라이언트 지원 팀](http://datahug.com/about/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9a903-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="9a903-170">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="9a903-172">**“고급 인증서 서명 설정 표시”**를 선택하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="9a903-174">a.</span><span class="sxs-lookup"><span data-stu-id="9a903-174">a.</span></span> <span data-ttu-id="9a903-175">**서명 옵션**에서 **SAML 어설션 서명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="9a903-176">b.</span><span class="sxs-lookup"><span data-stu-id="9a903-176">b.</span></span> <span data-ttu-id="9a903-177">**서명 알고리즘**에서 **SHA1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="9a903-178">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-178">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="9a903-180">**Datahug 구성** 섹션에서 **Datahug 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9a903-181">**빠른 참조 섹션**에서 **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="9a903-183">**Datahug** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**, **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 [Datahug 지원](http://datahug.com/about/contact-us/)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="9a903-184">그러면 이 응용 프로그램에서 SAML SSO 연결이 양쪽에 제대로 설정되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9a903-185">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a903-186">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a903-187">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a903-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9a903-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a903-189">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="9a903-191">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="9a903-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a903-192">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a903-194">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a903-196">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a903-198">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a903-200">a.</span><span class="sxs-lookup"><span data-stu-id="9a903-200">a.</span></span> <span data-ttu-id="9a903-201">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a903-202">b.</span><span class="sxs-lookup"><span data-stu-id="9a903-202">b.</span></span> <span data-ttu-id="9a903-203">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a903-204">c.</span><span class="sxs-lookup"><span data-stu-id="9a903-204">c.</span></span> <span data-ttu-id="9a903-205">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a903-206">d.</span><span class="sxs-lookup"><span data-stu-id="9a903-206">d.</span></span> <span data-ttu-id="9a903-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="9a903-208">Datahug 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9a903-208">Creating a Datahug test user</span></span>

<span data-ttu-id="9a903-209">Azure AD 사용자가 Datahug에 로그인할 수 있도록 하려면 Datahug로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="9a903-210">Datahug의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="9a903-211">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a903-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9a903-212">Datahug 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="9a903-213">오른쪽 위 모퉁이에 있는 **cog** 위로 마우스를 가져가고 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![직원 추가](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="9a903-215">**피플**을 선택하고 **사용자 추가** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-215">Choose **People** and click the **Add Users** tab</span></span>

    ![직원 추가](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="9a903-217">계정을 만들 사용자의 메일을 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![직원 추가](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="9a903-219">**환영 메일 보내기** 확인란을 선택하여 사용자에게 등록 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="9a903-220">Salesforce에 대한 계정을 만들 경우 환영 메일을 보내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9a903-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9a903-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="9a903-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9a903-222">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Datahug에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![사용자 할당][200] 

<span data-ttu-id="9a903-224">**Britta Simon을 Datahug에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a903-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="9a903-225">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9a903-227">응용 프로그램 목록에서 **Datahug**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-227">In the applications list, select **Datahug**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="9a903-229">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-229">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="9a903-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-231">Click **Add** button.</span></span> <span data-ttu-id="9a903-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="9a903-234">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a903-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a903-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a903-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9a903-237">Testing single sign-on</span></span>

<span data-ttu-id="9a903-238">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="9a903-239">액세스 패널에서 Datahug 타일을 클릭하면 Datahug 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a903-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="9a903-240">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a903-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a903-241">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9a903-241">Additional resources</span></span>

* [<span data-ttu-id="9a903-242">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="9a903-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a903-243">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9a903-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

