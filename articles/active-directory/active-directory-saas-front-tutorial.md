---
title: "자습서: Front와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Front 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="d9cf2-103">자습서: Front와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d9cf2-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="d9cf2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Front를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9cf2-105">Front를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9cf2-106">Front에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="d9cf2-107">사용자가 해당 Azure AD 계정으로 Front에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d9cf2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d9cf2-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9cf2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d9cf2-110">Prerequisites</span></span>

<span data-ttu-id="d9cf2-111">Front와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="d9cf2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d9cf2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9cf2-113">Front Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d9cf2-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9cf2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9cf2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9cf2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9cf2-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9cf2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d9cf2-118">Scenario description</span></span>
<span data-ttu-id="d9cf2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9cf2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9cf2-121">갤러리에서 Front 추가</span><span class="sxs-lookup"><span data-stu-id="d9cf2-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="d9cf2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d9cf2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="d9cf2-123">갤러리에서 Front 추가</span><span class="sxs-lookup"><span data-stu-id="d9cf2-123">Adding Front from the gallery</span></span>
<span data-ttu-id="d9cf2-124">Front의 Azure AD 통합을 구성하려면 갤러리의 Front를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9cf2-125">**갤러리에서 Front를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d9cf2-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9cf2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="d9cf2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9cf2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="d9cf2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="d9cf2-133">검색 상자에 **Front**를 입력하고 결과 패널에서 **Front**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Front](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d9cf2-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d9cf2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d9cf2-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Front에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d9cf2-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Front 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="d9cf2-138">즉, Azure AD 사용자와 Front의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="d9cf2-139">Front에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d9cf2-140">Front에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9cf2-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9cf2-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9cf2-143">**[Front 테스트 사용자 만들기](#create-a-front-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Front에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9cf2-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9cf2-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d9cf2-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d9cf2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d9cf2-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Front 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="d9cf2-148">**Front에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d9cf2-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="d9cf2-149">Azure Portal의 **Front** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="d9cf2-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="d9cf2-153">**Front 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="d9cf2-155">a.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-155">a.</span></span> <span data-ttu-id="d9cf2-156">**식별자** 텍스트 상자에서 `https://<companyname>.frontapp.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="d9cf2-157">b.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-157">b.</span></span> <span data-ttu-id="d9cf2-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="d9cf2-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="d9cf2-159">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="d9cf2-161">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="d9cf2-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d9cf2-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-162">These values are not real.</span></span> <span data-ttu-id="d9cf2-163">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다. 이러한 값은 자습서의 뒷부분에 나오거나 [Front 클라이언트 지원 팀](mailto:support@frontapp.com)에 문의하여 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="d9cf2-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="d9cf2-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d9cf2-168">**Front 구성** 섹션에서 **Front 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d9cf2-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="d9cf2-171">Front 테넌트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="d9cf2-172">**설정(왼쪽 세로 막대 아래에 있는 톱니바퀴 아이콘) > 기본 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="d9cf2-174">**Single Sign On** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-174">Click **Single Sign On** link.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="d9cf2-176">**Single Sign-On** 드롭다운 목록에서 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="d9cf2-178">**진입점** 텍스트 상자에서 Azure AD 응용 프로그램 구성 마법사에서 나온 **Single Sign-On Service URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="d9cf2-180">다운로드한 **인증서(Base64)** 파일을 메모장에서 열고 내용을 클립보드에 복사한 다음 **서명 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="d9cf2-182">**서비스 공급자 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="d9cf2-184">a.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-184">a.</span></span> <span data-ttu-id="d9cf2-185">**엔터티 ID** 값을 복사하고 Azure Portal의 **Front 도메인 및 URL** 섹션에 있는 **식별자** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="d9cf2-186">b.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-186">b.</span></span> <span data-ttu-id="d9cf2-187">**ACS URL** 값을 복사하고 Azure Portal의 **Front 도메인 및 URL** 섹션에 있는 **로그온 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="d9cf2-188">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="d9cf2-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9cf2-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9cf2-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d9cf2-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d9cf2-192">Create an Azure AD test user</span></span>

<span data-ttu-id="d9cf2-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="d9cf2-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d9cf2-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9cf2-196">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d9cf2-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d9cf2-200">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d9cf2-202">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-202">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d9cf2-204">a.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-204">a.</span></span> <span data-ttu-id="d9cf2-205">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9cf2-206">b.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-206">b.</span></span> <span data-ttu-id="d9cf2-207">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d9cf2-208">c.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-208">c.</span></span> <span data-ttu-id="d9cf2-209">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d9cf2-210">d.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-210">d.</span></span> <span data-ttu-id="d9cf2-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="d9cf2-212">Front 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d9cf2-212">Create a Front test user</span></span>

<span data-ttu-id="d9cf2-213">이 섹션에서는 Front에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="d9cf2-214">Front 플랫폼에서 사용자를 추가하려면 [Front 클라이언트 지원 팀](mailto:support@frontapp.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="d9cf2-215">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d9cf2-216">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d9cf2-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="d9cf2-217">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Front에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="d9cf2-219">**Britta Simon을 Front에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d9cf2-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="d9cf2-220">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d9cf2-222">응용 프로그램 목록에서 **Front**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-222">In the applications list, select **Front**.</span></span>

    ![응용 프로그램 목록의 Front 링크](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="d9cf2-224">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-224">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="d9cf2-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-226">Click **Add** button.</span></span> <span data-ttu-id="d9cf2-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="d9cf2-229">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9cf2-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9cf2-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d9cf2-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d9cf2-232">Test single sign-on</span></span>

<span data-ttu-id="d9cf2-233">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="d9cf2-234">액세스 패널에서 Front 타일을 클릭하면 Front 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9cf2-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9cf2-235">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d9cf2-235">Additional resources</span></span>

* [<span data-ttu-id="d9cf2-236">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d9cf2-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9cf2-237">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d9cf2-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

