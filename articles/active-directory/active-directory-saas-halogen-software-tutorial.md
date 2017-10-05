---
title: "자습서: Halogen Software와 Azure Active Directory 통합| Microsoft Azure"
description: "Azure Active Directory 및 Halogen Software 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="57531-103">자습서: Halogen Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="57531-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="57531-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Halogen Software를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="57531-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57531-105">Halogen Software를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57531-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57531-106">Halogen Software에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="57531-107">사용자가 해당 Azure AD 계정으로 Halogen Software에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57531-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57531-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57531-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57531-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="57531-110">Prerequisites</span></span>

<span data-ttu-id="57531-111">Halogen Software와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="57531-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="57531-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57531-113">Halogen Software Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="57531-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57531-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57531-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57531-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="57531-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57531-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57531-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="57531-118">Scenario description</span></span>

<span data-ttu-id="57531-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57531-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57531-121">갤러리에서 Halogen Software 추가</span><span class="sxs-lookup"><span data-stu-id="57531-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="57531-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="57531-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="57531-123">갤러리에서 Halogen Software 추가</span><span class="sxs-lookup"><span data-stu-id="57531-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="57531-124">Halogen Software의 Azure AD 통합을 구성하려면 갤러리의 Halogen Software를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57531-125">**갤러리에서 Halogen Software를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="57531-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57531-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57531-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57531-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="57531-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="57531-133">검색 상자에 **Halogen Software**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-133">In the search box, type **Halogen Software**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="57531-135">결과 패널에서 **Halogen Software**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57531-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="57531-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57531-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Halogen Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57531-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD의 사용자에 해당하는 Halogen Software의 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="57531-140">즉, Azure AD 사용자와 Halogen Software의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="57531-141">Halogen Software에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57531-142">Halogen Software에서 Azure AD Single Sign-on을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57531-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57531-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57531-145">**[Halogen Software 테스트 사용자 만들기](#creating-a-halogen-software-test-user)** - Britta Simon의 Azure AD 사용자 표현과 연결되는 대응 사용자를 Halogen Software에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57531-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57531-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57531-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57531-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="57531-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57531-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Halogen Software 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="57531-150">**Halogen Software에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="57531-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="57531-151">Azure Portal의 **Halogen Software** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="57531-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="57531-155">**Halogen Software 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="57531-157">a.</span><span class="sxs-lookup"><span data-stu-id="57531-157">a.</span></span> <span data-ttu-id="57531-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="57531-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="57531-159">b.</span><span class="sxs-lookup"><span data-stu-id="57531-159">b.</span></span> <span data-ttu-id="57531-160">**식별자** 텍스트 상자에서 `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57531-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="57531-161">These values are not real.</span></span> <span data-ttu-id="57531-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="57531-163">이러한 값을 얻으려면 [Halogen Software 클라이언트 지원 팀](https://support.halogensoftware.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="57531-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="57531-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="57531-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57531-168">다른 브라우저 창에서 **Halogen Software** 응용 프로그램에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="57531-169">**옵션** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-169">Click the **Options** tab.</span></span> 
   
    ![Azure AD Connect의 정의][12]

8. <span data-ttu-id="57531-171">왼쪽 탐색 창에서 **SAML 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Azure AD Connect의 정의][13]

9. <span data-ttu-id="57531-173">**SAML 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Azure AD Connect의 정의][14]

     <span data-ttu-id="57531-175">a.</span><span class="sxs-lookup"><span data-stu-id="57531-175">a.</span></span> <span data-ttu-id="57531-176">**고유 식별자**로 **NameID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="57531-177">b.</span><span class="sxs-lookup"><span data-stu-id="57531-177">b.</span></span> <span data-ttu-id="57531-178">**고유 식별자 매핑 대상**으로 **Username**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="57531-179">c.</span><span class="sxs-lookup"><span data-stu-id="57531-179">c.</span></span> <span data-ttu-id="57531-180">다운로드한 메타데이터 파일을 업로드하려면 **찾아보기**를 클릭하여 파일을 선택하고 **파일 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="57531-181">d.</span><span class="sxs-lookup"><span data-stu-id="57531-181">d.</span></span> <span data-ttu-id="57531-182">구성을 테스트하려면 **테스트 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="57531-183">"*SAML 테스트가 완료되었습니다. 이 창을 닫으십시오.*" 메시지가 표시될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="57531-184">그런 다음 열려 있는 브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-184">Then, close the opened browser window.</span></span> <span data-ttu-id="57531-185">**SAML 사용** 확인란은 테스트가 완료된 경우에만 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="57531-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="57531-186">e.</span><span class="sxs-lookup"><span data-stu-id="57531-186">e.</span></span> <span data-ttu-id="57531-187">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="57531-188">f.</span><span class="sxs-lookup"><span data-stu-id="57531-188">f.</span></span> <span data-ttu-id="57531-189">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="57531-190">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57531-191">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57531-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57531-192">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57531-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="57531-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="57531-194">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57531-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="57531-196">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="57531-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57531-197">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57531-199">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57531-201">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57531-203">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57531-205">a.</span><span class="sxs-lookup"><span data-stu-id="57531-205">a.</span></span> <span data-ttu-id="57531-206">**이름** 텍스트 상자에 이름을 **BrittaSimon**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="57531-207">b.</span><span class="sxs-lookup"><span data-stu-id="57531-207">b.</span></span> <span data-ttu-id="57531-208">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57531-209">c.</span><span class="sxs-lookup"><span data-stu-id="57531-209">c.</span></span> <span data-ttu-id="57531-210">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="57531-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57531-211">d.</span><span class="sxs-lookup"><span data-stu-id="57531-211">d.</span></span> <span data-ttu-id="57531-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="57531-213">Halogen Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="57531-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="57531-214">이 섹션의 목적은 Halogen Software에서 Britta Simon이라는 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57531-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="57531-215">**Halogen Software에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="57531-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="57531-216">**Halogen Software** 응용 프로그램에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="57531-217">**사용자 센터** 탭을 클릭한 후 **사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Azure AD Connect의 정의][300]  

3. <span data-ttu-id="57531-219">**새 사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Connect의 정의][301]

    <span data-ttu-id="57531-221">a.</span><span class="sxs-lookup"><span data-stu-id="57531-221">a.</span></span> <span data-ttu-id="57531-222">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="57531-223">b.</span><span class="sxs-lookup"><span data-stu-id="57531-223">b.</span></span> <span data-ttu-id="57531-224">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="57531-225">c.</span><span class="sxs-lookup"><span data-stu-id="57531-225">c.</span></span> <span data-ttu-id="57531-226">**사용자 이름** 텍스트 상자에 Azure Portal 사용자 이름으로 **Brita Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="57531-227">d.</span><span class="sxs-lookup"><span data-stu-id="57531-227">d.</span></span> <span data-ttu-id="57531-228">**암호** 텍스트 상자에 Britta에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="57531-229">e.</span><span class="sxs-lookup"><span data-stu-id="57531-229">e.</span></span> <span data-ttu-id="57531-230">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57531-231">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="57531-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57531-232">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Halogen Software에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![사용자 할당][200] 

<span data-ttu-id="57531-234">**Britta Simon을 Halogen Software에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="57531-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="57531-235">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="57531-237">응용 프로그램 목록에서 **Halogen Software**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-237">In the applications list, select **Halogen Software**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="57531-239">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-239">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="57531-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-241">Click **Add** button.</span></span> <span data-ttu-id="57531-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="57531-244">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57531-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57531-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57531-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="57531-247">Testing single sign-on</span></span>

<span data-ttu-id="57531-248">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57531-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="57531-249">액세스 패널에서 Halogen Software 타일을 클릭하면 Halogen Software 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="57531-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57531-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="57531-250">Additional resources</span></span>

* [<span data-ttu-id="57531-251">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="57531-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57531-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="57531-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
