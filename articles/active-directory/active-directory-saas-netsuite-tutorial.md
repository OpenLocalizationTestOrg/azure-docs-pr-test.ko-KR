---
title: "자습서: Netsuite와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Netsuite 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="a0535-103">자습서: Netsuite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a0535-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="a0535-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Netsuite를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0535-105">Netsuite를Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0535-106">Netsuite에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="a0535-107">사용자가 자신의 Azure AD 계정으로 Netsuite에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0535-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0535-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0535-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0535-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a0535-110">Prerequisites</span></span>

<span data-ttu-id="a0535-111">Netsuite와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="a0535-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a0535-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0535-113">Netsuite Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a0535-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0535-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0535-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0535-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a0535-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0535-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0535-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a0535-118">Scenario description</span></span>
<span data-ttu-id="a0535-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0535-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0535-121">갤러리에서 Netsuite 추가</span><span class="sxs-lookup"><span data-stu-id="a0535-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="a0535-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0535-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="a0535-123">갤러리에서 Netsuite 추가</span><span class="sxs-lookup"><span data-stu-id="a0535-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="a0535-124">Netsuite가 Azure AD에 통합되도록 구성하려면 갤러리의 Netsuite를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0535-125">**갤러리에서 Netsuite를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0535-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0535-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0535-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0535-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a0535-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a0535-133">검색 상자에 **Netsuite**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-133">In the search box, type **Netsuite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="a0535-135">결과 패널에서 **Netsuite**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0535-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0535-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0535-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Netsuite에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0535-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Netsuite 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="a0535-140">즉, Azure AD 사용자와 Netsuite의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="a0535-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Netsuite의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="a0535-142">Netsuite에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0535-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0535-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0535-145">**[Netsuite 테스트 사용자 만들기](#creating-a-netsuite-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Netsuite에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0535-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0535-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0535-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a0535-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0535-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Netsuite 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="a0535-150">**Netsuite에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0535-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="a0535-151">Azure Portal의 **Netsuite** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a0535-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="a0535-155">**Netsuite 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="a0535-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.  `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="a0535-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0535-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-158">This value is not real value.</span></span> <span data-ttu-id="a0535-159">실제 회신 URL로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="a0535-160">이 값을 얻으려면 [Netsuite 지원 팀](http://www.netsuite.com/portal/services/support.shtml)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a0535-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="a0535-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="a0535-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0535-165">**Netsuite 구성** 섹션에서 **Netsuite 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a0535-166">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="a0535-168">브라우저에서 새 탭을 열고 관리자 권한으로 Netsuite 회사 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="a0535-169">페이지의 위쪽에 있는 도구 모음에서 **설치**를 클릭한 다음 **설치 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="a0535-171">**설치 작업** 목록에서 **통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="a0535-173">**인증 관리** 섹션에서 **SAML Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="a0535-175">**SAML 설정** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="a0535-176">a.</span><span class="sxs-lookup"><span data-stu-id="a0535-176">a.</span></span> <span data-ttu-id="a0535-177">**로그온 구성**의 **빠른 참조** 섹션에서 **SAML Single Sign-On 서비스 URL**을 복사하여 Netsuite의 **Identity Provider Login Page**(ID 공급자 로그인 페이지) 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="a0535-179">b.</span><span class="sxs-lookup"><span data-stu-id="a0535-179">b.</span></span> <span data-ttu-id="a0535-180">[Netsuite 설치]에서 **기본 인증 방법**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="a0535-181">c.</span><span class="sxs-lookup"><span data-stu-id="a0535-181">c.</span></span> <span data-ttu-id="a0535-182">**SAMLV2 ID 공급자 메타데이터** 필드에서 **IDP 메타 데이터 파일 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="a0535-183">그런 다음 **찾아보기**를 클릭하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="a0535-185">d.</span><span class="sxs-lookup"><span data-stu-id="a0535-185">d.</span></span> <span data-ttu-id="a0535-186">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-186">Click **Submit**.</span></span>

12. <span data-ttu-id="a0535-187">Azure AD에서 **기타 모든 사용자 특성 보기 및 편집** 확인란을 클릭하고 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="a0535-189">**특성 이름** 필드에 `account`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="a0535-190">**특성 값** 필드에서 Netsuite 계정 ID를 입력합니다. 이 값은 상수이며 계정에 따라 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="a0535-191">사용자의 계정 ID를 찾는 방법에 대한 지침은 아래에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-191">Instructions on how to find your account ID are included below:</span></span>

      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="a0535-193">a.</span><span class="sxs-lookup"><span data-stu-id="a0535-193">a.</span></span> <span data-ttu-id="a0535-194">Netsuite의 위쪽 탐색 메뉴에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="a0535-195">b.</span><span class="sxs-lookup"><span data-stu-id="a0535-195">b.</span></span> <span data-ttu-id="a0535-196">그런 다음 왼쪽 탐색 메뉴의 **Setup Tasks**(설치 작업) 섹션 아래를 클릭하고 **통합** 섹션을 선택한 다음 **Web Services Preferences**(웹 서비스 기본 설정)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="a0535-197">c.</span><span class="sxs-lookup"><span data-stu-id="a0535-197">c.</span></span> <span data-ttu-id="a0535-198">Netsuite 계정 ID를 복사하여 Azure AD의 **특성 값** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="a0535-200">사용자가 Netsuite에서 Single Sign-On을 수행하려면 먼저 Netsuite에 적절한 권한을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="a0535-201">이러한 사용 권한을 할당하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="a0535-202">a.</span><span class="sxs-lookup"><span data-stu-id="a0535-202">a.</span></span> <span data-ttu-id="a0535-203">위쪽 탐색 메뉴에서 **설치**를 클릭한 다음 **설치 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="a0535-205">b.</span><span class="sxs-lookup"><span data-stu-id="a0535-205">b.</span></span> <span data-ttu-id="a0535-206">왼쪽 탐색 메뉴에서 **사용자/역할**을 선택한 다음 **역할 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="a0535-208">c.</span><span class="sxs-lookup"><span data-stu-id="a0535-208">c.</span></span> <span data-ttu-id="a0535-209">**새 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-209">Click **New Role**.</span></span>

    <span data-ttu-id="a0535-210">d.</span><span class="sxs-lookup"><span data-stu-id="a0535-210">d.</span></span> <span data-ttu-id="a0535-211">새 역할에 대한 **이름**을 입력하고 **Single Sign-On Only**(Single Sign-On 전용) 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="a0535-213">e.</span><span class="sxs-lookup"><span data-stu-id="a0535-213">e.</span></span> <span data-ttu-id="a0535-214">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-214">Click **Save**.</span></span>

    <span data-ttu-id="a0535-215">f.</span><span class="sxs-lookup"><span data-stu-id="a0535-215">f.</span></span> <span data-ttu-id="a0535-216">위쪽에 있는 메뉴에서 **사용 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="a0535-217">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-217">Then click **Setup**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="a0535-219">g.</span><span class="sxs-lookup"><span data-stu-id="a0535-219">g.</span></span> <span data-ttu-id="a0535-220">**SAM Single Sign-On 설치**를 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="a0535-221">h.</span><span class="sxs-lookup"><span data-stu-id="a0535-221">h.</span></span> <span data-ttu-id="a0535-222">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-222">Click **Save**.</span></span>

    <span data-ttu-id="a0535-223">i.</span><span class="sxs-lookup"><span data-stu-id="a0535-223">i.</span></span> <span data-ttu-id="a0535-224">위쪽 탐색 메뉴에서 **설치**를 클릭한 다음 **설치 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="a0535-226">j.</span><span class="sxs-lookup"><span data-stu-id="a0535-226">j.</span></span> <span data-ttu-id="a0535-227">왼쪽 탐색 메뉴에서 **사용자/역할**을 선택한 다음 **사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="a0535-229">k.</span><span class="sxs-lookup"><span data-stu-id="a0535-229">k.</span></span> <span data-ttu-id="a0535-230">테스트 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-230">Select a test user.</span></span> <span data-ttu-id="a0535-231">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-231">Then click **Edit**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="a0535-233">l.</span><span class="sxs-lookup"><span data-stu-id="a0535-233">l.</span></span> <span data-ttu-id="a0535-234">역할 대화 상자에서 만든 역할을 선택하거 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="a0535-236">m.</span><span class="sxs-lookup"><span data-stu-id="a0535-236">m.</span></span> <span data-ttu-id="a0535-237">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="a0535-238">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0535-239">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0535-240">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0535-241">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a0535-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0535-242">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a0535-244">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a0535-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0535-245">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="a0535-247">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0535-249">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0535-251">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0535-253">a.</span><span class="sxs-lookup"><span data-stu-id="a0535-253">a.</span></span> <span data-ttu-id="a0535-254">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0535-255">b.</span><span class="sxs-lookup"><span data-stu-id="a0535-255">b.</span></span> <span data-ttu-id="a0535-256">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0535-257">c.</span><span class="sxs-lookup"><span data-stu-id="a0535-257">c.</span></span> <span data-ttu-id="a0535-258">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0535-259">d.</span><span class="sxs-lookup"><span data-stu-id="a0535-259">d.</span></span> <span data-ttu-id="a0535-260">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="a0535-261">Netsuite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a0535-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="a0535-262">이 섹션에서는 Netsuite에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="a0535-263">Netsuite는 Just-In-Time 프로비전을 지원하며, 이 프로비전은 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="a0535-264">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-264">There is no action item for you in this section.</span></span> <span data-ttu-id="a0535-265">Netsuite에 아직 사용자가 없으면 Netsuite에 액세스하려고 할 때 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0535-266">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a0535-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0535-267">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Netsuite에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a0535-269">**Britta Simon을 Netsuite에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0535-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="a0535-270">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a0535-272">응용 프로그램 목록에서 **Netsuite**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-272">In the applications list, select **Netsuite**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="a0535-274">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-274">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a0535-276">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-276">Click **Add** button.</span></span> <span data-ttu-id="a0535-277">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a0535-279">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0535-280">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0535-281">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0535-282">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a0535-282">Testing single sign-on</span></span>

<span data-ttu-id="a0535-283">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a0535-284">Single Sign-On 설정을 테스트하려면 [https://myapps.microsoft.com](https://myapps.microsoft.com/)에서 액세스 패널을 연 다음 테스트 계정에 로그인하고 **Netsuite**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0535-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0535-285">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a0535-285">Additional resources</span></span>

* [<span data-ttu-id="a0535-286">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a0535-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0535-287">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a0535-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a0535-288">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="a0535-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

