---
title: "자습서: LogicMonitor와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 LogicMonitor 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="a7f19-103">자습서: LogicMonitor와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a7f19-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="a7f19-104">이 자습서에서는 Azure AD(Azure Active Directory)와 LogicMonitor를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7f19-105">LogicMonitor를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7f19-106">LogicMonitor에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="a7f19-107">사용자가 해당 Azure AD 계정으로 LogicMonitor에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7f19-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7f19-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7f19-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7f19-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a7f19-110">Prerequisites</span></span>

<span data-ttu-id="a7f19-111">LogicMonitor와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="a7f19-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a7f19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7f19-113">LogicMonitor Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a7f19-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7f19-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7f19-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7f19-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a7f19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7f19-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7f19-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a7f19-118">Scenario description</span></span>
<span data-ttu-id="a7f19-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7f19-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7f19-121">갤러리에서 LogicMonitor 추가</span><span class="sxs-lookup"><span data-stu-id="a7f19-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="a7f19-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a7f19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="a7f19-123">갤러리에서 LogicMonitor 추가</span><span class="sxs-lookup"><span data-stu-id="a7f19-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="a7f19-124">LogicMonitor의 Azure AD 통합을 구성하려면 갤러리의 LogicMonitor를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7f19-125">**갤러리에서 LogicMonitor를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7f19-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7f19-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7f19-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7f19-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a7f19-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a7f19-133">검색 상자에 **LogicMonitor**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-133">In the search box, type **LogicMonitor**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="a7f19-135">결과 패널에서 **LogicMonitor**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7f19-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a7f19-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7f19-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 LogicMonitor에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7f19-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 LogicMonitor 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="a7f19-140">즉, Azure AD 사용자와 LogicMonitor의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="a7f19-141">LogicMonitor에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7f19-142">LogicMonitor에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7f19-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7f19-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7f19-145">**[LogicMonitor 테스트 사용자 만들기](#creating-a-logicmonitor-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 LogicMonitor에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7f19-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7f19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7f19-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a7f19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7f19-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LogicMonitor 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="a7f19-150">**LogicMonitor에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7f19-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="a7f19-151">Azure Portal의 **LogicMonitor** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a7f19-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="a7f19-155">**LogicMonitor 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="a7f19-157">a.</span><span class="sxs-lookup"><span data-stu-id="a7f19-157">a.</span></span> <span data-ttu-id="a7f19-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="a7f19-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="a7f19-159">b.</span><span class="sxs-lookup"><span data-stu-id="a7f19-159">b.</span></span> <span data-ttu-id="a7f19-160">**식별자** 텍스트 상자에서 `https://<companyname>.logicmonitor.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7f19-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-161">These values are not real.</span></span> <span data-ttu-id="a7f19-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a7f19-163">이러한 값을 얻으려면 [LogicMonitor 클라이언트 지원 팀](https://www.logicmonitor.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a7f19-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="a7f19-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="a7f19-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7f19-168">**LogicMonitor** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="a7f19-169">위쪽의 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="a7f19-170">![설정](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "설정")</span><span class="sxs-lookup"><span data-stu-id="a7f19-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="a7f19-171">왼쪽의 탐색 모음에서 **Single Sign-On**</span><span class="sxs-lookup"><span data-stu-id="a7f19-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="a7f19-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a7f19-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="a7f19-173">**SSO(Single Sign-On) 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a7f19-174">![Single Sign-On 설정](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="a7f19-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="a7f19-175">a.</span><span class="sxs-lookup"><span data-stu-id="a7f19-175">a.</span></span> <span data-ttu-id="a7f19-176">**Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="a7f19-177">b.</span><span class="sxs-lookup"><span data-stu-id="a7f19-177">b.</span></span> <span data-ttu-id="a7f19-178">**기본 역할 할당**으로 **readonly**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="a7f19-179">c.</span><span class="sxs-lookup"><span data-stu-id="a7f19-179">c.</span></span> <span data-ttu-id="a7f19-180">다운로드한 메타데이터 파일을 메모장에서 열고 파일 내용을 **ID 공급자 메타데이터** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="a7f19-181">d.</span><span class="sxs-lookup"><span data-stu-id="a7f19-181">d.</span></span> <span data-ttu-id="a7f19-182">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a7f19-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7f19-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7f19-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7f19-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a7f19-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7f19-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a7f19-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a7f19-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7f19-190">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7f19-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7f19-194">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7f19-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7f19-198">a.</span><span class="sxs-lookup"><span data-stu-id="a7f19-198">a.</span></span> <span data-ttu-id="a7f19-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7f19-200">b.</span><span class="sxs-lookup"><span data-stu-id="a7f19-200">b.</span></span> <span data-ttu-id="a7f19-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7f19-202">c.</span><span class="sxs-lookup"><span data-stu-id="a7f19-202">c.</span></span> <span data-ttu-id="a7f19-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7f19-204">d.</span><span class="sxs-lookup"><span data-stu-id="a7f19-204">d.</span></span> <span data-ttu-id="a7f19-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="a7f19-206">LogicMonitor 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a7f19-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="a7f19-207">AAD 사용자가 로그인 할 수 있도록 Azure Active Directory 사용자 이름을 사용하여 LogicMonitor 응용 프로그램에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="a7f19-208">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7f19-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a7f19-209">LogicMonitor 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="a7f19-210">위쪽 메뉴에서 **설정**을 클릭한 다음 **역할 및 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="a7f19-211">![역할 및 사용자](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "역할 및 사용자")</span><span class="sxs-lookup"><span data-stu-id="a7f19-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="a7f19-212">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-212">Click **Add**.</span></span>

4. <span data-ttu-id="a7f19-213">**계정 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a7f19-214">![계정 추가](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "계정 추가")</span><span class="sxs-lookup"><span data-stu-id="a7f19-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="a7f19-215">a.</span><span class="sxs-lookup"><span data-stu-id="a7f19-215">a.</span></span> <span data-ttu-id="a7f19-216">프로비전할 Azure Active Directory 사용자의 **이름**, **전자 메일**, **암호** 및 **암호 확인** 값을 관련된 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="a7f19-217">b.</span><span class="sxs-lookup"><span data-stu-id="a7f19-217">b.</span></span> <span data-ttu-id="a7f19-218">**역할**, **보기 권한** 및 **상태**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="a7f19-219">c.</span><span class="sxs-lookup"><span data-stu-id="a7f19-219">c.</span></span> <span data-ttu-id="a7f19-220">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="a7f19-221">LogicMonitor에서 제공하는 다른 LogicMonitor 사용자 계정 만들기 도구 또는 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7f19-222">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a7f19-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7f19-223">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LogicMonitor에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a7f19-225">**Britta Simon을 LogicMonitor에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a7f19-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="a7f19-226">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a7f19-228">응용 프로그램 목록에서 **LogicMonitor**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="a7f19-230">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-230">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a7f19-232">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-232">Click **Add** button.</span></span> <span data-ttu-id="a7f19-233">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a7f19-235">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7f19-236">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7f19-237">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7f19-238">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a7f19-238">Testing single sign-on</span></span>

<span data-ttu-id="a7f19-239">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="a7f19-240">액세스 패널에서 LogicMonitor 타일을 클릭하면 LogicMonitor 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f19-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="a7f19-241">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7f19-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7f19-242">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a7f19-242">Additional resources</span></span>

* [<span data-ttu-id="a7f19-243">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a7f19-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7f19-244">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a7f19-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

