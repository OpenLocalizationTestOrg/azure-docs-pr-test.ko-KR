---
title: "자습서: RFPIO와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 RFPIO 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="5ae04-103">자습서: RFPIO와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5ae04-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="5ae04-104">이 자습서에서는 Azure AD(Azure Active Directory)와 RFPIO를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ae04-105">RFPIO를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ae04-106">RFPIO에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="5ae04-107">사용자가 해당 Azure AD 계정으로 RFPIO를에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5ae04-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="5ae04-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ae04-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ae04-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5ae04-110">Prerequisites</span></span>

<span data-ttu-id="5ae04-111">RFPIO와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="5ae04-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5ae04-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="5ae04-113">RFPIO Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5ae04-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5ae04-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="5ae04-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="5ae04-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5ae04-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="5ae04-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ae04-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5ae04-118">Scenario description</span></span>
<span data-ttu-id="5ae04-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ae04-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ae04-121">갤러리에서 RFPIO 추가</span><span class="sxs-lookup"><span data-stu-id="5ae04-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="5ae04-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5ae04-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="5ae04-123">갤러리에서 RFPIO 추가</span><span class="sxs-lookup"><span data-stu-id="5ae04-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="5ae04-124">RFPIO의 Azure AD 통합을 구성하려면 갤러리의 RFPIO를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="5ae04-125">갤러리에서 RFPIO를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="5ae04-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="5ae04-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ae04-128">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5ae04-130">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5ae04-132">검색 상자에 **RFPIO**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-132">In the search box, type **RFPIO**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="5ae04-134">결과 패널에서 **RFPIO**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5ae04-136">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5ae04-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5ae04-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 RFPIO에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ae04-138">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 RFPIO 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="5ae04-139">즉, Azure AD 사용자와 RFPIO의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="5ae04-140">RFPIO에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5ae04-141">RFPIO에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ae04-142">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ae04-143">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ae04-144">**[RFPIO 테스트 사용자 만들기](#creating-a-rfpio-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 RFPIO에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ae04-145">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ae04-146">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5ae04-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5ae04-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5ae04-148">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 RFPIO 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="5ae04-149">**RFPIO에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ae04-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae04-150">Azure Portal의 **RFPIO** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5ae04-152">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="5ae04-154">**RFPIO 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="5ae04-156">a.</span><span class="sxs-lookup"><span data-stu-id="5ae04-156">a.</span></span> <span data-ttu-id="5ae04-157">**식별자** 텍스트 상자에 URL `https://www.rfpio.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="5ae04-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ae04-159">b.</span></span> <span data-ttu-id="5ae04-160">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="5ae04-161">c.</span><span class="sxs-lookup"><span data-stu-id="5ae04-161">c.</span></span> <span data-ttu-id="5ae04-162">**릴레이 상태** 텍스트 상자에 문자열 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="5ae04-163">이 값을 얻으려면 [RFPIO 지원 팀](https://www.rfpio.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5ae04-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="5ae04-164">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="5ae04-165">**SP** 시작 모드에서 응용 프로그램을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="5ae04-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="5ae04-167">**로그온 URL** 텍스트 상자에 URL `https://www.app.rfpio.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="5ae04-168">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="5ae04-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5ae04-172">다른 웹 브라우저 창에서 **RFPIO** 웹 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="5ae04-173">왼쪽 아래 모서리 드롭다운을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-173">Click on the bottom left corner dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="5ae04-175">**조직 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-175">Click on the **Organization Settings**.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="5ae04-177">**기능 및 통합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="5ae04-179">**SAML SSO 구성**에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="5ae04-181">이 섹션에서 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-181">In this Section perform following actions:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="5ae04-183">a.</span><span class="sxs-lookup"><span data-stu-id="5ae04-183">a.</span></span> <span data-ttu-id="5ae04-184">**다운로드한 메타데이터 XML**의 내용을 복사하여 **ID 구성** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="5ae04-185">다운로드한 **메타데이터 XML**의 내용을 복사하려면 **메모장++** 또는 적절한 **XML 편집기**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="5ae04-186">b.</span><span class="sxs-lookup"><span data-stu-id="5ae04-186">b.</span></span> <span data-ttu-id="5ae04-187">**유효성 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-187">Click **Validate**.</span></span>

    <span data-ttu-id="5ae04-188">c.</span><span class="sxs-lookup"><span data-stu-id="5ae04-188">c.</span></span> <span data-ttu-id="5ae04-189">**유효성 검사**를 클릭한 후 **SAML(Enabled)**(SAML(사용))을 설정으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="5ae04-190">d.</span><span class="sxs-lookup"><span data-stu-id="5ae04-190">d.</span></span> <span data-ttu-id="5ae04-191">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="5ae04-192">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5ae04-193">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5ae04-194">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5ae04-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5ae04-195">Create an Azure AD test user</span></span>
<span data-ttu-id="5ae04-196">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5ae04-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5ae04-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae04-199">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ae04-201">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ae04-203">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ae04-205">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ae04-207">a.</span><span class="sxs-lookup"><span data-stu-id="5ae04-207">a.</span></span> <span data-ttu-id="5ae04-208">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ae04-209">b.</span><span class="sxs-lookup"><span data-stu-id="5ae04-209">b.</span></span> <span data-ttu-id="5ae04-210">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ae04-211">c.</span><span class="sxs-lookup"><span data-stu-id="5ae04-211">c.</span></span> <span data-ttu-id="5ae04-212">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ae04-213">d.</span><span class="sxs-lookup"><span data-stu-id="5ae04-213">d.</span></span> <span data-ttu-id="5ae04-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="5ae04-215">RFPIO 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5ae04-215">Create a RFPIO test user</span></span>

<span data-ttu-id="5ae04-216">Azure AD 사용자가 RFPIO에 로그인할 수 있도록 하려면 RFPIO로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="5ae04-217">RFPIO의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="5ae04-218">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ae04-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae04-219">RFPIO 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="5ae04-220">왼쪽 아래 모서리 드롭다운을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-220">Click on the bottom left corner dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="5ae04-222">**조직 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-222">Click on the **Organization Settings**.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="5ae04-224">**TEAM MEMBERS**(팀 멤버)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-224">Click **TEAM MEMBERS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="5ae04-226">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-226">Click on **ADD MEMBERS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="5ae04-228">**새 멤버 추가** 섹션에서</span><span class="sxs-lookup"><span data-stu-id="5ae04-228">In the **Add New Members** section.</span></span> <span data-ttu-id="5ae04-229">다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-229">Perform following actions:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="5ae04-231">a.</span><span class="sxs-lookup"><span data-stu-id="5ae04-231">a.</span></span> <span data-ttu-id="5ae04-232">**Enter one email per line**(줄당 하나의 메일 입력) 필드에 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="5ae04-233">b.</span><span class="sxs-lookup"><span data-stu-id="5ae04-233">b.</span></span> <span data-ttu-id="5ae04-234">요구 사항에 따라 **역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="5ae04-235">c.</span><span class="sxs-lookup"><span data-stu-id="5ae04-235">c.</span></span> <span data-ttu-id="5ae04-236">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="5ae04-237">Azure Active Directory 계정 보유자는 활성화되기 전에 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5ae04-238">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5ae04-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="5ae04-239">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 RFPIO에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5ae04-241">**Britta Simon을 RFPIO에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5ae04-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae04-242">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5ae04-244">응용 프로그램 목록에서 **RFPIO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-244">In the applications list, select **RFPIO**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="5ae04-246">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-246">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5ae04-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-248">Click **Add** button.</span></span> <span data-ttu-id="5ae04-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5ae04-251">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ae04-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ae04-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5ae04-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5ae04-254">Test single sign-on</span></span>

<span data-ttu-id="5ae04-255">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="5ae04-256">액세스 패널에서 RFPIO 타일을 클릭하면 RFPIO 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ae04-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="5ae04-257">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ae04-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ae04-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5ae04-258">Additional resources</span></span>

* [<span data-ttu-id="5ae04-259">Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5ae04-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ae04-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5ae04-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

