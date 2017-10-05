---
title: "자습서: IdeaScale과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 IdeaScale 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="e6009-103">자습서: IdeaScale과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e6009-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="e6009-104">이 자습서에서는 Azure AD(Azure Active Directory)와 IdeaScale을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6009-105">IdeaScale을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e6009-106">IdeaScale에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="e6009-107">사용자가 해당 Azure AD 계정으로 IdeaScale에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e6009-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e6009-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6009-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6009-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e6009-110">Prerequisites</span></span>

<span data-ttu-id="e6009-111">IdeaScale과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="e6009-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e6009-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6009-113">IdeaScale Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e6009-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e6009-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e6009-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6009-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e6009-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e6009-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e6009-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e6009-118">Scenario description</span></span>
<span data-ttu-id="e6009-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e6009-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6009-121">갤러리에서 IdeaScale 추가</span><span class="sxs-lookup"><span data-stu-id="e6009-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="e6009-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e6009-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="e6009-123">갤러리에서 IdeaScale 추가</span><span class="sxs-lookup"><span data-stu-id="e6009-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="e6009-124">IdeaScale의 Azure AD 통합을 구성하려면 갤러리의 IdeaScale을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e6009-125">**갤러리에서 IdeaScale을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e6009-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e6009-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e6009-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e6009-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e6009-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e6009-133">검색 상자에 **IdeaScale**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-133">In the search box, type **IdeaScale**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="e6009-135">결과 패널에서 **IdeaScale**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e6009-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e6009-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e6009-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 IdeaScale에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e6009-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 IdeaScale 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="e6009-140">즉, Azure AD 사용자와 IdeaScale의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="e6009-141">IdeaScale에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e6009-142">IdeaScale에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e6009-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e6009-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6009-145">**[IdeaScale 테스트 사용자 만들기](#creating-an-ideascale-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 IdeaScale에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e6009-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6009-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e6009-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e6009-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e6009-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 IdeaScale 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="e6009-150">**IdeaScale에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e6009-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="e6009-151">Azure Portal의 **IdeaScale** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e6009-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="e6009-155">**IdeaScale 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="e6009-157">a.</span><span class="sxs-lookup"><span data-stu-id="e6009-157">a.</span></span> <span data-ttu-id="e6009-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="e6009-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="e6009-159">b.</span><span class="sxs-lookup"><span data-stu-id="e6009-159">b.</span></span> <span data-ttu-id="e6009-160">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="e6009-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-161">These values are not real.</span></span> <span data-ttu-id="e6009-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e6009-163">이러한 값을 얻으려면 [IdeaScale 클라이언트 지원 팀](http://support.ideascale.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e6009-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="e6009-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="e6009-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e6009-168">**IdeaScale 구성** 섹션에서 **IdeaScale 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e6009-169">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML 엔터티 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="e6009-171">다른 웹 브라우저 창에서 IdeaScale 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="e6009-172">**커뮤니티 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="e6009-173">![커뮤니티 설정](./media/active-directory-saas-ideascale-tutorial/ic790847.png "커뮤니티 설정")</span><span class="sxs-lookup"><span data-stu-id="e6009-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="e6009-174">**보안 \> Single Sign On 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="e6009-175">![Single Signon 설정](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon 설정")</span><span class="sxs-lookup"><span data-stu-id="e6009-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="e6009-176">**Single Sign On 유형**으로 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="e6009-177">![Single Signon 유형](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon 유형")</span><span class="sxs-lookup"><span data-stu-id="e6009-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="e6009-178">**Single Sign On 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="e6009-179">![Single Signon 설정](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon 설정")</span><span class="sxs-lookup"><span data-stu-id="e6009-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="e6009-180">a.</span><span class="sxs-lookup"><span data-stu-id="e6009-180">a.</span></span> <span data-ttu-id="e6009-181">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **SAML IdP 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e6009-182">b.</span><span class="sxs-lookup"><span data-stu-id="e6009-182">b.</span></span> <span data-ttu-id="e6009-183">Azure Portal에서 다운로드한 메타데이터 파일의 콘텐츠를 복사한 다음 **SAML IdP 메타데이터** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="e6009-184">c.</span><span class="sxs-lookup"><span data-stu-id="e6009-184">c.</span></span> <span data-ttu-id="e6009-185">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 성공 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e6009-186">d.</span><span class="sxs-lookup"><span data-stu-id="e6009-186">d.</span></span> <span data-ttu-id="e6009-187">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e6009-188">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e6009-189">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e6009-190">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e6009-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e6009-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="e6009-192">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e6009-194">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="e6009-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e6009-195">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e6009-197">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e6009-199">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e6009-201">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e6009-203">a.</span><span class="sxs-lookup"><span data-stu-id="e6009-203">a.</span></span> <span data-ttu-id="e6009-204">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6009-205">b.</span><span class="sxs-lookup"><span data-stu-id="e6009-205">b.</span></span> <span data-ttu-id="e6009-206">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e6009-207">c.</span><span class="sxs-lookup"><span data-stu-id="e6009-207">c.</span></span> <span data-ttu-id="e6009-208">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e6009-209">d.</span><span class="sxs-lookup"><span data-stu-id="e6009-209">d.</span></span> <span data-ttu-id="e6009-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="e6009-211">IdeaScale 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e6009-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="e6009-212">Azure AD 사용자가 IdeaScale에 로그인할 수 있도록 하려면 IdeaScale로 프로비저닝되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="e6009-213">IdeaScale의 경우 프로비저닝은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="e6009-214">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e6009-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e6009-215">**IdeaScale** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="e6009-216">**커뮤니티 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="e6009-217">![커뮤니티 설정](./media/active-directory-saas-ideascale-tutorial/ic790847.png "커뮤니티 설정")</span><span class="sxs-lookup"><span data-stu-id="e6009-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="e6009-218">**기본 설정 \> 멤버 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="e6009-219">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="e6009-220">![멤버 관리](./media/active-directory-saas-ideascale-tutorial/ic790852.png "멤버 관리")</span><span class="sxs-lookup"><span data-stu-id="e6009-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="e6009-221">새 멤버 추가 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="e6009-222">![새 멤버 추가](./media/active-directory-saas-ideascale-tutorial/ic790853.png "새 멤버 추가")</span><span class="sxs-lookup"><span data-stu-id="e6009-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="e6009-223">a.</span><span class="sxs-lookup"><span data-stu-id="e6009-223">a.</span></span> <span data-ttu-id="e6009-224">**전자 메일 주소** 텍스트 상자에 프로비저닝할 유효한 AAD 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="e6009-225">b.</span><span class="sxs-lookup"><span data-stu-id="e6009-225">b.</span></span> <span data-ttu-id="e6009-226">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="e6009-227">Azure Active Directory 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크가 포함된 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="e6009-228">다른 IdeaScale 사용자 계정 생성 도구 또는 IdeaScale이 제공한 API를 사용하여 AAD 사용자 계정을 프로비저닝할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e6009-229">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e6009-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e6009-230">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 IdeaScale에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e6009-232">**Britta Simon을 IdeaScale에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e6009-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="e6009-233">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e6009-235">응용 프로그램 목록에서 **IdeaScale**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-235">In the applications list, select **IdeaScale**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="e6009-237">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-237">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e6009-239">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-239">Click **Add** button.</span></span> <span data-ttu-id="e6009-240">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e6009-242">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e6009-243">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e6009-244">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e6009-245">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e6009-245">Testing single sign-on</span></span>


<span data-ttu-id="e6009-246">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e6009-247">액세스 패널에서 IdeaScale 타일을 클릭하면 IdeaScale 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6009-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e6009-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e6009-248">Additional resources</span></span>

* [<span data-ttu-id="e6009-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e6009-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6009-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e6009-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

