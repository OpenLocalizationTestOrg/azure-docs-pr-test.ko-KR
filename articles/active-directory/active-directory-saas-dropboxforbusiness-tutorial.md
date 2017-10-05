---
title: "자습서: Dropbox for Business와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Dropbox for Business 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="8d7c8-103">자습서: Dropbox for Business와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="8d7c8-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="8d7c8-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Dropbox for Business를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d7c8-105">Dropbox for Business를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d7c8-106">Dropbox for Business에 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="8d7c8-107">사용자가 자신의 Azure AD 계정으로 Dropbox for Business에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d7c8-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d7c8-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d7c8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8d7c8-110">Prerequisites</span></span>

<span data-ttu-id="8d7c8-111">Dropbox for Business와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="8d7c8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="8d7c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d7c8-113">Dropbox for Business Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="8d7c8-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d7c8-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d7c8-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d7c8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d7c8-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d7c8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="8d7c8-118">Scenario description</span></span>
<span data-ttu-id="8d7c8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d7c8-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d7c8-121">갤러리에서 Dropbox for Business 추가</span><span class="sxs-lookup"><span data-stu-id="8d7c8-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="8d7c8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8d7c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="8d7c8-123">갤러리에서 Dropbox for Business 추가</span><span class="sxs-lookup"><span data-stu-id="8d7c8-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="8d7c8-124">Dropbox for Business가 Azure AD에 통합되도록 구성하려면 갤러리에서 Dropbox for Business를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d7c8-125">**갤러리에서 Dropbox for Business를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8d7c8-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d7c8-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d7c8-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d7c8-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="8d7c8-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="8d7c8-133">검색 상자에 **Dropbox for Business**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="8d7c8-135">결과 패널에서 **Dropbox for Business**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d7c8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8d7c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d7c8-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Dropbox for Business에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d7c8-139">Single Sign-On이 작동하려면 Azure AD의 사용자에 해당하는 Dropbox for Business의 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="8d7c8-140">즉, Azure AD 사용자와 Dropbox for Business의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="8d7c8-141">이 링크 관계는 Azure AD의 **사용자 이름** 값을 Dropbox for Business의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="8d7c8-142">Dropbox for Business에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d7c8-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d7c8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d7c8-145">**[Dropbox for Business 테스트 사용자 만들기](#creating-a-dropbox-for-business-test-user)** - Britta Simon의 Azure AD 표현과 연결된 사용자를 Dropbox for Business에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d7c8-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d7c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d7c8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="8d7c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d7c8-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Dropbox for Business 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="8d7c8-150">**Dropbox for Business에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8d7c8-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="8d7c8-151">Azure Portal의 **Dropbox for Business** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="8d7c8-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="8d7c8-155">**Dropbox for Business 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="8d7c8-156">a.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-156">a.</span></span> <span data-ttu-id="8d7c8-157">Dropbox for Business 테넌트에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="8d7c8-158">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="8d7c8-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8d7c8-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-159">b.</span></span> <span data-ttu-id="8d7c8-160">왼쪽의 탐색 창에서 **관리 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="8d7c8-161">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="8d7c8-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8d7c8-162">c.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-162">c.</span></span> <span data-ttu-id="8d7c8-163">**관리 콘솔**의 왼쪽 탐색 창에서 **인증**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="8d7c8-164">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="8d7c8-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8d7c8-165">d.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-165">d.</span></span> <span data-ttu-id="8d7c8-166">**Single Sign-On** 섹션에서 **Single Sign-On 사용**을 선택한 다음 **추가**를 클릭하여 이 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="8d7c8-167">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="8d7c8-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8d7c8-168">e.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-168">e.</span></span> <span data-ttu-id="8d7c8-169">**자신의 전자 메일 주소를 입력하여 사용자가 로그인하거나 직접 이동할 수 있습니다.**옆의 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="8d7c8-171">f.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-171">f.</span></span> <span data-ttu-id="8d7c8-172">Azure Portal에서 **로그온 URL** 텍스트 상자에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="8d7c8-174">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="8d7c8-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d7c8-175">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-175">This value is not real value.</span></span> <span data-ttu-id="8d7c8-176">Single Sign-On 섹션에서 얻은 실제 로그온 URL로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="8d7c8-177">이 값을 얻으려면 [Dropbox for Business 클라이언트 지원 팀](https://www.dropbox.com/business/contact)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="8d7c8-178">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="8d7c8-180">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-180">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d7c8-182">**Dropbox for Business 구성** 섹션에서 **Dropbox for Business 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8d7c8-183">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="8d7c8-185">**Dropbox for Business** 측에서 Single Sign-On을 구성하려면 Dropbox for Business 테넌트로 이동하여 **인증** 페이지의 **Single Sign-On** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="8d7c8-186">![Single Sign-On 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="8d7c8-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="8d7c8-187">a.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-187">a.</span></span> <span data-ttu-id="8d7c8-188">**필수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-188">Click **Required**.</span></span>
   
    <span data-ttu-id="8d7c8-189">b.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-189">b.</span></span> <span data-ttu-id="8d7c8-190">Azure Portal의 **로그온 구성** 창에서 **SAML Single Sign-On 서비스 URL** 값을 복사한 다음 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="8d7c8-191">c.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-191">c.</span></span> <span data-ttu-id="8d7c8-192">**인증서 선택**을 클릭한 다음 **Base64로 인코딩된 인증서 파일**을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="8d7c8-193">d.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-193">d.</span></span> <span data-ttu-id="8d7c8-194">**변경 내용 저장**을 클릭하여 DropBox for Business 테넌트의 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="8d7c8-195">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d7c8-196">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d7c8-197">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d7c8-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8d7c8-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d7c8-199">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="8d7c8-201">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="8d7c8-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d7c8-202">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="8d7c8-204">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d7c8-206">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d7c8-208">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d7c8-210">a.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-210">a.</span></span> <span data-ttu-id="8d7c8-211">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d7c8-212">b.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-212">b.</span></span> <span data-ttu-id="8d7c8-213">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d7c8-214">c.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-214">c.</span></span> <span data-ttu-id="8d7c8-215">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d7c8-216">d.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-216">d.</span></span> <span data-ttu-id="8d7c8-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="8d7c8-218">Dropbox for Business 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8d7c8-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="8d7c8-219">이 섹션에서는 Dropbox for Business에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="8d7c8-220">Dropbox for Business는 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8d7c8-221">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-221">There is no action item for you in this section.</span></span> <span data-ttu-id="8d7c8-222">Dropbox for Business에 아직 사용자가 없으면 Dropbox for Business에 액세스하려고 할 때 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="8d7c8-223">사용자를 수동으로 만들어야 하는 경우 [Dropbox for Business 클라이언트 지원 팀](https://www.dropbox.com/business/contact)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d7c8-224">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="8d7c8-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d7c8-225">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Dropbox for Business에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![사용자 할당][200] 

<span data-ttu-id="8d7c8-227">**Britta Simon을 Dropbox for Business에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8d7c8-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="8d7c8-228">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="8d7c8-230">응용 프로그램 목록에서 **Dropbox for Business**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="8d7c8-232">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-232">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="8d7c8-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-234">Click **Add** button.</span></span> <span data-ttu-id="8d7c8-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="8d7c8-237">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d7c8-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d7c8-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d7c8-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="8d7c8-240">Testing single sign-on</span></span>

<span data-ttu-id="8d7c8-241">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8d7c8-242">액세스 패널에서 Dropbox for Business 타일을 클릭하면 Dropbox for Business 응용 프로그램의 로그인 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d7c8-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8d7c8-243">Additional resources</span></span>

* [<span data-ttu-id="8d7c8-244">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="8d7c8-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d7c8-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8d7c8-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8d7c8-246">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="8d7c8-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

