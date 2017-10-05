---
title: "자습서: InsideView와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 InsideView 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: f2b0a1d4bc44f8d0cd57c61e2d78950cb6a99854
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="a53e9-103">자습서: InsideView와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a53e9-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="a53e9-104">이 자습서에서는 Azure AD(Azure Active Directory)와 InsideView를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-104">In this tutorial, you learn how to integrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a53e9-105">InsideView를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-105">Integrating InsideView with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a53e9-106">InsideView에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-106">You can control in Azure AD who has access to InsideView</span></span>
- <span data-ttu-id="a53e9-107">사용자가 해당 Azure AD 계정으로 InsideView에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-107">You can enable your users to automatically get signed-on to InsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a53e9-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a53e9-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a53e9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a53e9-110">Prerequisites</span></span>

<span data-ttu-id="a53e9-111">InsideView와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-111">To configure Azure AD integration with InsideView, you need the following items:</span></span>

- <span data-ttu-id="a53e9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a53e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a53e9-113">InsideView Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a53e9-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a53e9-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a53e9-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a53e9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a53e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a53e9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a53e9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a53e9-118">Scenario description</span></span>
<span data-ttu-id="a53e9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a53e9-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a53e9-121">갤러리에서 InsideView 추가</span><span class="sxs-lookup"><span data-stu-id="a53e9-121">Adding InsideView from the gallery</span></span>
2. <span data-ttu-id="a53e9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a53e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-the-gallery"></a><span data-ttu-id="a53e9-123">갤러리에서 InsideView 추가</span><span class="sxs-lookup"><span data-stu-id="a53e9-123">Adding InsideView from the gallery</span></span>
<span data-ttu-id="a53e9-124">InsideView의 Azure AD 통합을 구성하려면 갤러리의 InsideView를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-124">To configure the integration of InsideView in to Azure AD, you need to add InsideView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a53e9-125">**갤러리에서 InsideView를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a53e9-125">**To add InsideView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a53e9-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a53e9-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a53e9-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a53e9-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a53e9-133">검색 상자에 **InsideView**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-133">In the search box, type **InsideView**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="a53e9-135">결과 패널에서 **InsideView**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-135">In the results panel, select **InsideView**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a53e9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a53e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a53e9-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 InsideView에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a53e9-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 InsideView 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in InsideView is to a user in Azure AD.</span></span> <span data-ttu-id="a53e9-140">즉, Azure AD 사용자와 InsideView의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-140">In other words, a link relationship between an Azure AD user and the related user in InsideView needs to be established.</span></span>

<span data-ttu-id="a53e9-141">InsideView에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-141">In InsideView, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a53e9-142">InsideView에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-142">To configure and test Azure AD single sign-on with InsideView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a53e9-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a53e9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a53e9-145">**[InsideView 테스트 사용자 만들기](#creating-a-insideview-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 InsideView에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - to have a counterpart of Britta Simon in InsideView that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a53e9-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a53e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a53e9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a53e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a53e9-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 InsideView 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="a53e9-150">**InsideView에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a53e9-150">**To configure Azure AD single sign-on with InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="a53e9-151">Azure Portal의 **InsideView** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-151">In the Azure portal, on the **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a53e9-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="a53e9-155">**InsideView 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-155">On the **InsideView Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="a53e9-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="a53e9-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a53e9-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-158">This value is not real.</span></span> <span data-ttu-id="a53e9-159">실제 회신 URL로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="a53e9-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="a53e9-160">이 값을 가져오려면 [InsideView 지원 팀](mailto:support@insideview.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a53e9-160">Contact [InsideView support team ](mailto:support@insideview.com) to get this value.</span></span>
 
4. <span data-ttu-id="a53e9-161">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="a53e9-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a53e9-165">**InsideView 구성** 섹션에서 **InsideView 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-165">On the **InsideView Configuration** section, click **Configure InsideView** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a53e9-166">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="a53e9-168">다른 웹 브라우저 창에서 InsideView 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-168">In a different web browser window, log in to your InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="a53e9-169">위쪽의 도구 모음에서 **관리자**, **SingleSignOn 설정**을 클릭한 다음 **SAML 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-169">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="a53e9-170">![SAML Single Sign On 설정](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On 설정")</span><span class="sxs-lookup"><span data-stu-id="a53e9-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="a53e9-171">**새 SAML 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-171">In the **Add a New SAML** section, perform the following steps:</span></span>

    <span data-ttu-id="a53e9-172">![새 SAML 추가](./media/active-directory-saas-insideview-tutorial/ic794136.png "새 SAML 추가")</span><span class="sxs-lookup"><span data-stu-id="a53e9-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="a53e9-173">a.</span><span class="sxs-lookup"><span data-stu-id="a53e9-173">a.</span></span> <span data-ttu-id="a53e9-174">**STS 이름** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-174">In the **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="a53e9-175">b.</span><span class="sxs-lookup"><span data-stu-id="a53e9-175">b.</span></span> <span data-ttu-id="a53e9-176">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SamlP/WS-Fed Unsolicited EndPoint**(SamlP/WS-Fed 원치 않는 끝점) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a53e9-177">c.</span><span class="sxs-lookup"><span data-stu-id="a53e9-177">c.</span></span> <span data-ttu-id="a53e9-178">Azure Portal에서 다운로드한 Base-64로 인코딩된 인증서를 열고, 내용을 클립보드에 복사한 다음, **STS Certificate**(STS 인증서) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox.</span></span>

    <span data-ttu-id="a53e9-179">d.</span><span class="sxs-lookup"><span data-stu-id="a53e9-179">d.</span></span> <span data-ttu-id="a53e9-180">**Crm User Id Mapping**(Crm 사용자 ID 매핑) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-180">In the **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="a53e9-181">e.</span><span class="sxs-lookup"><span data-stu-id="a53e9-181">e.</span></span> <span data-ttu-id="a53e9-182">**Crm Email Mapping**(Crm 메일 매핑) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-182">In the **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="a53e9-183">f.</span><span class="sxs-lookup"><span data-stu-id="a53e9-183">f.</span></span> <span data-ttu-id="a53e9-184">**Crm First Name Mapping**(Crm 이름 매핑) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-184">In the **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="a53e9-185">g.</span><span class="sxs-lookup"><span data-stu-id="a53e9-185">g.</span></span> <span data-ttu-id="a53e9-186">**Crm lastName Mapping**(Crm 성 매핑) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-186">In the **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="a53e9-187">h.</span><span class="sxs-lookup"><span data-stu-id="a53e9-187">h.</span></span> <span data-ttu-id="a53e9-188">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a53e9-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a53e9-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a53e9-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a53e9-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a53e9-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="a53e9-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a53e9-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a53e9-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a53e9-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a53e9-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a53e9-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a53e9-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a53e9-204">a.</span><span class="sxs-lookup"><span data-stu-id="a53e9-204">a.</span></span> <span data-ttu-id="a53e9-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a53e9-206">b.</span><span class="sxs-lookup"><span data-stu-id="a53e9-206">b.</span></span> <span data-ttu-id="a53e9-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a53e9-208">c.</span><span class="sxs-lookup"><span data-stu-id="a53e9-208">c.</span></span> <span data-ttu-id="a53e9-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a53e9-210">d.</span><span class="sxs-lookup"><span data-stu-id="a53e9-210">d.</span></span> <span data-ttu-id="a53e9-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="a53e9-212">InsideView 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a53e9-212">Creating a InsideView test user</span></span>

<span data-ttu-id="a53e9-213">Azure AD 사용자가 InsideView에 로그인할 수 있도록 하려면 InsideView로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-213">To enable Azure AD users to log in to InsideView, they must be provisioned in to InsideView.</span></span> <span data-ttu-id="a53e9-214">InsideView의 경우 프로비저닝은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-214">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="a53e9-215">InsideView에서 생성된 사용자 또는 연락처를 얻으려면 [InsideView 지원 팀](mailto:support@insideview.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a53e9-215">To get users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="a53e9-216">다른 InsideView 사용자 계정 생성 도구 또는 InsideView가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비저닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-216">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a53e9-217">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a53e9-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a53e9-218">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 InsideView에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InsideView.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a53e9-220">**Britta Simon을 InsideView에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a53e9-220">**To assign Britta Simon to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="a53e9-221">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a53e9-223">응용 프로그램 목록에서 **InsideView**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-223">In the applications list, select **InsideView**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="a53e9-225">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-225">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a53e9-227">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-227">Click **Add** button.</span></span> <span data-ttu-id="a53e9-228">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a53e9-230">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a53e9-231">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a53e9-232">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a53e9-233">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a53e9-233">Testing single sign-on</span></span>

<span data-ttu-id="a53e9-234">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a53e9-235">액세스 패널에서 InsideView 타일을 클릭하면 InsideView 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a53e9-235">When you click the InsideView tile in the Access Panel, you should get automatically signed-on to your InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a53e9-236">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a53e9-236">Additional resources</span></span>

* [<span data-ttu-id="a53e9-237">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a53e9-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a53e9-238">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a53e9-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

