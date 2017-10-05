---
title: "자습서: Wdesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Wdesk 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="31611-103">자습서: Wdesk와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="31611-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="31611-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Wdesk를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31611-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31611-105">Wdesk를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="31611-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31611-106">Wdesk에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="31611-107">사용자가 해당 Azure AD 계정으로 Wdesk에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31611-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31611-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="31611-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="31611-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31611-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31611-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31611-111">Prerequisites</span></span>

<span data-ttu-id="31611-112">Wdesk와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="31611-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="31611-113">An Azure AD subscription</span></span>
- <span data-ttu-id="31611-114">Wdesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="31611-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31611-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31611-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31611-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="31611-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31611-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31611-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="31611-119">Scenario description</span></span>
<span data-ttu-id="31611-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31611-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31611-122">갤러리에서 Wdesk 추가</span><span class="sxs-lookup"><span data-stu-id="31611-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="31611-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="31611-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="31611-124">갤러리에서 Wdesk 추가</span><span class="sxs-lookup"><span data-stu-id="31611-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="31611-125">Wdesk의 Azure AD 통합을 구성하려면 갤러리의 Wdesk를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31611-126">**갤러리에서 Wdesk를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="31611-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31611-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31611-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31611-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-130">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="31611-132">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="31611-134">검색 상자에 **Wdesk**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-134">In the search box, type **Wdesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="31611-136">결과 창에서 **Wdesk**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31611-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="31611-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31611-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Wdesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="31611-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Wdesk 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="31611-141">즉, Azure AD 사용자와 Wdesk의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="31611-142">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Wdesk의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="31611-143">Wdesk에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31611-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31611-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31611-146">**[Wdesk 테스트 사용자 만들기](#creating-a-wdesk-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Wdesk에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31611-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31611-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31611-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31611-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="31611-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31611-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Wdesk 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="31611-151">**Wdesk에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="31611-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="31611-152">Azure Portal의 **Wdesk** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="31611-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="31611-156">**Wdesk 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="31611-158">a.</span><span class="sxs-lookup"><span data-stu-id="31611-158">a.</span></span> <span data-ttu-id="31611-159">**식별자** 텍스트 상자에서 `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="31611-160">b.</span><span class="sxs-lookup"><span data-stu-id="31611-160">b.</span></span> <span data-ttu-id="31611-161">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="31611-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="31611-162">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="31611-163">**SP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="31611-165">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="31611-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="31611-166">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="31611-166">These values are not real.</span></span> <span data-ttu-id="31611-167">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="31611-168">SSO를 구성할 때 WDesk 포털에서 이러한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="31611-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="31611-169">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="31611-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="31611-173">다른 웹 브라우저 창에서 Wdesk에 보안 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="31611-174">왼쪽 아래에서 **관리**를 클릭하고 **계정 관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="31611-176">Wdesk 관리에서 **보안**, **SAML** > **SAML 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="31611-178">**일반 설정**에서 **SAML Single Sign On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="31611-180">**서비스 공급자 세부 정보**에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="31611-182">a.</span><span class="sxs-lookup"><span data-stu-id="31611-182">a.</span></span> <span data-ttu-id="31611-183">**로그인 URL**을 복사한 후 Azure Portal의 **로그온 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="31611-184">b.</span><span class="sxs-lookup"><span data-stu-id="31611-184">b.</span></span> <span data-ttu-id="31611-185">**메타데이터 URL**을 복사한 후 Azure Portal의 **식별자** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="31611-186">c.</span><span class="sxs-lookup"><span data-stu-id="31611-186">c.</span></span> <span data-ttu-id="31611-187">**소비자 URL**을 복사한 후 Azure Portal의 **회신 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="31611-188">d.</span><span class="sxs-lookup"><span data-stu-id="31611-188">d.</span></span> <span data-ttu-id="31611-189">Azure Portal에서 **저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="31611-190">**IdP 설정 구성**을 클릭하여 **IdP 설정 편집** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31611-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="31611-191">**파일 선택**을 클릭하여 Azure Portal에서 저장한 **Metadata.xml** 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="31611-193">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-193">Click **Save changes**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="31611-195">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31611-196">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31611-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31611-197">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31611-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31611-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="31611-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="31611-199">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31611-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="31611-201">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="31611-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31611-202">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31611-204">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31611-206">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31611-208">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31611-210">a.</span><span class="sxs-lookup"><span data-stu-id="31611-210">a.</span></span> <span data-ttu-id="31611-211">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31611-212">b.</span><span class="sxs-lookup"><span data-stu-id="31611-212">b.</span></span> <span data-ttu-id="31611-213">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31611-214">c.</span><span class="sxs-lookup"><span data-stu-id="31611-214">c.</span></span> <span data-ttu-id="31611-215">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="31611-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31611-216">d.</span><span class="sxs-lookup"><span data-stu-id="31611-216">d.</span></span> <span data-ttu-id="31611-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="31611-218">Wdesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="31611-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="31611-219">Azure AD 사용자가 Wdesk에 로그인할 수 있도록 하려면 Wdesk로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="31611-220">Wdesk의 경우, 수동으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="31611-221">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="31611-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="31611-222">보안 관리자 권한으로 Wdesk에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="31611-223">**관리** > **계정 관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="31611-225">**피플** 아래에서 **구성원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="31611-226">이제 **구성원 추가**를 클릭하여 **구성원 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31611-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="31611-228">**사용자** 텍스트 상자에 **brittasimon@contoso.com** 과 같은 사용자의 사용자 이름을 입력하고 **계속** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="31611-230">아래와 같이 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-230">Enter the details as shown below:</span></span>
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="31611-232">a.</span><span class="sxs-lookup"><span data-stu-id="31611-232">a.</span></span> <span data-ttu-id="31611-233">**전자 메일** 텍스트 상자에 **brittasimon@contoso.com** 와 같은 사용자의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="31611-234">b.</span><span class="sxs-lookup"><span data-stu-id="31611-234">b.</span></span> <span data-ttu-id="31611-235">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="31611-236">c.</span><span class="sxs-lookup"><span data-stu-id="31611-236">c.</span></span> <span data-ttu-id="31611-237">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="31611-238">**구성원 저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-238">Click **Save Member** button.</span></span>  

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31611-240">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="31611-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31611-241">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Wdesk에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![사용자 할당][200] 

<span data-ttu-id="31611-243">**Britta Simon을 Wdesk에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="31611-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="31611-244">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="31611-246">응용 프로그램 목록에서 **Wdesk**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-246">In the applications list, select **Wdesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="31611-248">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-248">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="31611-250">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-250">Click **Add** button.</span></span> <span data-ttu-id="31611-251">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="31611-253">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31611-254">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31611-255">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31611-256">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="31611-256">Testing single sign-on</span></span>

<span data-ttu-id="31611-257">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="31611-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31611-258">액세스 패널에서 Wdesk 타일을 클릭하면 Wdesk 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="31611-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="31611-259">액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31611-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="31611-260">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="31611-260">Additional resources</span></span>

* [<span data-ttu-id="31611-261">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="31611-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31611-262">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="31611-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

