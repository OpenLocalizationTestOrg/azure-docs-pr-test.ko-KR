---
title: "자습서: Image Relay와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Image Relay 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="91a22-103">자습서: Image Relay와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="91a22-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="91a22-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Image Relay를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91a22-105">Image Relay와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91a22-106">Azure AD에서는 Image Relay에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="91a22-107">사용자가 해당 Azure AD 계정으로 Image Relay에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91a22-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="91a22-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91a22-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91a22-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="91a22-110">Prerequisites</span></span>

<span data-ttu-id="91a22-111">Image Relay와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="91a22-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="91a22-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91a22-113">Image Relay Single Sign-On 사용이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="91a22-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91a22-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91a22-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91a22-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="91a22-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91a22-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91a22-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="91a22-118">Scenario description</span></span>
<span data-ttu-id="91a22-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91a22-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91a22-121">갤러리에서 Image Relay 추가</span><span class="sxs-lookup"><span data-stu-id="91a22-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="91a22-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="91a22-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="91a22-123">갤러리에서 Image Relay 추가</span><span class="sxs-lookup"><span data-stu-id="91a22-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="91a22-124">Azure AD에 Image Relay를 통합하도록 구성하려면 갤러리의 Image Relay를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91a22-125">**갤러리에서 Image Relay를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="91a22-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91a22-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91a22-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91a22-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="91a22-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="91a22-133">검색 상자에서 **Image Relay**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-133">In the search box, type **Image Relay**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="91a22-135">결과 패널에서 **Image Relay**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91a22-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="91a22-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91a22-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Image Relay에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91a22-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Image Relay 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="91a22-140">즉 Azure AD 사용자와 Image Relay의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="91a22-141">Image Relay에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="91a22-142">Image Relay에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91a22-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="91a22-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91a22-145">**[Image Relay 테스트 사용자 만들기](#creating-an-image-relay-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Image Relay에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="91a22-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91a22-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91a22-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="91a22-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91a22-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Image Relay 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="91a22-150">**Image Relay에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="91a22-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="91a22-151">Azure Portal의 **Image Relay** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="91a22-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="91a22-155">**Image Relay 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="91a22-157">a.</span><span class="sxs-lookup"><span data-stu-id="91a22-157">a.</span></span> <span data-ttu-id="91a22-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="91a22-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="91a22-159">b.</span><span class="sxs-lookup"><span data-stu-id="91a22-159">b.</span></span> <span data-ttu-id="91a22-160">**식별자** 텍스트 상자에서 `https://<companyname>.imagerelay.com/sso/metadata` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91a22-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-161">These values are not real.</span></span> <span data-ttu-id="91a22-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91a22-163">이러한 값을 얻으려면 [Image Relay 클라이언트 지원 팀](http://support.imagerelay.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="91a22-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="91a22-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="91a22-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91a22-168">**Image Relay 구성** 섹션에서 **Image Relay 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91a22-169">**빠른 참조 섹션**에서 **로그아웃 서비스 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="91a22-171">다른 브라우저 창에서 Image Relay 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="91a22-172">위쪽의 도구 모음에서 **사용자 및 권한** 워크로드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="91a22-174">**새 사용 권한 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-174">Click **Create New Permission**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="91a22-176">**Single Sign-On 설정** 워크로드에서 **이 그룹은 Single Sign On을 통해서만 로그인 가능** 확인란을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="91a22-178">**계정 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-178">Go to **Account Settings**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="91a22-180">**Single Sign On 설정** 작업으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Single Sign-On 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="91a22-182">**SAML 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Single Sign-On 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="91a22-184">a.</span><span class="sxs-lookup"><span data-stu-id="91a22-184">a.</span></span> <span data-ttu-id="91a22-185">Azure Portal에서 복사한 **Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91a22-186">b.</span><span class="sxs-lookup"><span data-stu-id="91a22-186">b.</span></span> <span data-ttu-id="91a22-187">Azure Portal에서 복사한 **Single Sign-Out 서비스 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91a22-188">c.</span><span class="sxs-lookup"><span data-stu-id="91a22-188">c.</span></span> <span data-ttu-id="91a22-189">**이름 ID 형식**으로 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="91a22-190">d.</span><span class="sxs-lookup"><span data-stu-id="91a22-190">d.</span></span> <span data-ttu-id="91a22-191">**서비스 공급자(Image Relay) 요청에 대한 바인딩 옵션**으로 **POST 바인딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="91a22-192">e.</span><span class="sxs-lookup"><span data-stu-id="91a22-192">e.</span></span> <span data-ttu-id="91a22-193">**x.509 인증서**에서 **인증서 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="91a22-195">f.</span><span class="sxs-lookup"><span data-stu-id="91a22-195">f.</span></span> <span data-ttu-id="91a22-196">다운로드한 인증서를 메모장에서 열고, 내용을 복사한 다음 전체 인증서를 x.509 인증서 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="91a22-198">g.</span><span class="sxs-lookup"><span data-stu-id="91a22-198">g.</span></span> <span data-ttu-id="91a22-199">**Just-In-Time 사용자 프로비전** 섹션에서 **Just-In-Time 사용자 프로비전 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="91a22-201">h.</span><span class="sxs-lookup"><span data-stu-id="91a22-201">h.</span></span> <span data-ttu-id="91a22-202">Single Sign-On을 통해서만 로그인할 수 있는 사용 권한 그룹(예: **SSO 기본**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="91a22-204">i.</span><span class="sxs-lookup"><span data-stu-id="91a22-204">i.</span></span> <span data-ttu-id="91a22-205">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="91a22-206">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91a22-207">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91a22-208">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91a22-209">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="91a22-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="91a22-210">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="91a22-212">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="91a22-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91a22-213">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91a22-215">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91a22-217">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91a22-219">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91a22-221">a.</span><span class="sxs-lookup"><span data-stu-id="91a22-221">a.</span></span> <span data-ttu-id="91a22-222">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91a22-223">b.</span><span class="sxs-lookup"><span data-stu-id="91a22-223">b.</span></span> <span data-ttu-id="91a22-224">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91a22-225">c.</span><span class="sxs-lookup"><span data-stu-id="91a22-225">c.</span></span> <span data-ttu-id="91a22-226">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="91a22-227">d.</span><span class="sxs-lookup"><span data-stu-id="91a22-227">d.</span></span> <span data-ttu-id="91a22-228">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="91a22-229">Image Relay 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="91a22-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="91a22-230">이 섹션에서는 Image Relay에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="91a22-231">**Image Relay에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="91a22-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="91a22-232">Image Relay 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="91a22-233">**사용자 및 권한**으로 이동하여 **SSO 사용자 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="91a22-235">프로비전하려는 사용자의 **전자 메일**, **이름**, **성** 및 **회사**를 입력하고 Single Sign-On을 통해서만 로그인할 수 있는 그룹인 권한 그룹(예: SSO 기본)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="91a22-237">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="91a22-238">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="91a22-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="91a22-239">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Image Relay에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![사용자 할당][200] 

<span data-ttu-id="91a22-241">**Britta Simon을 Image Relay에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="91a22-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="91a22-242">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="91a22-244">응용 프로그램 목록에서 **Image Relay**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-244">In the applications list, select **Image Relay**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="91a22-246">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-246">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="91a22-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-248">Click **Add** button.</span></span> <span data-ttu-id="91a22-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="91a22-251">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="91a22-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91a22-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91a22-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="91a22-254">Testing single sign-on</span></span>

<span data-ttu-id="91a22-255">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="91a22-256">[액세스 패널]에서 [Image Relay] 타일을 클릭하면 Image Relay 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a22-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="91a22-257">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="91a22-257">Additional resources</span></span>

* [<span data-ttu-id="91a22-258">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="91a22-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91a22-259">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="91a22-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

