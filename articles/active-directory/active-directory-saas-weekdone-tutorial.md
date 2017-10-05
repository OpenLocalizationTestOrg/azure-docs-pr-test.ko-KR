---
title: "자습서: Weekdone과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Weekdone 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="9fe6f-103">자습서: Weekdone과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9fe6f-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="9fe6f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Weekdone을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fe6f-105">Weekdone을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9fe6f-106">Weekdone에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="9fe6f-107">사용자가 해당 Azure AD 계정으로 Weekdone에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fe6f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9fe6f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fe6f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9fe6f-110">Prerequisites</span></span>

<span data-ttu-id="9fe6f-111">Weekdone과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="9fe6f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9fe6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9fe6f-113">Weekdone Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9fe6f-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fe6f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fe6f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fe6f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fe6f-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fe6f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9fe6f-118">Scenario description</span></span>
<span data-ttu-id="9fe6f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fe6f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fe6f-121">갤러리에서 Weekdone 추가</span><span class="sxs-lookup"><span data-stu-id="9fe6f-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="9fe6f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9fe6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="9fe6f-123">갤러리에서 Weekdone 추가</span><span class="sxs-lookup"><span data-stu-id="9fe6f-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="9fe6f-124">Weekdone의 Azure AD 통합을 구성하려면 갤러리의 Weekdone을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9fe6f-125">**갤러리에서 Weekdone을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9fe6f-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe6f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9fe6f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9fe6f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="9fe6f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="9fe6f-133">검색 상자에 **Weekdone**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-133">In the search box, type **Weekdone**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="9fe6f-135">결과 창에서 **Weekdone**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fe6f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9fe6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fe6f-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Weekdone에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9fe6f-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Weekdone 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="9fe6f-140">즉, Azure AD 사용자와 Weekdone의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="9fe6f-141">Weekdone에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9fe6f-142">Weekdone에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9fe6f-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9fe6f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fe6f-145">**[Weekdone 테스트 사용자 만들기](#creating-a-weekdone-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Weekdone에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fe6f-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fe6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fe6f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9fe6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fe6f-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Weekdone 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="9fe6f-150">**Weekdone에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9fe6f-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe6f-151">Azure Portal의 **Weekdone** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="9fe6f-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="9fe6f-155">**Weekdone 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="9fe6f-157">a.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-157">a.</span></span> <span data-ttu-id="9fe6f-158">**식별자** 텍스트 상자에서 `https://weekdone.com/a/<tenantname>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="9fe6f-159">b.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-159">b.</span></span> <span data-ttu-id="9fe6f-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="9fe6f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="9fe6f-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9fe6f-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="9fe6f-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="9fe6f-164">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="9fe6f-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9fe6f-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-165">These values are not real.</span></span> <span data-ttu-id="9fe6f-166">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9fe6f-167">이러한 값을 얻으려면 [Weekdone 클라이언트 지원 팀](mailto:hello@weekdone.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="9fe6f-168">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="9fe6f-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9fe6f-172">**Weekdone 구성** 섹션에서 **Weekdone 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9fe6f-173">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="9fe6f-175">**Weekdone** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML, 로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 [Weekdone 지원 팀](mailto:hello@weekdone.com)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="9fe6f-176">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9fe6f-177">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9fe6f-178">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fe6f-179">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9fe6f-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="9fe6f-180">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="9fe6f-182">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="9fe6f-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe6f-183">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fe6f-185">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fe6f-187">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fe6f-189">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fe6f-191">a.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-191">a.</span></span> <span data-ttu-id="9fe6f-192">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fe6f-193">b.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-193">b.</span></span> <span data-ttu-id="9fe6f-194">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fe6f-195">c.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-195">c.</span></span> <span data-ttu-id="9fe6f-196">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9fe6f-197">d.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-197">d.</span></span> <span data-ttu-id="9fe6f-198">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="9fe6f-199">Weekdone 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9fe6f-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="9fe6f-200">이 섹션은 Weekdone에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="9fe6f-201">Weekdone은 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9fe6f-202">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-202">There is no action item for you in this section.</span></span> <span data-ttu-id="9fe6f-203">새 사용자가 아직 존재하지 않는 경우 Weekdone에 액세스를 시도하는 동안 만들어 집니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="9fe6f-204">사용자를 수동으로 생성해야 하는 경우 [Weekdone 클라이언트 지원 팀](mailto:hello@weekdone.com)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9fe6f-205">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="9fe6f-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9fe6f-206">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Weekdone에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![사용자 할당][200] 

<span data-ttu-id="9fe6f-208">**Britta Simon을 Weekdone에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="9fe6f-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="9fe6f-209">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9fe6f-211">응용 프로그램 목록에서 **Weekdone**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-211">In the applications list, select **Weekdone**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="9fe6f-213">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-213">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="9fe6f-215">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-215">Click **Add** button.</span></span> <span data-ttu-id="9fe6f-216">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="9fe6f-218">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9fe6f-219">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fe6f-220">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fe6f-221">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9fe6f-221">Testing single sign-on</span></span>

<span data-ttu-id="9fe6f-222">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9fe6f-223">액세스 패널에서 Weekdone 타일을 클릭하면 Weekdone 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe6f-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fe6f-224">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9fe6f-224">Additional resources</span></span>

* [<span data-ttu-id="9fe6f-225">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="9fe6f-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fe6f-226">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9fe6f-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

