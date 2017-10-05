---
title: "자습서: Cerner Central과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Cerner Central 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="6a7ed-103">자습서: Cerner Central과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6a7ed-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="6a7ed-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Cerner Central을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a7ed-105">Cerner Central을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a7ed-106">Cerner Central에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="6a7ed-107">사용자가 해당 Azure AD 계정으로 Cerner Central에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a7ed-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a7ed-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a7ed-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6a7ed-110">Prerequisites</span></span>

<span data-ttu-id="6a7ed-111">Cerner Central과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="6a7ed-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6a7ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a7ed-113">승인된 Cerner Central 시스템 계정</span><span class="sxs-lookup"><span data-stu-id="6a7ed-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="6a7ed-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a7ed-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a7ed-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a7ed-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a7ed-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6a7ed-118">Scenario description</span></span>
<span data-ttu-id="6a7ed-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a7ed-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a7ed-121">갤러리에서 Cerner Central 추가</span><span class="sxs-lookup"><span data-stu-id="6a7ed-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="6a7ed-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6a7ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="6a7ed-123">갤러리에서 Cerner Central 추가</span><span class="sxs-lookup"><span data-stu-id="6a7ed-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="6a7ed-124">Cerner Central과 Azure AD의 통합을 구성하려면 갤러리의 Cerner Central을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a7ed-125">**갤러리에서 Cerner Central을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6a7ed-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a7ed-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a7ed-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a7ed-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6a7ed-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6a7ed-133">검색 상자에 **Cerner Central**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-133">In the search box, type **Cerner Central**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="6a7ed-135">결과 창에서 **Cerner Central**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a7ed-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6a7ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a7ed-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Cerner Central에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a7ed-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Cerner Central 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="6a7ed-140">즉, Azure AD 사용자와 Cerner Central의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="6a7ed-141">Cerner Central에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a7ed-142">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a7ed-143">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a7ed-144">**[Cerner Central 테스트 사용자 만들기](#creating-a-cerner-central-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Cerner Central에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="6a7ed-145">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a7ed-146">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a7ed-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6a7ed-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a7ed-148">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Cerner Central 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="6a7ed-149">**Cerner Central에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6a7ed-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="6a7ed-150">Azure Portal의 **Cerner Central** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6a7ed-152">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="6a7ed-154">**Cerner Central 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="6a7ed-156">a.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-156">a.</span></span> <span data-ttu-id="6a7ed-157">**식별자** 텍스트 상자에 다음과 같은 패턴을 사용하여 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="6a7ed-158">b.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-158">b.</span></span> <span data-ttu-id="6a7ed-159">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="6a7ed-160">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-160">These values are not the real.</span></span> <span data-ttu-id="6a7ed-161">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6a7ed-162">이러한 값을 얻으려면 [Cerner Central 지원 팀](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="6a7ed-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="6a7ed-165">**메타데이터** URL을 생성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="6a7ed-166">a.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-166">a.</span></span> <span data-ttu-id="6a7ed-167">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-167">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="6a7ed-169">b.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-169">b.</span></span> <span data-ttu-id="6a7ed-170">**끝점**을 클릭하여 **끝점** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="6a7ed-172">c.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-172">c.</span></span> <span data-ttu-id="6a7ed-173">복사 단추를 클릭하여 **페더레이션 메타데이터 문서** URL을 복사하여 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="6a7ed-175">d.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-175">d.</span></span> <span data-ttu-id="6a7ed-176">이제 **Cerner Central**의 속성 페이지로 이동하고 **복사** 단추를 사용하여 **응용 프로그램 ID**를 복사하여 매모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="6a7ed-178">e.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-178">e.</span></span> <span data-ttu-id="6a7ed-179">`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 패턴을 사용하여 **메타데이터 URL**을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="6a7ed-180">**Cerner Central** 쪽에서 Single Sign-On을 구성하려면 **메타데이터 URL**을 [Cerner Central 지원](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="6a7ed-181">그러면 응용 프로그램 쪽에서 SSO를 구성하여 통합을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="6a7ed-182">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a7ed-183">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a7ed-184">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a7ed-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6a7ed-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a7ed-186">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6a7ed-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="6a7ed-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a7ed-189">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a7ed-191">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a7ed-193">**사용자** 대화 상자를 열려면 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a7ed-195">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a7ed-197">a.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-197">a.</span></span> <span data-ttu-id="6a7ed-198">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a7ed-199">b.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-199">b.</span></span> <span data-ttu-id="6a7ed-200">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6a7ed-201">c.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-201">c.</span></span> <span data-ttu-id="6a7ed-202">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a7ed-203">d.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-203">d.</span></span> <span data-ttu-id="6a7ed-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="6a7ed-205">Cerner Central 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6a7ed-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="6a7ed-206">**Cerner Central** 응용 프로그램은 모든 페더레이션된 ID 공급자의 인증을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="6a7ed-207">사용자가 응용 프로그램 홈페이지에 로그인할 수 있다면 페더레이션되고 수동 프로비전이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a7ed-208">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6a7ed-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a7ed-209">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Cerner Central에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6a7ed-211">**Britta Simon을 Cerner Central에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="6a7ed-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="6a7ed-212">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6a7ed-214">응용 프로그램 목록에서 **Cerner Central**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-214">In the applications list, select **Cerner Central**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="6a7ed-216">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-216">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6a7ed-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-218">Click **Add** button.</span></span> <span data-ttu-id="6a7ed-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6a7ed-221">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a7ed-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a7ed-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a7ed-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6a7ed-224">Testing single sign-on</span></span>

<span data-ttu-id="6a7ed-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a7ed-226">액세스 패널에서 Cerner Central 타일을 클릭하면 Cerner Central 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="6a7ed-227">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a7ed-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a7ed-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6a7ed-228">Additional resources</span></span>

* [<span data-ttu-id="6a7ed-229">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="6a7ed-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a7ed-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6a7ed-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

