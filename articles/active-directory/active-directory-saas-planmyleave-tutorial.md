---
title: "자습서: PlanMyLeave와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 PlanMyLeave 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="22c26-103">자습서: PlanMyLeave와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="22c26-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="22c26-104">이 자습서에서는 Azure AD(Azure Active Directory)와 PlanMyLeave를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22c26-105">PlanMyLeave를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="22c26-106">PlanMyLeave에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="22c26-107">사용자가 해당 Azure AD 계정으로 PlanMyLeave에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22c26-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="22c26-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22c26-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22c26-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="22c26-110">Prerequisites</span></span>

<span data-ttu-id="22c26-111">PlanMyLeave와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="22c26-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="22c26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22c26-113">PlanMyLeave Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="22c26-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="22c26-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="22c26-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22c26-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="22c26-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="22c26-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="22c26-118">Scenario description</span></span>
<span data-ttu-id="22c26-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22c26-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22c26-121">갤러리에서 PlanMyLeave 추가</span><span class="sxs-lookup"><span data-stu-id="22c26-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="22c26-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="22c26-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="22c26-123">갤러리에서 PlanMyLeave 추가</span><span class="sxs-lookup"><span data-stu-id="22c26-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="22c26-124">PlanMyLeave의 Azure AD 통합을 구성하려면 갤러리의 PlanMyLeave를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="22c26-125">**갤러리에서 PlanMyLeave를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22c26-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="22c26-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22c26-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="22c26-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="22c26-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="22c26-133">검색 상자에서 **PlanMyLeave**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="22c26-135">결과 창에서 **PlanMyLeave**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22c26-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="22c26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22c26-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 PlanMyLeave에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22c26-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 PlanMyLeave 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="22c26-140">즉, Azure AD 사용자와 PlanMyLeave의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="22c26-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 PlanMyLeave의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="22c26-142">PlanMyLeave에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="22c26-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="22c26-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22c26-145">**[PlanMyLeave 테스트 사용자 만들기](#creating-a-planmyleave-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 PlanMyLeave에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="22c26-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22c26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22c26-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="22c26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22c26-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 PlanMyLeave 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="22c26-150">**PlanMyLeave에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22c26-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="22c26-151">Azure 관리 포털의 **PlanMyLeave** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성][4]

2. <span data-ttu-id="22c26-153">**Single sign on** 대화 상자 페이지에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="22c26-155">**PlanMyLeave 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="22c26-157">a.</span><span class="sxs-lookup"><span data-stu-id="22c26-157">a.</span></span> <span data-ttu-id="22c26-158">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://<company-name>.planmyleave.com/Login.aspx`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="22c26-159">b.</span><span class="sxs-lookup"><span data-stu-id="22c26-159">b.</span></span> <span data-ttu-id="22c26-160">**식별자** 텍스트 상자에 `https://<company-name>.planmyleave.com` 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="22c26-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-161">Please note that these are not the real values.</span></span> <span data-ttu-id="22c26-162">실제 로그온 URL 및 식별자로 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="22c26-163">이러한 값을 얻으려면 [PlanMyLeave 지원 팀](mailto:support@planmyleave.com)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="22c26-164">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="22c26-166">**새 인증서 만들기** 대화 상자에서 달력 아이콘을 클릭하고 **만료 날짜**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="22c26-167">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-167">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="22c26-169">**SAML 서명 인증서** 섹션에서 **새 인증서 활성화**를 선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="22c26-171">팝업 **롤오버 인증서** 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="22c26-173">**SAML 서명 인증서** 섹션에서 **인증서(base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="22c26-175">**PlanMyLeave 구성** 섹션에서 **PlanMyLeave 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="22c26-178">다른 웹 브라우저 창에서 PlanMyLeave 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="22c26-179">**시스템 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-179">Go to **System Setup**.</span></span> <span data-ttu-id="22c26-180">그런 다음 **보안 관리** 섹션에서 **회사 SAML 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="22c26-182">**SAML 설정** 섹션에서 편집기 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="22c26-184">**SAML 설정 업데이트** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="22c26-186">a.</span><span class="sxs-lookup"><span data-stu-id="22c26-186">a.</span></span>  <span data-ttu-id="22c26-187">**로그인 URL** 텍스트 상자에 Azure AD 응용 프로그램 구성 창의 **SAML Single Sign-on 서비스 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="22c26-188">b.</span><span class="sxs-lookup"><span data-stu-id="22c26-188">b.</span></span>  <span data-ttu-id="22c26-189">다운로드된 인증서 파일을 메모장에서 열고, ---Begin Certificate--- 및 ---End certificate---- 사이의 내용을 클립보드에 복사한 다음 전체 인증서를 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="22c26-190">c.</span><span class="sxs-lookup"><span data-stu-id="22c26-190">c.</span></span> <span data-ttu-id="22c26-191">"**Is Enable(사용 여부)**"을 "**예**"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="22c26-192">d.</span><span class="sxs-lookup"><span data-stu-id="22c26-192">d.</span></span> <span data-ttu-id="22c26-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22c26-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="22c26-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="22c26-195">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="22c26-197">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="22c26-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="22c26-198">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22c26-200">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22c26-202">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22c26-204">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22c26-206">a.</span><span class="sxs-lookup"><span data-stu-id="22c26-206">a.</span></span> <span data-ttu-id="22c26-207">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22c26-208">b.</span><span class="sxs-lookup"><span data-stu-id="22c26-208">b.</span></span> <span data-ttu-id="22c26-209">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22c26-210">c.</span><span class="sxs-lookup"><span data-stu-id="22c26-210">c.</span></span> <span data-ttu-id="22c26-211">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="22c26-212">d.</span><span class="sxs-lookup"><span data-stu-id="22c26-212">d.</span></span> <span data-ttu-id="22c26-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="22c26-214">PlanMyLeave 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="22c26-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="22c26-215">이 섹션은 PlanMyLeave에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="22c26-216">PlanMyLeave는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="22c26-217">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-217">There is no action item for you in this section.</span></span> <span data-ttu-id="22c26-218">새 사용자가 아직 존재하지 않는 경우 PlanMyLeave에 액세스하는 동안 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="22c26-219">사용자를 수동으로 만들어야 하는 경우 [PlanMyLeave 지원 팀](mailto:support@planmyleave.com)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="22c26-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="22c26-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="22c26-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 PlanMyLeave에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![사용자 할당][200] 

<span data-ttu-id="22c26-223">**Britta Simon을 PlanMyLeave에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="22c26-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="22c26-224">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="22c26-226">응용 프로그램 목록에서 **PlanMyLeave**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="22c26-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-228">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="22c26-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-230">Click **Add** button.</span></span> <span data-ttu-id="22c26-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="22c26-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="22c26-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22c26-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="22c26-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="22c26-236">Testing single sign-on</span></span>

<span data-ttu-id="22c26-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="22c26-238">액세스 패널에서 PlanMyLeave 타일을 클릭하면 PlanMyLeave 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c26-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="22c26-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="22c26-239">Additional resources</span></span>

* [<span data-ttu-id="22c26-240">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="22c26-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22c26-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="22c26-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png