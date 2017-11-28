---
title: "자습서: Azure Active Directory와 Perception United States(비 UltiPro) 통합 | Microsoft Docs"
description: "Azure Active Directory와 Perception United States(비 UltiPro) 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8e2f9f979f8b94e0c043d4db6e93bd7a53c3dd27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="f03e1-103">자습서: Azure Active Directory와 Perception United States(비 UltiPro) 통합</span><span class="sxs-lookup"><span data-stu-id="f03e1-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="f03e1-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Perception United States(비 UltiPro)를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f03e1-105">Perception United States(비 UltiPro)를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f03e1-106">Perception United States(비 UltiPro)에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="f03e1-107">사용자가 해당 Azure AD 계정으로 Perception United States(비 UltiPro)에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f03e1-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f03e1-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f03e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f03e1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f03e1-110">Prerequisites</span></span>

<span data-ttu-id="f03e1-111">Perception United States(비 UltiPro)와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span></span>

- <span data-ttu-id="f03e1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f03e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f03e1-113">Perception United States(비 UltiPro) Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f03e1-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f03e1-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f03e1-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f03e1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f03e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f03e1-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f03e1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f03e1-118">Scenario description</span></span>
<span data-ttu-id="f03e1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f03e1-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f03e1-121">갤러리에서 Perception United States(비 UltiPro) 추가</span><span class="sxs-lookup"><span data-stu-id="f03e1-121">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
2. <span data-ttu-id="f03e1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f03e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a><span data-ttu-id="f03e1-123">갤러리에서 Perception United States(비 UltiPro) 추가</span><span class="sxs-lookup"><span data-stu-id="f03e1-123">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
<span data-ttu-id="f03e1-124">Perception United States(비 UltiPro)의 Azure AD 통합을 구성하려면 갤러리의 Perception United States(비 UltiPro)를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f03e1-125">**갤러리에서 Perception United States(비 UltiPro)를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f03e1-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f03e1-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="f03e1-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f03e1-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="f03e1-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="f03e1-133">검색 상자에 **Perception United States(비 UltiPro)**를 입력하고 결과 패널에서 **Perception United States(비 UltiPro)**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Perception United States(비 UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f03e1-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f03e1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f03e1-136">이 섹션에서는 Britta Simon이라는 테스트 사용자를 기반으로 Perception United States(비 UltiPro)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f03e1-137">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Perception United States(비 UltiPro) 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span></span> <span data-ttu-id="f03e1-138">즉, Azure AD 사용자와 Perception United States(비 UltiPro)의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span></span>

<span data-ttu-id="f03e1-139">Perception United States(비 UltiPro)에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f03e1-140">Perception United States(비 UltiPro)에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f03e1-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f03e1-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f03e1-143">**[Perception United States(비 UltiPro) 테스트 사용자 만들기](#create-a-perception-united-states-non-ultipro-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Perception United States(비 UltiPro)에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f03e1-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f03e1-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f03e1-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f03e1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f03e1-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Perception United States(비 UltiPro) 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="f03e1-148">**Perception United States(비 UltiPro)에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f03e1-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="f03e1-149">Azure Portal의 **Perception United States(비 UltiPro)** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="f03e1-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="f03e1-153">**Perception United States(비 UltiPro) 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span></span>

    ![Perception United States(비 UltiPro) 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="f03e1-155">a.</span><span class="sxs-lookup"><span data-stu-id="f03e1-155">a.</span></span> <span data-ttu-id="f03e1-156">**식별자** 텍스트 상자에 URL `https://perception.kanjoya.com/sp`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="f03e1-157">b.</span><span class="sxs-lookup"><span data-stu-id="f03e1-157">b.</span></span> <span data-ttu-id="f03e1-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="f03e1-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f03e1-159">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-159">The value is not real.</span></span> <span data-ttu-id="f03e1-160">자습서 뒷부분에 설명된 실제 회신 URL로 값을 업데이트하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="f03e1-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="f03e1-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-163">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f03e1-165">**Perception United States(비 UltiPro) 구성** 섹션에서 **Perception United States(비 UltiPro) 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f03e1-166">**빠른 참조 섹션**에서 **SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="f03e1-167">a.</span><span class="sxs-lookup"><span data-stu-id="f03e1-167">a.</span></span> <span data-ttu-id="f03e1-168">**Perception United States(비 UltiPro)** 응용 프로그램이 URI 인코딩이 되려면 복사한 **SAML 엔터티 ID** 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span></span> <span data-ttu-id="f03e1-169">URI 인코딩된 값을 가져오려면 다음 링크:**http://www.url-encode-decode.com/**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="f03e1-170">b.</span><span class="sxs-lookup"><span data-stu-id="f03e1-170">b.</span></span> <span data-ttu-id="f03e1-171">URI 인코딩된 값을 얻은 후 아래에서 설명된 것과 같이 **회신 URL**과 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="f03e1-172">c.</span><span class="sxs-lookup"><span data-stu-id="f03e1-172">c.</span></span> <span data-ttu-id="f03e1-173">**Perception United States(비 UltiPro) 도메인 및 URL** 섹션의 **회신 URL** 텍스트 상자에 위의 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Perception United States(비 UltiPro) 구성](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="f03e1-175">다른 웹 브라우저 창에서 Perception United States(비 UltiPro) 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="f03e1-176">주 도구 모음에서 **계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-176">In the main toolbar, click **Account Settings**.</span></span>

    ![Perception United States(비 UltiPro) 사용자](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="f03e1-178">**계정 설정** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-178">On the **Account Settings** page, perform the following steps:</span></span>

    ![Perception United States(비 UltiPro) 사용자](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="f03e1-180">a.</span><span class="sxs-lookup"><span data-stu-id="f03e1-180">a.</span></span> <span data-ttu-id="f03e1-181">**회사 이름** 텍스트 상자에 **회사**의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-181">In the **Company Name** textbox, type the name of the **Company**.</span></span>
    
    <span data-ttu-id="f03e1-182">b.</span><span class="sxs-lookup"><span data-stu-id="f03e1-182">b.</span></span> <span data-ttu-id="f03e1-183">**계정 이름** 텍스트 상자에 **계정**의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-183">In the **Account Name** textbox, type the name of the **Account**.</span></span>

    <span data-ttu-id="f03e1-184">c.</span><span class="sxs-lookup"><span data-stu-id="f03e1-184">c.</span></span> <span data-ttu-id="f03e1-185">**기본 회신 전자 메일** 텍스트 상자에 유효한 **전자 메일**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-185">In **Default Reply-To Email** text box, type the valid **Email**.</span></span>

    <span data-ttu-id="f03e1-186">d.</span><span class="sxs-lookup"><span data-stu-id="f03e1-186">d.</span></span> <span data-ttu-id="f03e1-187">**SAML 2.0**으로 **SSO ID 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="f03e1-188">**SSO 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-188">On the **SSO Configuration** page, perform the following steps:</span></span>

    ![Perception United States(비 UltiPro) SSO 구성](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="f03e1-190">a.</span><span class="sxs-lookup"><span data-stu-id="f03e1-190">a.</span></span> <span data-ttu-id="f03e1-191">**전자 메일**로 **SAML NameID 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="f03e1-192">b.</span><span class="sxs-lookup"><span data-stu-id="f03e1-192">b.</span></span> <span data-ttu-id="f03e1-193">**SSO 구성 이름** 텍스트 상자에 **구성**의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span></span>
    
    <span data-ttu-id="f03e1-194">c.</span><span class="sxs-lookup"><span data-stu-id="f03e1-194">c.</span></span> <span data-ttu-id="f03e1-195">**ID 공급자 이름** 텍스트 상자에 Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="f03e1-196">d.</span><span class="sxs-lookup"><span data-stu-id="f03e1-196">d.</span></span> <span data-ttu-id="f03e1-197">**SAML 도메인 텍스트 상자**에 **@contoso.com**과 같은 도메인을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span></span>

    <span data-ttu-id="f03e1-198">e.</span><span class="sxs-lookup"><span data-stu-id="f03e1-198">e.</span></span> <span data-ttu-id="f03e1-199">**다시 업로드**를 클릭하여 **메타데이터 XML** 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-199">Click on **Upload Again** to upload the **Metadata XML** file.</span></span>

    <span data-ttu-id="f03e1-200">f.</span><span class="sxs-lookup"><span data-stu-id="f03e1-200">f.</span></span> <span data-ttu-id="f03e1-201">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="f03e1-202">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f03e1-203">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f03e1-204">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f03e1-205">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f03e1-205">Create an Azure AD test user</span></span>

<span data-ttu-id="f03e1-206">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="f03e1-208">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f03e1-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f03e1-209">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f03e1-211">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f03e1-213">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f03e1-215">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-215">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f03e1-217">a.</span><span class="sxs-lookup"><span data-stu-id="f03e1-217">a.</span></span> <span data-ttu-id="f03e1-218">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f03e1-219">b.</span><span class="sxs-lookup"><span data-stu-id="f03e1-219">b.</span></span> <span data-ttu-id="f03e1-220">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f03e1-221">c.</span><span class="sxs-lookup"><span data-stu-id="f03e1-221">c.</span></span> <span data-ttu-id="f03e1-222">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f03e1-223">d.</span><span class="sxs-lookup"><span data-stu-id="f03e1-223">d.</span></span> <span data-ttu-id="f03e1-224">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="f03e1-225">Perception United States(비 UltiPro) 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f03e1-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="f03e1-226">이 섹션에서는 Perception United States(비 UltiPro)에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="f03e1-227">Perception United States(비 UltiPro) 플랫폼에 사용자를 추가하려면 [Perception United States(비 UltiPro) 지원 팀](http://www.ultimatesoftware.com/Contact/ContactUs)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f03e1-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f03e1-228">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f03e1-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="f03e1-229">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Perception United States(비 UltiPro)에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="f03e1-231">**Britta Simon을 Perception United States(비 UltiPro)에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f03e1-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="f03e1-232">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f03e1-234">응용 프로그램 목록에서 **Perception United States(비 UltiPro)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![응용 프로그램 목록의 Perception United States(비 UltiPro) 링크](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="f03e1-236">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-236">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="f03e1-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-238">Click **Add** button.</span></span> <span data-ttu-id="f03e1-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="f03e1-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f03e1-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f03e1-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f03e1-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f03e1-244">Test single sign-on</span></span>

<span data-ttu-id="f03e1-245">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f03e1-246">액세스 패널에서 Perception United States(비 UltiPro) 타일을 클릭하면 Perception United States(비 UltiPro) 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f03e1-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="f03e1-247">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f03e1-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f03e1-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f03e1-248">Additional resources</span></span>

* [<span data-ttu-id="f03e1-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f03e1-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f03e1-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f03e1-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

