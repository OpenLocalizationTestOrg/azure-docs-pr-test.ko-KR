---
title: "자습서: YouEarnedIt과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 YouEarnedIt 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="a39d9-103">자습서: Azure Active Directory와 YouEarnedIt 통합</span><span class="sxs-lookup"><span data-stu-id="a39d9-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="a39d9-104">이 자습서에서는 Azure AD(Azure Active Directory)와 YouEarnedIt을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a39d9-105">YouEarnedIt을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a39d9-106">YouEarnedIt에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="a39d9-107">사용자가 해당 Azure AD 계정으로 YouEarnedIt에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a39d9-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a39d9-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a39d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a39d9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a39d9-110">Prerequisites</span></span>

<span data-ttu-id="a39d9-111">YouEarnedIt과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="a39d9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a39d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a39d9-113">YouEarnedIt Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a39d9-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a39d9-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a39d9-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a39d9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a39d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a39d9-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a39d9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a39d9-118">Scenario description</span></span>
<span data-ttu-id="a39d9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a39d9-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a39d9-121">갤러리에서 YouEarnedIt 추가</span><span class="sxs-lookup"><span data-stu-id="a39d9-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="a39d9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a39d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="a39d9-123">갤러리에서 YouEarnedIt 추가</span><span class="sxs-lookup"><span data-stu-id="a39d9-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="a39d9-124">YouEarnedIt의 Azure AD 통합을 구성하려면 갤러리의 YouEarnedIt을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a39d9-125">**갤러리에서 YouEarnedIt을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a39d9-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a39d9-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="a39d9-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a39d9-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="a39d9-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="a39d9-133">검색 상자에 **YouEarnedIt**를 입력하고 결과 패널에서 **YouEarnedIt**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a39d9-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a39d9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a39d9-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 YouEarnedIt에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a39d9-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 YouEarnedIt 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="a39d9-138">즉, Azure AD 사용자와 YouEarnedIt의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="a39d9-139">YouEarnedIt에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a39d9-140">YouEarnedIt에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a39d9-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a39d9-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a39d9-143">**[YouEarnedIt 테스트 사용자 만들기](#create-a-youearnedit-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 YouEarnedIt에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a39d9-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a39d9-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a39d9-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a39d9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a39d9-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 YouEarnedIt 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="a39d9-148">**YouEarnedIt에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a39d9-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="a39d9-149">Azure Portal의 **YouEarnedIt** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="a39d9-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="a39d9-153">**YouEarnedIt 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![YouEarnedIt 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="a39d9-155">a.</span><span class="sxs-lookup"><span data-stu-id="a39d9-155">a.</span></span> <span data-ttu-id="a39d9-156">**로그온 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="a39d9-157">Environment</span><span class="sxs-lookup"><span data-stu-id="a39d9-157">Environment</span></span>  | <span data-ttu-id="a39d9-158">패턴</span><span class="sxs-lookup"><span data-stu-id="a39d9-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="a39d9-159">프로덕션</span><span class="sxs-lookup"><span data-stu-id="a39d9-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="a39d9-160">샌드박스</span><span class="sxs-lookup"><span data-stu-id="a39d9-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="a39d9-161">b.</span><span class="sxs-lookup"><span data-stu-id="a39d9-161">b.</span></span> <span data-ttu-id="a39d9-162">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="a39d9-163">Environment</span><span class="sxs-lookup"><span data-stu-id="a39d9-163">Environment</span></span>  | <span data-ttu-id="a39d9-164">패턴</span><span class="sxs-lookup"><span data-stu-id="a39d9-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="a39d9-165">프로덕션</span><span class="sxs-lookup"><span data-stu-id="a39d9-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="a39d9-166">샌드박스</span><span class="sxs-lookup"><span data-stu-id="a39d9-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="a39d9-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-167">These values are not real.</span></span> <span data-ttu-id="a39d9-168">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a39d9-169">이러한 값을 얻으려면 [YouEarnedIt 클라이언트 지원 팀](https://youearnedit.freshdesk.com/support/tickets/new)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a39d9-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="a39d9-170">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="a39d9-172">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-172">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a39d9-174">**YouEarnedIt 구성** 섹션에서 **YouEarnedIt 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a39d9-175">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![YouEarnedIt 구성](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="a39d9-177">**YouEarnedIt** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서(Base64)** 및 **SAML Single Sign-On 서비스 URL**을 [YouEarnedIt 지원 팀](https://youearnedit.freshdesk.com/support/tickets/new)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="a39d9-178">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a39d9-179">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a39d9-180">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a39d9-181">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a39d9-182">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a39d9-182">Create an Azure AD test user</span></span>

<span data-ttu-id="a39d9-183">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="a39d9-185">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a39d9-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a39d9-186">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a39d9-188">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a39d9-190">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a39d9-192">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-192">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a39d9-194">a.</span><span class="sxs-lookup"><span data-stu-id="a39d9-194">a.</span></span> <span data-ttu-id="a39d9-195">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a39d9-196">b.</span><span class="sxs-lookup"><span data-stu-id="a39d9-196">b.</span></span> <span data-ttu-id="a39d9-197">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a39d9-198">c.</span><span class="sxs-lookup"><span data-stu-id="a39d9-198">c.</span></span> <span data-ttu-id="a39d9-199">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a39d9-200">d.</span><span class="sxs-lookup"><span data-stu-id="a39d9-200">d.</span></span> <span data-ttu-id="a39d9-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="a39d9-202">YouEarnedIt 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a39d9-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="a39d9-203">이 섹션에서는 YouEarnedIt에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="a39d9-204">YouEarnedIt 플랫폼에서 사용자를 추가하려면 YouEarnedIt 지원 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a39d9-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="a39d9-205">YouEarnedIt은 ID 공급자가 NameID 특성의 EmailAddress 또는 UserName을 제공할 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="a39d9-206">해당 UserName 또는 EmailAddress가 데이터베이스 내에 없거나 정확히 일치하지 않을 경우 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="a39d9-207">이 경우 SSO 통합 전에 YouEarnedIt 시스템으로 계정을 가져와야 합니다(일반적으로 API 또는 CSV 가져오기를 통해).</span><span class="sxs-lookup"><span data-stu-id="a39d9-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a39d9-208">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a39d9-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="a39d9-209">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 YouEarnedIt에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="a39d9-211">**Britta Simon을 YouEarnedIt에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a39d9-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="a39d9-212">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a39d9-214">응용 프로그램 목록에서 **YouEarnedIt**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![응용 프로그램 목록의 YouEarnedIt 연결](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="a39d9-216">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-216">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="a39d9-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-218">Click **Add** button.</span></span> <span data-ttu-id="a39d9-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="a39d9-221">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a39d9-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a39d9-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a39d9-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a39d9-224">Test single sign-on</span></span>

<span data-ttu-id="a39d9-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a39d9-226">액세스 패널에서 YouEarnedIt 타일을 클릭하면 YouEarnedIt 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a39d9-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="a39d9-227">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a39d9-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a39d9-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a39d9-228">Additional resources</span></span>

* [<span data-ttu-id="a39d9-229">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a39d9-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a39d9-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a39d9-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

