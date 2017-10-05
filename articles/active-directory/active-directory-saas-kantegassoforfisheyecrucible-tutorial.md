---
title: "자습서: Kantega SSO for FishEye/Crucible과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Kantega SSO for FishEye/Crucible 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9eaa2ec661a3488b0bef1f6b7cc7a82290720054
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="a7d78-103">자습서: Kantega SSO for FishEye/Crucible과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a7d78-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="a7d78-104">이 자습서에서는 Kantega SSO for FishEye/Crucible을 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-104">In this tutorial, you learn how to integrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7d78-105">Kantega SSO for FishEye/Crucible을 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7d78-106">Kantega SSO for FishEye/Crucible에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-106">You can control in Azure AD who has access to Kantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="a7d78-107">사용자가 자신의 Azure AD 계정으로 Kantega SSO for FishEye/Crucible에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-107">You can enable your users to automatically get signed-on to Kantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7d78-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7d78-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7d78-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7d78-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a7d78-110">Prerequisites</span></span>

<span data-ttu-id="a7d78-111">Kantega SSO for FishEye/Crucible과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-111">To configure Azure AD integration with Kantega SSO for FishEye/Crucible, you need the following items:</span></span>

- <span data-ttu-id="a7d78-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a7d78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7d78-113">Kantega SSO for FishEye/Crucible Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a7d78-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7d78-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7d78-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7d78-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a7d78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7d78-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7d78-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a7d78-118">Scenario description</span></span>
<span data-ttu-id="a7d78-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7d78-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7d78-121">갤러리에서 Kantega SSO for FishEye/Crucible 추가</span><span class="sxs-lookup"><span data-stu-id="a7d78-121">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
2. <span data-ttu-id="a7d78-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a7d78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-the-gallery"></a><span data-ttu-id="a7d78-123">갤러리에서 Kantega SSO for FishEye/Crucible 추가</span><span class="sxs-lookup"><span data-stu-id="a7d78-123">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
<span data-ttu-id="a7d78-124">Kantega SSO for FishEye/Crucible이 Azure AD에 통합되도록 구성하려면 갤러리에서 Kantega SSO for FishEye/Crucible을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-124">To configure the integration of Kantega SSO for FishEye/Crucible into Azure AD, you need to add Kantega SSO for FishEye/Crucible from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7d78-125">**갤러리에서 Kantega SSO for FishEye/Crucible을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7d78-125">**To add Kantega SSO for FishEye/Crucible from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d78-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7d78-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7d78-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a7d78-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a7d78-133">검색 상자에 **Kantega SSO for FishEye/Crucible**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-133">In the search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="a7d78-135">결과 창에서 **Kantega SSO for FishEye/Crucible**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-135">In the results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7d78-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a7d78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7d78-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Kantega SSO for FishEye/Crucible에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7d78-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Kantega SSO for FishEye/Crucible 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for FishEye/Crucible is to a user in Azure AD.</span></span> <span data-ttu-id="a7d78-140">즉, Azure AD 사용자와 Kantega SSO for FishEye/Crucible의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for FishEye/Crucible needs to be established.</span></span>

<span data-ttu-id="a7d78-141">Kantega SSO for FishEye/Crucible에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-141">In Kantega SSO for FishEye/Crucible, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7d78-142">Kantega SSO for FishEye/Crucible에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-142">To configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7d78-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7d78-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7d78-145">**[Kantega SSO for FishEye/Crucible 테스트 사용자 만들기](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Kantega SSO for FishEye/Crucible에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7d78-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7d78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7d78-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a7d78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7d78-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Kantega SSO for FishEye/Crucible 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="a7d78-150">**Kantega SSO for FishEye/Crucible에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7d78-150">**To configure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d78-151">Azure Portal의 **Kantega SSO for FishEye/Crucible** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-151">In the Azure portal, on the **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a7d78-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="a7d78-155">**IDP** 시작 모드로 **Kantega SSO for FishEye/Crucible 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-155">In **IDP** initiated mode, on the **Kantega SSO for FishEye/Crucible Domain and URLs** section perform the following step :</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="a7d78-157">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-157">a.</span></span> <span data-ttu-id="a7d78-158">**식별자** 텍스트 상자에서 `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="a7d78-159">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-159">b.</span></span> <span data-ttu-id="a7d78-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="a7d78-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="a7d78-161">**SP** 시작 모드에서 **고급 URL 설정 표시**를 확인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="a7d78-163">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="a7d78-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a7d78-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-164">These values are not real.</span></span> <span data-ttu-id="a7d78-165">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a7d78-166">이러한 값은 FishEye/Crucible 플러그 인 구성 중에 수신되며 자습서의 뒷부분에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-166">These values are recieved during the configuration of FishEye/Crucible plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="a7d78-167">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="a7d78-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a7d78-171">다른 웹 브라우저 창에서 FishEye/Crucible 온-프레미스 서버에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-171">In a different web browser window, log in to your FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="a7d78-172">마우스로 선 위를 가리키고 **추가 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="a7d78-174">시스템 설정 섹션에서 **새 추가 기능 찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="a7d78-176">**Kantega SSO for Crucible**을 검색하고 **설치** 단추를 클릭하여 새 SAML 플러그 인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-176">Search **Kantega SSO for Crucible** and click **Install** button to install the new SAML plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="a7d78-178">플러그 인 설치가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-178">The plugin installation starts.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="a7d78-180">설치가 완료되면</span><span class="sxs-lookup"><span data-stu-id="a7d78-180">Once the installation is complete.</span></span> <span data-ttu-id="a7d78-181">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-181">Click **Close**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="a7d78-183">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-183">Click **Manage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="a7d78-185">**구성**을 클릭하여 새 플러그 인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-185">Click **Configure** to configure the new plugin.</span></span>    

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="a7d78-187">**SAML** 섹션의</span><span class="sxs-lookup"><span data-stu-id="a7d78-187">In the **SAML** section.</span></span> <span data-ttu-id="a7d78-188">**ID 공급자 추가** 드롭다운에서 **Azure AD(Azure Active Directory)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="a7d78-190">구독 수준을 **기본**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-190">Select subscription level as **Basic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="a7d78-192">**앱 속성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-192">On the **App properties** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="a7d78-194">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-194">a.</span></span> <span data-ttu-id="a7d78-195">**앱 ID URI**을 복사하여 Azure Portal의 **Kantega SSO for FishEye/Crucible 도메인 및 URL** 섹션에서 **식별자, 회신 URL 및 로그온 URL**로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="a7d78-196">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-196">b.</span></span> <span data-ttu-id="a7d78-197">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-197">Click **Next**.</span></span>

18. <span data-ttu-id="a7d78-198">**Metadata import**(메타데이터 가져오기) 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-198">On the **Metadata import** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="a7d78-200">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-200">a.</span></span> <span data-ttu-id="a7d78-201">**Metadata file on my computer**(내 컴퓨터의 메타데이터 파일)를 클릭하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="a7d78-202">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-202">b.</span></span> <span data-ttu-id="a7d78-203">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-203">Click **Next**.</span></span>

19. <span data-ttu-id="a7d78-204">**Name and SSO location**(이름 및 SSO 위치) 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="a7d78-206">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-206">a.</span></span> <span data-ttu-id="a7d78-207">**ID 공급자 이름** 텍스트 상자에 ID 공급자의 이름(예: Azure AD)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="a7d78-208">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-208">b.</span></span> <span data-ttu-id="a7d78-209">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-209">Click **Next**.</span></span>

20. <span data-ttu-id="a7d78-210">서명 인증서를 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-210">Verify the Signing certificate and click **Next**.</span></span>  

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="a7d78-212">**FishEye 사용자 계정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-212">On the **FishEye user accounts** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="a7d78-214">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-214">a.</span></span> <span data-ttu-id="a7d78-215">선택 **필요한 경우 물고기의 내부 디렉터리에서 사용자를 만들려면** 사용자에 대 한 그룹의 적절 한 이름을 입력 하 고 (수 여러 아니요.</span><span class="sxs-lookup"><span data-stu-id="a7d78-215">Select **Create users in FishEye's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="a7d78-216">그룹의 쉼표로 구분).</span><span class="sxs-lookup"><span data-stu-id="a7d78-216">of groups separated by comma).</span></span>

    <span data-ttu-id="a7d78-217">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-217">b.</span></span> <span data-ttu-id="a7d78-218">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-218">Click **Next**.</span></span>

22. <span data-ttu-id="a7d78-219">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-219">Click **Finish**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="a7d78-221">**Known domains for Azure AD**(Azure AD에 알려진 도메인) 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="a7d78-223">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-223">a.</span></span> <span data-ttu-id="a7d78-224">페이지의 왼쪽 창에서 **Known domains**(알려진 도메인)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="a7d78-225">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-225">b.</span></span> <span data-ttu-id="a7d78-226">**Known domains**(알려진 도메인) 텍스트 상자에 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="a7d78-227">c.</span><span class="sxs-lookup"><span data-stu-id="a7d78-227">c.</span></span> <span data-ttu-id="a7d78-228">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="a7d78-229">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7d78-230">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7d78-231">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7d78-232">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d78-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7d78-233">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a7d78-235">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a7d78-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d78-236">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7d78-238">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7d78-240">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7d78-242">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7d78-244">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-244">a.</span></span> <span data-ttu-id="a7d78-245">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7d78-246">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-246">b.</span></span> <span data-ttu-id="a7d78-247">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7d78-248">c.</span><span class="sxs-lookup"><span data-stu-id="a7d78-248">c.</span></span> <span data-ttu-id="a7d78-249">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7d78-250">d.</span><span class="sxs-lookup"><span data-stu-id="a7d78-250">d.</span></span> <span data-ttu-id="a7d78-251">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="a7d78-252">Kantega SSO for FishEye/Crucible 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a7d78-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="a7d78-253">Azure AD 사용자가 FishEye/Crucible에 로그인할 수 있도록 하려면 FishEye/Crucible로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-253">To enable Azure AD users to log in to FishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="a7d78-254">Kantega SSO for FishEye/Crucible에서는 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="a7d78-255">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7d78-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d78-256">Crucible 온-프레미스 서버에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-256">Log in to your Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="a7d78-257">마우스로 톱니바퀴를 가리키고 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-257">Hover on cog and click the **Users**.</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="a7d78-259">**사용자** 탭 섹션에서 **사용자 추가** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-259">Under **Users** tab section, click **Add user**.</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="a7d78-261">**새 사용자 추가** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-261">On the **Add New User** dialog page, perform the following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="a7d78-263">a.</span><span class="sxs-lookup"><span data-stu-id="a7d78-263">a.</span></span> <span data-ttu-id="a7d78-264">**사용자 이름** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="a7d78-265">b.</span><span class="sxs-lookup"><span data-stu-id="a7d78-265">b.</span></span> <span data-ttu-id="a7d78-266">**표시 이름** 텍스트 상자에 사용자의 표시 이름(예: Britta Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-266">In the **Display Name** textbox, type display name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="a7d78-267">c.</span><span class="sxs-lookup"><span data-stu-id="a7d78-267">c.</span></span> <span data-ttu-id="a7d78-268">**이메일 주소** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="a7d78-269">d.</span><span class="sxs-lookup"><span data-stu-id="a7d78-269">d.</span></span> <span data-ttu-id="a7d78-270">**암호** 텍스트 상자에서 사용자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="a7d78-271">e.</span><span class="sxs-lookup"><span data-stu-id="a7d78-271">e.</span></span> <span data-ttu-id="a7d78-272">**암호 확인** 텍스트 상자에 사용자의 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="a7d78-273">f.</span><span class="sxs-lookup"><span data-stu-id="a7d78-273">f.</span></span> <span data-ttu-id="a7d78-274">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-274">Click **Add**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7d78-275">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a7d78-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7d78-276">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Kantega SSO for FishEye/Crucible에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for FishEye/Crucible.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a7d78-278">**Britta Simon을 Kantega SSO for FishEye/Crucible에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7d78-278">**To assign Britta Simon to Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d78-279">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a7d78-281">응용 프로그램 목록에서 **Kantega SSO for FishEye/Crucible**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-281">In the applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="a7d78-283">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-283">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a7d78-285">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-285">Click **Add** button.</span></span> <span data-ttu-id="a7d78-286">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a7d78-288">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7d78-289">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7d78-290">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7d78-291">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a7d78-291">Testing single sign-on</span></span>

<span data-ttu-id="a7d78-292">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7d78-293">액세스 패널에서 Kantega SSO for FishEye/Crucible 타일을 클릭하면 Kantega SSO for FishEye/Crucible 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7d78-293">When you click the Kantega SSO for FishEye/Crucible tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="a7d78-294">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7d78-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7d78-295">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a7d78-295">Additional resources</span></span>

* [<span data-ttu-id="a7d78-296">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a7d78-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7d78-297">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a7d78-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

