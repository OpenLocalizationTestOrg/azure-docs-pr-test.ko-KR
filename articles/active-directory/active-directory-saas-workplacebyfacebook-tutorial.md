---
title: "자습서: Workplace by Facebook과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Workplace by Facebook 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="4798e-103">자습서: Workplace by Facebook과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4798e-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="4798e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Workplace by Facebook을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4798e-105">Workplace by Facebook과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4798e-106">Azure AD에서는 Workplace by Facebook에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="4798e-107">사용자가 Azure AD 계정으로 Workplace by Facebook에 자동으로 로그인(Single Sign-On)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4798e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4798e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4798e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4798e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4798e-110">Prerequisites</span></span>

<span data-ttu-id="4798e-111">Workplace by Facebook과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="4798e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4798e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4798e-113">Workplace by Facebook Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4798e-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4798e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4798e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4798e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4798e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4798e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4798e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4798e-118">Scenario description</span></span>
<span data-ttu-id="4798e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4798e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4798e-121">갤러리에서 Workplace by Facebook 추가</span><span class="sxs-lookup"><span data-stu-id="4798e-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="4798e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4798e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="4798e-123">갤러리에서 Workplace by Facebook 추가</span><span class="sxs-lookup"><span data-stu-id="4798e-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="4798e-124">Azure AD에 Workplace by Facebook을 통합하도록 구성하려면 갤러리의 Workplace by Facebook을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4798e-125">**갤러리에서 Workplace by Facebook을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4798e-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4798e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4798e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4798e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="4798e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="4798e-133">검색 상자에서 **Workplace by Facebook**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="4798e-135">결과 패널에서 **Workplace by Facebook**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4798e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4798e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4798e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workplace by Facebook에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4798e-139">Single Sign-On이 작동하려면 Azure AD의 사용자에 해당하는 Workplace by Facebook의 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="4798e-140">즉, Azure AD 사용자와 Workplace by Facebook의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="4798e-141">이 링크 관계는 Azure AD의 **사용자 이름** 값을 Workplace by Facebook의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="4798e-142">Workplace by Facebook에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4798e-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4798e-144">**[재인증 빈도 구성](#configuring-reauthentication-frequency)** - SAML 확인을 요청하도록 작업 공간을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="4798e-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="4798e-146">**[Workplace by Facebook 테스트 사용자 만들기](#creating-a-workplace-by-facebook-test-user)** - Britta Simon의 Azure AD 표현과 연결된 사용자를 Workplace by Facebook에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="4798e-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="4798e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4798e-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4798e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4798e-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Workplace by Facebook 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="4798e-151">**Workplace by Facebook에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4798e-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="4798e-152">Azure Portal의 **Workplace by Facebook** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="4798e-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="4798e-156">**Workplace by Facebook 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="4798e-158">a.</span><span class="sxs-lookup"><span data-stu-id="4798e-158">a.</span></span> <span data-ttu-id="4798e-159">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="4798e-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="4798e-160">b.</span><span class="sxs-lookup"><span data-stu-id="4798e-160">b.</span></span> <span data-ttu-id="4798e-161">**식별자** 텍스트 상자에서 `https://www.facebook.com/company/<instancename>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4798e-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-162">These values are not the real.</span></span> <span data-ttu-id="4798e-163">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4798e-164">이러한 값을 구하려면 [Workplace by Facebook 클라이언트 지원 팀](https://workplace.fb.com/faq/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="4798e-165">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="4798e-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4798e-169">**Workplace by Facebook 구성** 섹션에서 **Workplace by Facebook 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4798e-170">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="4798e-172">다른 웹 브라우저 창에서 Workplace by Facebook 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="4798e-173">SAML 인증 프로세스의 일환으로 Workplace는 Azure AD에 매개 변수를 전달하기 위해 최대 2.5KB 크기의 쿼리 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="4798e-174">**회사 대시보드**에서 **인증** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="4798e-175">**SAML 인증** 아래 드롭다운 목록에서 **SSO 전용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="4798e-176">Azure Portal의 **Workplace by Facebook 구성** 섹션에서 복사한 값을 해당 필드에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="4798e-177">**SAML URL** 텍스트 상자에 Azure Portal에서 복사한 **Single Sign-On 서비스 URL** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="4798e-178">**SAML 발급자 URL 텍스트 상자**에 Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="4798e-179">**SAML 로그아웃 리디렉션**(선택 사항)에 Azure Portal에서 복사한 **로그아웃 URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="4798e-180">Azure Portal에서 다운로드한 **base-64로 인코딩된 인증서**를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음 **SAML 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="4798e-181">**SAML 구성** 섹션에 나열된 대상 그룹 URL, 받는 사람 URL 및 ACS(Assertion Consumer Service) URL을 입력해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="4798e-182">섹션 맨 아래로 스크롤하여 **SSO 테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="4798e-183">Azure AD 로그인 페이지가 있는 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="4798e-184">일반적인 인증처럼 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="4798e-185">**문제 해결:** Azure AD에서 반환되는 이메일 주소가 로그인한 Workplace 계정과 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="4798e-186">테스트가 성공적으로 완료되면 페이지 하단으로 스크롤하여 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="4798e-187">Workplace를 사용하는 모든 사용자에게 이제 인증을 위한 Azure AD 로그인 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="4798e-188">**SAML 로그아웃 리디렉션(선택 사항)** -</span><span class="sxs-lookup"><span data-stu-id="4798e-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="4798e-189">Azure AD의 로그아웃 페이지를 가리키는 데 사용할 수 있는 SAML 로그아웃 URL을 선택적으로 구성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="4798e-190">이 설정을 사용하도록 설정하고 구성하면 더 이상 사용자가 Workplace 로그아웃 페이지로 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="4798e-191">대신 SAML 로그아웃 리디렉션 설정에 추가된 URL로 사용자가 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="4798e-192">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4798e-193">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4798e-194">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="4798e-195">재인증 빈도 구성</span><span class="sxs-lookup"><span data-stu-id="4798e-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="4798e-196">매일, 3일, 1주, 2주, 매달을 주기로 SAML 확인을 요청하거나 SAML 확인을 요청하지 않도록 Workplace를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="4798e-197">모바일 응용 프로그램에서 SAML 확인에 대한 최소값은 일주일로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="4798e-198">Require SAML authentication for all users now(모든 사용자에게 SAML 인증 요구) 단추를 사용하여 모든 사용자에 대해 SAML 다시 설정을 강제 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4798e-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4798e-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="4798e-200">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="4798e-202">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="4798e-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4798e-203">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4798e-205">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4798e-207">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4798e-209">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4798e-211">a.</span><span class="sxs-lookup"><span data-stu-id="4798e-211">a.</span></span> <span data-ttu-id="4798e-212">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4798e-213">b.</span><span class="sxs-lookup"><span data-stu-id="4798e-213">b.</span></span> <span data-ttu-id="4798e-214">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4798e-215">c.</span><span class="sxs-lookup"><span data-stu-id="4798e-215">c.</span></span> <span data-ttu-id="4798e-216">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4798e-217">d.</span><span class="sxs-lookup"><span data-stu-id="4798e-217">d.</span></span> <span data-ttu-id="4798e-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="4798e-219">Workplace by Facebook 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4798e-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="4798e-220">이 섹션에서는 Workplace by Facebook에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="4798e-221">Workplace by Facebook은 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="4798e-222">이 섹션에는 사용자의 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-222">There is no action for you in this section.</span></span> <span data-ttu-id="4798e-223">Workplace by Facebook에 사용자가 없는 경우 Workplace by Facebook에 액세스하려고 하면 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="4798e-224">사용자를 수동으로 만들어야 하는 경우 [Workplace by Facebook 클라이언트 지원 팀](https://workplace.fb.com/faq/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4798e-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4798e-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4798e-226">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Workplace by Facebook에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4798e-228">**Britta Simon을 Workplace by Facebook에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4798e-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="4798e-229">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4798e-231">응용 프로그램 목록에서 **Workplace by Facebook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="4798e-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-233">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="4798e-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-235">Click **Add** button.</span></span> <span data-ttu-id="4798e-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="4798e-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4798e-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4798e-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4798e-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4798e-241">Testing single sign-on</span></span>

<span data-ttu-id="4798e-242">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4798e-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="4798e-243">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4798e-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4798e-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4798e-244">Additional resources</span></span>

* [<span data-ttu-id="4798e-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="4798e-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4798e-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4798e-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4798e-247">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="4798e-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

