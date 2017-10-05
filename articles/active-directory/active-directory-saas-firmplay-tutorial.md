---
title: "자습서: FirmPlay - Employee Advocacy for Recruiting과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 FirmPlay - Employee Advocacy for Recruiting 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="c6ecf-103">자습서: FirmPlay - Employee Advocacy for Recruiting과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c6ecf-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="c6ecf-104">이 자습서에서는 Azure AD(Azure Active Directory)와 FirmPlay - Employee Advocacy for Recruiting을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6ecf-105">FirmPlay - Employee Advocacy for Recruiting을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c6ecf-106">FirmPlay - Employee Advocacy for Recruiting에 대한 액세스 권한이 있는 사용자는 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="c6ecf-107">사용자가 해당 Azure AD 계정으로 FirmPlay - Employee Advocacy for Recruiting에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6ecf-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="c6ecf-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6ecf-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c6ecf-110">Prerequisites</span></span>

<span data-ttu-id="c6ecf-111">FirmPlay - Employee Advocacy for Recruiting과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="c6ecf-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c6ecf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6ecf-113">FirmPlay - Employee Advocacy for Recruiting Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c6ecf-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="c6ecf-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c6ecf-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6ecf-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c6ecf-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c6ecf-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c6ecf-118">Scenario description</span></span>
<span data-ttu-id="c6ecf-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6ecf-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6ecf-121">갤러리에서 FirmPlay - Employee Advocacy for Recruiting 추가</span><span class="sxs-lookup"><span data-stu-id="c6ecf-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="c6ecf-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c6ecf-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="c6ecf-123">갤러리에서 FirmPlay - Employee Advocacy for Recruiting 추가</span><span class="sxs-lookup"><span data-stu-id="c6ecf-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="c6ecf-124">Azure AD와 FirmPlay - Employee Advocacy for Recruiting이 통합되도록 구성하려면 갤러리에서 FirmPlay - Employee Advocacy for Recruiting을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c6ecf-125">**갤러리에서 FirmPlay - Employee Advocacy for Recruiting을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ecf-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6ecf-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c6ecf-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c6ecf-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c6ecf-133">검색 상자에 **FirmPlay - Employee Advocacy for Recruiting**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="c6ecf-135">결과 창에서 **FirmPlay - Employee Advocacy for Recruiting**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6ecf-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c6ecf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6ecf-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FirmPlay - Employee Advocacy for Recruiting에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6ecf-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 FirmPlay - Employee Advocacy for Recruiting 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="c6ecf-140">즉, Azure AD 사용자와 FirmPlay - Employee Advocacy for Recruiting의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="c6ecf-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 FirmPlay - Employee Advocacy for Recruiting의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="c6ecf-142">FirmPlay - Employee Advocacy for Recruiting에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c6ecf-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c6ecf-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6ecf-145">**[FirmPlay - Employee Advocacy for Recruiting 테스트 사용자 만들기](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  - FirmPlay: Employee Advocacy for Recruiting에서 Azure AD 담당자와 연결된 Britta Simon에 해당하는 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c6ecf-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6ecf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6ecf-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c6ecf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6ecf-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 FirmPlay - Employee Advocacy for Recruiting 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="c6ecf-150">**FirmPlay - Employee Advocacy for Recruiting에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ecf-151">Azure 관리 포털의 **FirmPlay - Employee Advocacy for Recruiting** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c6ecf-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="c6ecf-155">**FirmPlay - Employee Advocacy for Recruiting 도메인 및 URL** 섹션에서 **로그인 URL** 텍스트 상자에 다음 패턴을 사용하여 URL을 입력합니다.`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="c6ecf-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="c6ecf-157">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-157">Please note that this is not the real value.</span></span> <span data-ttu-id="c6ecf-158">이 값은 실제 로그인 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="c6ecf-159">[FirmPlay - Employee Advocacy for Recruiting 지원 팀](mailto:engineering@firmplay.com)에 문의하여 이 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="c6ecf-160">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="c6ecf-162">**새 인증서 만들기** 대화 상자에서 달력 아이콘을 클릭하고 **만료 날짜**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="c6ecf-163">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-163">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="c6ecf-165">**SAML 서명 인증서** 섹션에서 **새 인증서 활성화**를 선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="c6ecf-167">팝업 **롤오버 인증서** 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c6ecf-169">**SAML 서명 인증서** 섹션에서 **인증서(base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Single Sign-On 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="c6ecf-171">**FirmPlay - Employee Advocacy for Recruiting Configuration** 섹션에서 **FirmPlay - Employee Advocacy for Recruiting 구성**을 클릭하여 **로그인 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Single Sign-On 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="c6ecf-174">응용 프로그램에 대해 구성된 SSO를 얻으려면 [FirmPlay - Employee Advocacy for Recruiting 지원 팀](mailto:engineering@firmplay.com)에 문의하고 다음을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="c6ecf-175">•  다운로드한 **인증서 파일**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="c6ecf-176">•  **SAML Single Sign-On 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="c6ecf-177">•  **SAML 엔터티 ID**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="c6ecf-178">•  **로그아웃 URL**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6ecf-179">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ecf-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6ecf-180">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c6ecf-182">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ecf-183">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6ecf-185">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6ecf-187">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6ecf-189">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6ecf-191">a.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-191">a.</span></span> <span data-ttu-id="c6ecf-192">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6ecf-193">b.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-193">b.</span></span> <span data-ttu-id="c6ecf-194">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6ecf-195">c.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-195">c.</span></span> <span data-ttu-id="c6ecf-196">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c6ecf-197">d.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-197">d.</span></span> <span data-ttu-id="c6ecf-198">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="c6ecf-199">FirmPlay - Employee Advocacy for Recruiting 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ecf-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="c6ecf-200">이 섹션에서는 FirmPlay - Employee Advocacy for Recruiting에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="c6ecf-201">[FirmPlay - Employee Advocacy for Recruiting 지원 팀](mailto:engineering@firmplay.com)을 사용하여 FirmPlay - Employee Advocacy for Recruiting 플랫폼에서 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c6ecf-202">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c6ecf-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c6ecf-203">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 FirmPlay - Employee Advocacy for Recruiting에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c6ecf-205">**FirmPlay - Employee Advocacy for Recruiting에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6ecf-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ecf-206">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c6ecf-208">응용 프로그램 목록에서 **FirmPlay - Employee Advocacy for Recruiting**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="c6ecf-210">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-210">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c6ecf-212">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-212">Click **Add** button.</span></span> <span data-ttu-id="c6ecf-213">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c6ecf-215">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c6ecf-216">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6ecf-217">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="c6ecf-218">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c6ecf-218">Testing single sign-on</span></span>

<span data-ttu-id="c6ecf-219">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c6ecf-220">액세스 패널에서 FirmPlay - Employee Advocacy for Recruiting 타일을 클릭하는 경우 FirmPlay - Employee Advocacy for Recruiting 응용 프로그램에 자동으로 로그인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ecf-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c6ecf-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c6ecf-221">Additional resources</span></span>

* [<span data-ttu-id="c6ecf-222">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c6ecf-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6ecf-223">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c6ecf-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png