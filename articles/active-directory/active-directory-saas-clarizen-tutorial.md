---
title: "자습서: Clarizen과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Clarizen 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="d3bac-103">자습서: Clarizen과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d3bac-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="d3bac-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Clarizen을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="d3bac-105">이 통합은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="d3bac-106">Clarizen에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="d3bac-107">사용자가 해당 Azure AD 계정으로 Clarizen에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d3bac-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="d3bac-109">이 자습서의 시나리오는 다음 두 가지 주요 작업으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="d3bac-110">갤러리에서 Clarizen을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="d3bac-111">Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="d3bac-112">Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bac-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3bac-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d3bac-113">Prerequisites</span></span>
<span data-ttu-id="d3bac-114">Clarizen과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="d3bac-115">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d3bac-115">An Azure AD subscription</span></span>
- <span data-ttu-id="d3bac-116">Single Sign-On이 활성화된 Clarizen 구독</span><span class="sxs-lookup"><span data-stu-id="d3bac-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="d3bac-117">이 자습서의 단계를 테스트하려면 다음 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d3bac-118">테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3bac-119">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d3bac-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d3bac-120">Azure AD 테스트 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="d3bac-121">갤러리에서 Clarizen 추가</span><span class="sxs-lookup"><span data-stu-id="d3bac-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="d3bac-122">Clarizen의 Azure AD 통합을 구성하려면 갤러리의 Clarizen을 관리되는 SaaS 앱 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="d3bac-123">[Azure Portal](https://portal.azure.com)의 왼쪽 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 아이콘][1]

2. <span data-ttu-id="d3bac-125">**엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="d3bac-126">그런 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-126">Then click **All applications**.</span></span>

    ![“엔터프라이즈 응용 프로그램” 및 “모든 응용 프로그램” 클릭][2]

3. <span data-ttu-id="d3bac-128">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![“추가” 단추][3]

4. <span data-ttu-id="d3bac-130">검색 상자에 **Clarizen**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-130">In the search box, type **Clarizen**.</span></span>

    ![검색 상자에 “Clarizen” 입력](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="d3bac-132">결과 창에서 **Clarizen**을 선택하고 **추가**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![결과 창에서 Clarizen 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d3bac-134">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d3bac-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d3bac-135">다음 섹션에서는 테스트 사용자 Britta Simon을 기준으로 Clarizen에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="d3bac-136">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Clarizen 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="d3bac-137">즉, Azure AD 사용자와 Clarizen의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="d3bac-138">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Clarizen의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="d3bac-139">Clarizen에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="d3bac-140">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3bac-141">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3bac-142">**[Clarizen 테스트 사용자 만들기](#create-a-clarizen-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Clarizen에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d3bac-143">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3bac-144">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d3bac-145">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d3bac-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="d3bac-146">Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Clarizen 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="d3bac-147">Azure Portal의 **Clarizen** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    !["Single sign-on" 클릭][4]

2. <span data-ttu-id="d3bac-149">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    !["SAML 기반 로그온" 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="d3bac-151">**Clarizen 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![식별자 및 회신 URL 상자](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="d3bac-153">a.</span><span class="sxs-lookup"><span data-stu-id="d3bac-153">a.</span></span> <span data-ttu-id="d3bac-154">**식별자** 상자에 해당 값으로 **Clarizen**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="d3bac-155">b.</span><span class="sxs-lookup"><span data-stu-id="d3bac-155">b.</span></span> <span data-ttu-id="d3bac-156">**회신 URL** 상자에 **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx** 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3bac-157">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-157">These are not the real values.</span></span> <span data-ttu-id="d3bac-158">실제 식별자 및 회신 URL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="d3bac-159">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="d3bac-160">실제 값을 확인하려면 [Clarizen 지원 팀](https://success.clarizen.com/hc/en-us/requests/new)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d3bac-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="d3bac-161">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    !["새 인증서 만들기" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="d3bac-163">**새 인증서 만들기** 대화 상자에서 달력 아이콘을 클릭하고 만료 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="d3bac-164">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-164">Then click **Save**.</span></span>

    ![만료 날짜 선택 및 저장](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="d3bac-166">**SAML 서명 인증서** 섹션에서 **새 인증서 활성화**를 선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![새 인증서를 활성화하기 위한 확인란 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="d3bac-168">**롤오버 인증서** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    !["확인"을 클릭하여 인증서를 활성화할지 확인](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d3bac-170">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    !["인증서(Base64)"를 클릭하여 다운로드 시작](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="d3bac-172">**Clarizen 구성** 섹션에서 **Clarizen 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    !["Clarizen 구성" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![파일 및 URL을 포함하는 "로그온 구성" 창](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="d3bac-175">다른 웹 브라우저 창에서 Clarizen 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="d3bac-176">사용자 이름을 클릭한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="d3bac-177">![사용자 이름 아래에서 "설정" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "설정")</span><span class="sxs-lookup"><span data-stu-id="d3bac-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="d3bac-178">**전역 설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="d3bac-179">그런 다음 **페더레이션 인증** 옆에 있는 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="d3bac-180">![“전역 설정” 탭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "전역 설정")</span><span class="sxs-lookup"><span data-stu-id="d3bac-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="d3bac-181">**페더레이션 인증** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="d3bac-182">![“페더레이션 인증” 대화 상자](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "페더레이션 인증")</span><span class="sxs-lookup"><span data-stu-id="d3bac-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="d3bac-183">a.</span><span class="sxs-lookup"><span data-stu-id="d3bac-183">a.</span></span> <span data-ttu-id="d3bac-184">**페더레이션 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="d3bac-185">b.</span><span class="sxs-lookup"><span data-stu-id="d3bac-185">b.</span></span> <span data-ttu-id="d3bac-186">다운로드한 인증서를 업로드하려면 **업로드** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="d3bac-187">c.</span><span class="sxs-lookup"><span data-stu-id="d3bac-187">c.</span></span> <span data-ttu-id="d3bac-188">**로그인 URL** 상자에 Azure AD 응용 프로그램 구성 창의 **SAML Single Sign-on 서비스 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="d3bac-189">d.</span><span class="sxs-lookup"><span data-stu-id="d3bac-189">d.</span></span> <span data-ttu-id="d3bac-190">**로그아웃 URL** 상자에 Azure AD 응용 프로그램 구성 창의 **로그아웃 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="d3bac-191">e.</span><span class="sxs-lookup"><span data-stu-id="d3bac-191">e.</span></span> <span data-ttu-id="d3bac-192">**POST 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-192">Select **Use POST**.</span></span>

    <span data-ttu-id="d3bac-193">f.</span><span class="sxs-lookup"><span data-stu-id="d3bac-193">f.</span></span> <span data-ttu-id="d3bac-194">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d3bac-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d3bac-195">Create an Azure AD test user</span></span>
<span data-ttu-id="d3bac-196">Azure Portal에서 Britta Simon이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Azure AD 테스트 사용자의 이름 및 전자 메일 주소][100]

1. <span data-ttu-id="d3bac-198">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 아이콘](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d3bac-200">**사용자 및 그룹**을 클릭하고 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 클릭](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d3bac-202">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![“추가” 단추](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d3bac-204">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-204">In the **User** dialog box, perform the following steps:</span></span>

    ![이름, 전자 메일 주소 및 암호가 입력된 "사용자" 대화 상자](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d3bac-206">a.</span><span class="sxs-lookup"><span data-stu-id="d3bac-206">a.</span></span> <span data-ttu-id="d3bac-207">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3bac-208">b.</span><span class="sxs-lookup"><span data-stu-id="d3bac-208">b.</span></span> <span data-ttu-id="d3bac-209">**사용자 이름** 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="d3bac-210">c.</span><span class="sxs-lookup"><span data-stu-id="d3bac-210">c.</span></span> <span data-ttu-id="d3bac-211">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="d3bac-212">d.</span><span class="sxs-lookup"><span data-stu-id="d3bac-212">d.</span></span> <span data-ttu-id="d3bac-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="d3bac-214">Clarizen 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d3bac-214">Create a Clarizen test user</span></span>
<span data-ttu-id="d3bac-215">Azure AD 사용자가 Clarizen에 로그인할 수 있도록 하려면 사용자 계정을 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="d3bac-216">Clarizen의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="d3bac-217">Clarizen 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="d3bac-218">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-218">Click **People**.</span></span>

    <span data-ttu-id="d3bac-219">!["피플" 클릭](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "피플")</span><span class="sxs-lookup"><span data-stu-id="d3bac-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="d3bac-220">**사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-220">Click **Invite User**.</span></span>

    <span data-ttu-id="d3bac-221">!["사용자 초대" 단추](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "사용자 초대")</span><span class="sxs-lookup"><span data-stu-id="d3bac-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="d3bac-222">**피플 초대** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="d3bac-223">!["피플 초대" 대화 상자](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="d3bac-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="d3bac-224">a.</span><span class="sxs-lookup"><span data-stu-id="d3bac-224">a.</span></span> <span data-ttu-id="d3bac-225">**전자 메일** 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="d3bac-226">b.</span><span class="sxs-lookup"><span data-stu-id="d3bac-226">b.</span></span> <span data-ttu-id="d3bac-227">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3bac-228">Azure Active Directory 계정 보유자는 활성화되기 전에 전자 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d3bac-229">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d3bac-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="d3bac-230">Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Clarizen에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![할당된 테스트 사용자][200]

1. <span data-ttu-id="d3bac-232">Azure Portal에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동한 후 **엔터프라이즈 응용 프로그램**을 클릭하고 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![“엔터프라이즈 응용 프로그램” 및 “모든 응용 프로그램” 클릭][201]

2. <span data-ttu-id="d3bac-234">응용 프로그램 목록에서 **Clarizen**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-234">In the applications list, select **Clarizen**.</span></span>

    ![목록에서 Clarizen 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="d3bac-236">왼쪽 창에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-236">In the left pane, click **Users and groups**.</span></span>

    ![“사용자 및 그룹” 클릭][202]

4. <span data-ttu-id="d3bac-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-238">Click the **Add** button.</span></span> <span data-ttu-id="d3bac-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    !["추가" 단추 및 "할당 추가" 대화 상자][203]

5. <span data-ttu-id="d3bac-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="d3bac-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="d3bac-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="d3bac-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d3bac-244">Test single sign-on</span></span>
<span data-ttu-id="d3bac-245">액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="d3bac-246">액세스 패널에서 Clarizen 타일을 클릭하면 Clarizen 응용 프로그램에 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3bac-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3bac-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d3bac-247">Additional resources</span></span>

* [<span data-ttu-id="d3bac-248">Azure Active Directory를 사용하여 SaaS 앱을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d3bac-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3bac-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d3bac-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
