---
title: "자습서: AnswerHub와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 AnswerHub 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="94247-103">자습서: AnswerHub와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="94247-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="94247-104">이 자습서에서는 Azure AD(Azure Active Directory)와 AnswerHub를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94247-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94247-105">AnswerHub와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="94247-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94247-106">AnswerHub에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="94247-107">사용자가 해당 Azure AD 계정으로 AnswerHub에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94247-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="94247-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94247-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94247-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="94247-110">Prerequisites</span></span>

<span data-ttu-id="94247-111">AnswerHub와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="94247-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="94247-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94247-113">AnswerHub Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="94247-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94247-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94247-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94247-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="94247-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94247-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94247-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="94247-118">Scenario description</span></span>
<span data-ttu-id="94247-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94247-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94247-121">갤러리에서 AnswerHub 추가</span><span class="sxs-lookup"><span data-stu-id="94247-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="94247-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="94247-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="94247-123">갤러리에서 AnswerHub 추가</span><span class="sxs-lookup"><span data-stu-id="94247-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="94247-124">AnswerHub의 Azure AD 통합을 구성하려면 갤러리의 AnswerHub를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94247-125">**갤러리에서 AnswerHub를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94247-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94247-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94247-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94247-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="94247-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="94247-133">검색 상자에 **AnswerHub**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-133">In the search box, type **AnswerHub**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="94247-135">결과 패널에서 **AnswerHub**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94247-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="94247-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94247-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AnswerHub에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94247-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 AnswerHub 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="94247-140">즉, Azure AD 사용자와 AnswerHub의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="94247-141">AnswerHub에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94247-142">AnswerHub에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94247-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94247-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94247-145">**[AnswerHub 테스트 사용자 만들기](#creating-an-answerhub-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 AnswerHub에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94247-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94247-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94247-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94247-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="94247-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94247-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 AnswerHub 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="94247-150">**AnswerHub에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94247-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="94247-151">Azure Portal의 **AnswerHub** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="94247-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="94247-155">**AnswerHub 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="94247-157">a.</span><span class="sxs-lookup"><span data-stu-id="94247-157">a.</span></span> <span data-ttu-id="94247-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="94247-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="94247-159">b.</span><span class="sxs-lookup"><span data-stu-id="94247-159">b.</span></span> <span data-ttu-id="94247-160">**식별자** 텍스트 상자에서 `https://<company>.answerhub.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94247-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="94247-161">These values are not real.</span></span> <span data-ttu-id="94247-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="94247-163">이러한 값을 가져오려면 [AnswerHub 클라이언트 지원팀](mailto:success@answerhub.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="94247-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="94247-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="94247-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94247-168">**AnswerHub 구성** 섹션에서 **AnswerHub 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="94247-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94247-169">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="94247-171">다른 웹 브라우저 창에서 AnswerHub 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="94247-172">AnswerHub 구성하는 데 도움이 필요하면 [AnswerHub 지원 팀](mailto:success@answerhub.com.)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="94247-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="94247-173">**관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="94247-174">**사용자 및 그룹** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="94247-175">탐색 창의 왼쪽에 있는 **소셜 설정** 섹션에서 **SAML 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="94247-176">**IDP 구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="94247-177">**IDP 구성** 탭에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="94247-178">![SAML 설정](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="94247-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="94247-179">a.</span><span class="sxs-lookup"><span data-stu-id="94247-179">a.</span></span> <span data-ttu-id="94247-180">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **IDP 로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="94247-181">b.</span><span class="sxs-lookup"><span data-stu-id="94247-181">b.</span></span> <span data-ttu-id="94247-182">Azure Portal에서 복사한 **로그아웃 URL**을 **IDP 로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="94247-183">c.</span><span class="sxs-lookup"><span data-stu-id="94247-183">c.</span></span> <span data-ttu-id="94247-184">**사용자 특성** 섹션의 Azure Portal에서 선택한 것과 동일한 사용자 ID 값을 **IDP 이름 식별자 형식**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="94247-185">d.</span><span class="sxs-lookup"><span data-stu-id="94247-185">d.</span></span> <span data-ttu-id="94247-186">**키 및 인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="94247-187">키와 인증서 탭에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="94247-188">![키 및 인증서](./media/active-directory-saas-answerhub-tutorial/ic785173.png "키 및 인증서")</span><span class="sxs-lookup"><span data-stu-id="94247-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="94247-189">a.</span><span class="sxs-lookup"><span data-stu-id="94247-189">a.</span></span> <span data-ttu-id="94247-190">Azure Portal에서 다운로드한 Base-64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **IDP 공개 키(x509 형식)** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="94247-191">b.</span><span class="sxs-lookup"><span data-stu-id="94247-191">b.</span></span> <span data-ttu-id="94247-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-192">Click **Save**.</span></span>

14. <span data-ttu-id="94247-193">**IDP 구성** 탭에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="94247-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94247-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94247-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94247-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94247-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="94247-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="94247-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94247-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="94247-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="94247-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94247-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94247-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94247-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94247-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94247-209">a.</span><span class="sxs-lookup"><span data-stu-id="94247-209">a.</span></span> <span data-ttu-id="94247-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94247-211">b.</span><span class="sxs-lookup"><span data-stu-id="94247-211">b.</span></span> <span data-ttu-id="94247-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94247-213">c.</span><span class="sxs-lookup"><span data-stu-id="94247-213">c.</span></span> <span data-ttu-id="94247-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="94247-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="94247-215">d.</span><span class="sxs-lookup"><span data-stu-id="94247-215">d.</span></span> <span data-ttu-id="94247-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="94247-217">AnswerHub 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="94247-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="94247-218">Azure AD 사용자가 AnswerHub에 로그인할 수 있도록 하려면 AnswerHub로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="94247-219">AnswerHub의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="94247-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="94247-220">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94247-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="94247-221">**AnswerHub** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="94247-222">**관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="94247-223">**사용자 및 그룹** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="94247-224">왼쪽 탐색 창의 **사용자 관리** 섹션에서 **사용자 만들기 또는 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="94247-225">![사용자 및 그룹](./media/active-directory-saas-answerhub-tutorial/ic785175.png "사용자 및 그룹")</span><span class="sxs-lookup"><span data-stu-id="94247-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="94247-226">관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 계정의 **전자 메일 주소**, **사용자 이름** 및 **암호**를 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="94247-227">다른 AnswerHub 사용자 계정 생성 도구 또는 AnswerHub가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94247-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="94247-228">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="94247-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="94247-229">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 AnswerHub에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![사용자 할당][200] 

<span data-ttu-id="94247-231">**Britta Simon을 AnswerHub에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94247-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="94247-232">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="94247-234">응용 프로그램 목록에서 **AnswerHub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-234">In the applications list, select **AnswerHub**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="94247-236">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-236">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="94247-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-238">Click **Add** button.</span></span> <span data-ttu-id="94247-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="94247-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94247-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94247-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94247-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="94247-244">Testing single sign-on</span></span>

<span data-ttu-id="94247-245">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="94247-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94247-246">액세스 패널에서 AnswerHub 타일을 클릭하면 AnswerHub 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="94247-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="94247-247">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94247-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94247-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="94247-248">Additional resources</span></span>

* [<span data-ttu-id="94247-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="94247-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94247-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="94247-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

