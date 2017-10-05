---
title: "자습서: TeamSeer와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 TeamSeer 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="c70f3-103">자습서: TeamSeer와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c70f3-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="c70f3-104">이 자습서에서는 Azure AD(Azure Active Directory)와 TeamSeer를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c70f3-105">TeamSeer를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c70f3-106">TeamSeer에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="c70f3-107">사용자가 해당 Azure AD 계정으로 TeamSeer에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c70f3-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c70f3-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c70f3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c70f3-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c70f3-110">Prerequisites</span></span>

<span data-ttu-id="c70f3-111">TeamSeer와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="c70f3-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c70f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c70f3-113">TeamSeer Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c70f3-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c70f3-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c70f3-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c70f3-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c70f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c70f3-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c70f3-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c70f3-118">Scenario description</span></span>
<span data-ttu-id="c70f3-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c70f3-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c70f3-121">갤러리에서 TeamSeer 추가</span><span class="sxs-lookup"><span data-stu-id="c70f3-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="c70f3-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c70f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="c70f3-123">갤러리에서 TeamSeer 추가</span><span class="sxs-lookup"><span data-stu-id="c70f3-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="c70f3-124">TeamSeer와 Azure AD 통합을 구성하려면 갤러리의 TeamSeer를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c70f3-125">**갤러리에서 TeamSeer를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c70f3-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c70f3-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c70f3-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c70f3-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c70f3-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c70f3-133">검색 상자에 **TeamSeer**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-133">In the search box, type **TeamSeer**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="c70f3-135">결과 창에서 **TeamSeer**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c70f3-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c70f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c70f3-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 TeamSeer에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c70f3-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 TeamSeer 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="c70f3-140">즉, Azure AD 사용자와 TeamSeer의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="c70f3-141">TeamSeer에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c70f3-142">TeamSeer에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c70f3-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c70f3-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c70f3-145">**[TeamSeer 테스트 사용자 만들기](#creating-a-teamseer-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 TeamSeer에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c70f3-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c70f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c70f3-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c70f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c70f3-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 TeamSeer 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="c70f3-150">**TeamSeer에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c70f3-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="c70f3-151">Azure Portal의 **TeamSeer** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c70f3-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="c70f3-155">**TeamSeer 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="c70f3-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="c70f3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c70f3-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-158">The value is not real.</span></span> <span data-ttu-id="c70f3-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="c70f3-160">값을 얻으려면 [TeamSeer 클라이언트 지원 팀](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c70f3-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="c70f3-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="c70f3-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c70f3-165">**TeamSeer 구성** 섹션에서 **TeamSeer 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c70f3-166">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="c70f3-168">다른 웹 브라우저 창에서 TeamSeer 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="c70f3-169">**HR 관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="c70f3-170">![HR 관리자](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR 관리자")</span><span class="sxs-lookup"><span data-stu-id="c70f3-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="c70f3-171">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="c70f3-172">![설치](./media/active-directory-saas-teamseer-tutorial/ic789635.png "설치")</span><span class="sxs-lookup"><span data-stu-id="c70f3-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="c70f3-173">**SAML 공급자 세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="c70f3-174">![SAML 설정](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="c70f3-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="c70f3-175">SAML 공급자 세부 정보 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="c70f3-176">![SAML 설정](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="c70f3-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="c70f3-177">a.</span><span class="sxs-lookup"><span data-stu-id="c70f3-177">a.</span></span> <span data-ttu-id="c70f3-178">**Single Sign-On 서비스 URL** 값을 **URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="c70f3-179">b.</span><span class="sxs-lookup"><span data-stu-id="c70f3-179">b.</span></span> <span data-ttu-id="c70f3-180">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **IdP 공용 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="c70f3-181">SMAL 공급자 구성을 완료하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="c70f3-182">![SAML 설정](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="c70f3-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="c70f3-183">a.</span><span class="sxs-lookup"><span data-stu-id="c70f3-183">a.</span></span> <span data-ttu-id="c70f3-184">**테스트 이메일 주소**에 테스트 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="c70f3-185">b.</span><span class="sxs-lookup"><span data-stu-id="c70f3-185">b.</span></span> <span data-ttu-id="c70f3-186">**발급자** 텍스트 상자에 서비스 공급자의 발급자 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="c70f3-187">c.</span><span class="sxs-lookup"><span data-stu-id="c70f3-187">c.</span></span> <span data-ttu-id="c70f3-188">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c70f3-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c70f3-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c70f3-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c70f3-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c70f3-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="c70f3-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c70f3-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c70f3-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c70f3-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c70f3-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c70f3-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c70f3-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c70f3-204">a.</span><span class="sxs-lookup"><span data-stu-id="c70f3-204">a.</span></span> <span data-ttu-id="c70f3-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c70f3-206">b.</span><span class="sxs-lookup"><span data-stu-id="c70f3-206">b.</span></span> <span data-ttu-id="c70f3-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c70f3-208">c.</span><span class="sxs-lookup"><span data-stu-id="c70f3-208">c.</span></span> <span data-ttu-id="c70f3-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c70f3-210">d.</span><span class="sxs-lookup"><span data-stu-id="c70f3-210">d.</span></span> <span data-ttu-id="c70f3-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="c70f3-212">TeamSeer 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c70f3-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="c70f3-213">Azure AD 사용자가 TeamSeer에 로그인할 수 있도록 하려면 ShiftPlanning으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="c70f3-214">TeamSeer의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="c70f3-215">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c70f3-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c70f3-216">**TeamSeer** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="c70f3-217">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="c70f3-218">![HR 관리자](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR 관리자")</span><span class="sxs-lookup"><span data-stu-id="c70f3-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="c70f3-219">a.</span><span class="sxs-lookup"><span data-stu-id="c70f3-219">a.</span></span> <span data-ttu-id="c70f3-220">**HR 관리자 \> 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="c70f3-221">b.</span><span class="sxs-lookup"><span data-stu-id="c70f3-221">b.</span></span> <span data-ttu-id="c70f3-222">**새 사용자 마법사 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="c70f3-223">**사용자 세부 정보** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c70f3-224">![사용자 세부 정보](./media/active-directory-saas-teamseer-tutorial/ic789641.png "사용자 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="c70f3-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="c70f3-225">a.</span><span class="sxs-lookup"><span data-stu-id="c70f3-225">a.</span></span> <span data-ttu-id="c70f3-226">관련된 텍스트 상자에 프로비전할 유효한 AAD 계정의 **이름**, **성**, **사용자 이름(이메일 주소)**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="c70f3-227">b.</span><span class="sxs-lookup"><span data-stu-id="c70f3-227">b.</span></span> <span data-ttu-id="c70f3-228">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-228">Click **Next**.</span></span>

4. <span data-ttu-id="c70f3-229">새 사용자를 추가하기 위한 화면의 지시를 따르고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="c70f3-230">다른 TeamSeer 사용자 계정 생성 도구 또는 TeamSeer가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c70f3-231">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c70f3-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c70f3-232">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 TeamSeer에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c70f3-234">**Britta Simon을 TeamSeer에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c70f3-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="c70f3-235">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c70f3-237">응용 프로그램 목록에서 **TeamSeer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-237">In the applications list, select **TeamSeer**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="c70f3-239">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-239">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c70f3-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-241">Click **Add** button.</span></span> <span data-ttu-id="c70f3-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c70f3-244">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c70f3-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c70f3-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c70f3-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c70f3-247">Testing single sign-on</span></span>

<span data-ttu-id="c70f3-248">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c70f3-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c70f3-249">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c70f3-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c70f3-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c70f3-250">Additional resources</span></span>

* [<span data-ttu-id="c70f3-251">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c70f3-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c70f3-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c70f3-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

