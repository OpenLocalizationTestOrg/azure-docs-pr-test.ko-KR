---
title: "자습서: LearnUpon과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 LearnUpon 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="338d4-103">자습서: LearnUpon과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="338d4-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="338d4-104">이 자습서에서는 Azure AD(Azure Active Directory)와 LearnUpon을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="338d4-105">LearnUpon을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="338d4-106">LearnUpon에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="338d4-107">사용자가 해당 Azure AD 계정으로 LearnUpon에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="338d4-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="338d4-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="338d4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="338d4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="338d4-110">Prerequisites</span></span>

<span data-ttu-id="338d4-111">LearnUpon과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="338d4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="338d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="338d4-113">LearnUpon Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="338d4-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="338d4-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="338d4-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="338d4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="338d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="338d4-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="338d4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="338d4-118">Scenario description</span></span>
<span data-ttu-id="338d4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="338d4-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="338d4-121">갤러리에서 LearnUpon 추가</span><span class="sxs-lookup"><span data-stu-id="338d4-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="338d4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="338d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="338d4-123">갤러리에서 LearnUpon 추가</span><span class="sxs-lookup"><span data-stu-id="338d4-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="338d4-124">LearnUpon의 Azure AD 통합을 구성하려면 갤러리의 LearnUpon을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="338d4-125">**갤러리에서 LearnUpon을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="338d4-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="338d4-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="338d4-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="338d4-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="338d4-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="338d4-133">검색 상자에 **LearnUpon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-133">In the search box, type **LearnUpon**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="338d4-135">결과 패널에서 **LearnUpon**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="338d4-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="338d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="338d4-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 LearnUpon에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="338d4-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 LearnUpon 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="338d4-140">즉, Azure AD 사용자와 LearnUpon의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="338d4-141">LearnUpon에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="338d4-142">LearnUpon에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="338d4-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="338d4-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="338d4-145">**[LearnUpon 테스트 사용자 만들기](#creating-a-learnupon-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 LearnUpon에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="338d4-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="338d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="338d4-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="338d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="338d4-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LearnUpon 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="338d4-150">**LearnUpon에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="338d4-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="338d4-151">Azure Portal의 **LearnUpon** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="338d4-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="338d4-155">**LearnUpon 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="338d4-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="338d4-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="338d4-158">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-158">Please note that this is not the real value.</span></span> <span data-ttu-id="338d4-159">이 값은 실제 회신 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="338d4-160">이 값을 얻으려면 [LearnUpon 지원 팀](https://www.learnupon.com/features/support/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="338d4-161">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="338d4-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="338d4-165">**LearnUpon 구성** 섹션에서 **LearnUpon 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="338d4-166">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="338d4-168">다른 브라우저 인스턴스를 열고 관리자 계정으로 LearnUpon에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="338d4-169">**설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-169">Click the **settings** tab.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="338d4-171">**Single Sign On-SAML**을 클릭한 다음 **일반 설정**을 클릭하여 SAML 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="338d4-173">**일반 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="338d4-175">a.</span><span class="sxs-lookup"><span data-stu-id="338d4-175">a.</span></span> <span data-ttu-id="338d4-176">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-176">Select **Enabled**.</span></span>

    <span data-ttu-id="338d4-177">b.</span><span class="sxs-lookup"><span data-stu-id="338d4-177">b.</span></span> <span data-ttu-id="338d4-178">**버전**을 **2.0**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="338d4-179">c.</span><span class="sxs-lookup"><span data-stu-id="338d4-179">c.</span></span> <span data-ttu-id="338d4-180">**건너뛰기 조건**으로 **아니오**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="338d4-181">d.</span><span class="sxs-lookup"><span data-stu-id="338d4-181">d.</span></span> <span data-ttu-id="338d4-182">**SAML 토큰 게시 매개 변수 이름** 텍스트 상자에서 확인하고 인증할 SAML 어설션을 포함하는 위에 표시된 SAML 소비자 URL에 대한 요청 게시 매개 변수의 이름을 입력합니다. 예를 들어 **SAMLResponse**입니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="338d4-183">e.</span><span class="sxs-lookup"><span data-stu-id="338d4-183">e.</span></span> <span data-ttu-id="338d4-184">**이름 식별자 형식** 텍스트 상자에서 사용자 식별자(메일 주소)(예: **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**)가 있는 SAML 어설션의 위치를 나타내는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="338d4-185">f.</span><span class="sxs-lookup"><span data-stu-id="338d4-185">f.</span></span> <span data-ttu-id="338d4-186">**ID 공급자 위치** 텍스트 상자에서 Azure Portal 로그인 화면에서 업로드된 아이콘을 클릭할 경우 사용자가 전송되는 위치를 나타내는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="338d4-187">g.</span><span class="sxs-lookup"><span data-stu-id="338d4-187">g.</span></span> <span data-ttu-id="338d4-188">Azure Portal에서 복사한 **로그아웃 URL**을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="338d4-189">h.</span><span class="sxs-lookup"><span data-stu-id="338d4-189">h.</span></span> <span data-ttu-id="338d4-190">**지문 관리**를 클릭한 다음 다운로드한 인증서의 지문을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="338d4-191">**사용자 설정**을 클릭한 후 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Single Sign-On 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="338d4-193">a.</span><span class="sxs-lookup"><span data-stu-id="338d4-193">a.</span></span> <span data-ttu-id="338d4-194">**이름 식별자 형식** 텍스트 상자에서 사용자 이름(예: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**)이 있는 SAML 어설션의 위치를 알려주는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="338d4-195">b.</span><span class="sxs-lookup"><span data-stu-id="338d4-195">b.</span></span> <span data-ttu-id="338d4-196">**성 식별자 형식** 텍스트 상자에서 사용자 이름(예: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**)이 있는 SAML 어설션의 위치를 알려주는 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="338d4-197">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="338d4-198">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="338d4-199">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="338d4-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="338d4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="338d4-201">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="338d4-203">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="338d4-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="338d4-204">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="338d4-206">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="338d4-208">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="338d4-210">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="338d4-212">a.</span><span class="sxs-lookup"><span data-stu-id="338d4-212">a.</span></span> <span data-ttu-id="338d4-213">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="338d4-214">b.</span><span class="sxs-lookup"><span data-stu-id="338d4-214">b.</span></span> <span data-ttu-id="338d4-215">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="338d4-216">c.</span><span class="sxs-lookup"><span data-stu-id="338d4-216">c.</span></span> <span data-ttu-id="338d4-217">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="338d4-218">d.</span><span class="sxs-lookup"><span data-stu-id="338d4-218">d.</span></span> <span data-ttu-id="338d4-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="338d4-220">LearnUpon 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="338d4-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="338d4-221">이 섹션은 LearnUpon에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="338d4-222">LearnUpon은 Just-In-Time 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="338d4-223">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-223">There is no action item for you in this section.</span></span> <span data-ttu-id="338d4-224">새 사용자가 아직 존재하지 않는 경우 LearnUpon에 액세스하는 동안 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="338d4-225">[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="338d4-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="338d4-226">사용자를 수동으로 만들어야 하는 경우 [LearnUpon 지원 팀](https://www.learnupon.com/features/support/)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="338d4-227">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="338d4-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="338d4-228">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LearnUpon에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![사용자 할당][200] 

<span data-ttu-id="338d4-230">**Britta Simon을 LearnUpon에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="338d4-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="338d4-231">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="338d4-233">응용 프로그램 목록에서 **LearnUpon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-233">In the applications list, select **LearnUpon**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="338d4-235">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-235">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="338d4-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-237">Click **Add** button.</span></span> <span data-ttu-id="338d4-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="338d4-240">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="338d4-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="338d4-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="338d4-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="338d4-243">Testing single sign-on</span></span>

<span data-ttu-id="338d4-244">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="338d4-245">액세스 패널에서 LearnUpon 타일을 클릭하면 LearnUpon 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="338d4-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="338d4-246">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="338d4-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="338d4-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="338d4-247">Additional resources</span></span>

* [<span data-ttu-id="338d4-248">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="338d4-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="338d4-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="338d4-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

