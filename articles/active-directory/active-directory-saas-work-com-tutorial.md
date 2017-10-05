---
title: "자습서: Work.com와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Work.com 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="2d05d-103">자습서: Work.com과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2d05d-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="2d05d-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Work.com을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d05d-105">Work.com을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2d05d-106">Work.com에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="2d05d-107">사용자가 해당 Azure AD 계정으로 Work.com에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d05d-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2d05d-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d05d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d05d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2d05d-110">Prerequisites</span></span>

<span data-ttu-id="2d05d-111">Work.com과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="2d05d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2d05d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d05d-113">Work.com Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2d05d-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d05d-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d05d-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d05d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2d05d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d05d-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d05d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2d05d-118">Scenario description</span></span>
<span data-ttu-id="2d05d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d05d-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d05d-121">갤러리에서 Work.com 추가</span><span class="sxs-lookup"><span data-stu-id="2d05d-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="2d05d-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2d05d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="2d05d-123">갤러리에서 Work.com 추가</span><span class="sxs-lookup"><span data-stu-id="2d05d-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="2d05d-124">Work.com의 Azure AD 통합을 구성하려면 갤러리의 Work.com을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2d05d-125">**갤러리에서 Work.com을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d05d-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2d05d-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d05d-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2d05d-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2d05d-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2d05d-133">검색 상자에 **Work.com**을 입력하고 결과 패널에서 **Work.com**을 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![갤러리에서 추가](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2d05d-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2d05d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2d05d-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Work.com에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d05d-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Work.com 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="2d05d-138">즉, Azure AD 사용자와 Work.com의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="2d05d-139">Work.com에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2d05d-140">Work.com에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2d05d-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2d05d-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d05d-143">**[Work.com 테스트 사용자 만들기](#create-a-workcom-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Work.com에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d05d-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d05d-145">**[Single Sign-on 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2d05d-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2d05d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2d05d-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Work.com 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="2d05d-148">Single Sign-On을 구성하려면 사용자 할당 도메인 이름을 Work.com로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="2d05d-149">최소한 한 개의 도메인 이름을 정의하고, 도메인 이름을 테스트 한 후 전체 조직에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="2d05d-150">**Work.com에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d05d-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="2d05d-151">Azure Portal의 **Work.com** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2d05d-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="2d05d-155">**Work.com 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Work.com 도메인 및 URL 섹션](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="2d05d-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2d05d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d05d-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-158">This value is not real.</span></span> <span data-ttu-id="2d05d-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2d05d-160">이 값을 얻으려면 [Work.com 클라이언트 지원 팀](https://help.salesforce.com/articleView?id=000159855&type=3)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="2d05d-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="2d05d-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="2d05d-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-163">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d05d-165">**Work.com 구성** 섹션에서 **Work.com 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2d05d-166">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Work.com 구성 섹션](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="2d05d-168">관리자 권한으로 Work.com 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="2d05d-169">**설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="2d05d-170">![설치](./media/active-directory-saas-work-com-tutorial/ic794108.png "설치")</span><span class="sxs-lookup"><span data-stu-id="2d05d-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="2d05d-171">왼쪽 탐색창의 **관리** 섹션에서 **도메인 관리**를 클릭해 관련된 섹션을 확장한 다음 **내 도메인**을 클릭해 **내 도메인** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="2d05d-172">![내 도메인](./media/active-directory-saas-work-com-tutorial/ic767825.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="2d05d-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="2d05d-173">도메인이 올바르게 설정되었는지 확인하려면 “**Step 4 Deployed to Users**(4단계 사용자에게 배포)”에 있는지 확인하고 “**My Domain Settings**(내 도메인 설정)”을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="2d05d-174">![사용자에게 배포된 도메인](./media/active-directory-saas-work-com-tutorial/ic784377.png "사용자에게 배포된 도메인")</span><span class="sxs-lookup"><span data-stu-id="2d05d-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="2d05d-175">Work.com 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="2d05d-176">**설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="2d05d-177">![설치](./media/active-directory-saas-work-com-tutorial/ic794108.png "설치")</span><span class="sxs-lookup"><span data-stu-id="2d05d-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="2d05d-178">**보안 제어** 메뉴를 확장한 다음 **Single Sign-On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="2d05d-179">![Single Sign-On 설정](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="2d05d-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="2d05d-180">**Single Sign-On 설정** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="2d05d-181">![SAML 사용](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML 사용")</span><span class="sxs-lookup"><span data-stu-id="2d05d-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="2d05d-182">a.</span><span class="sxs-lookup"><span data-stu-id="2d05d-182">a.</span></span> <span data-ttu-id="2d05d-183">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="2d05d-184">b.</span><span class="sxs-lookup"><span data-stu-id="2d05d-184">b.</span></span> <span data-ttu-id="2d05d-185">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-185">Click **New**.</span></span>

15. <span data-ttu-id="2d05d-186">**SAML Single Sign-On 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="2d05d-187">![SAML Single Sign-On 설정](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="2d05d-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="2d05d-188">a.</span><span class="sxs-lookup"><span data-stu-id="2d05d-188">a.</span></span> <span data-ttu-id="2d05d-189">**이름** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="2d05d-190">**이름**에 값을 제공하면 **API 이름** 텍스트 상자가 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="2d05d-191">b.</span><span class="sxs-lookup"><span data-stu-id="2d05d-191">b.</span></span> <span data-ttu-id="2d05d-192">**발급자** 텍스트 상자에 Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2d05d-193">c.</span><span class="sxs-lookup"><span data-stu-id="2d05d-193">c.</span></span> <span data-ttu-id="2d05d-194">Azure Portal에서 다운로드한 인증서를 업로드하려면 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="2d05d-195">d.</span><span class="sxs-lookup"><span data-stu-id="2d05d-195">d.</span></span> <span data-ttu-id="2d05d-196">**엔터티 ID** 텍스트 상자에 `https://salesforce-work.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="2d05d-197">e.</span><span class="sxs-lookup"><span data-stu-id="2d05d-197">e.</span></span> <span data-ttu-id="2d05d-198">**SAML ID 유형**으로 **사용자 개체에서 페더레이션 ID를 포함하는 어설션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="2d05d-199">f.</span><span class="sxs-lookup"><span data-stu-id="2d05d-199">f.</span></span> <span data-ttu-id="2d05d-200">**SAML ID 위치**에서 **Subject 문의 NameIdentifier 요소에 ID 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="2d05d-201">g.</span><span class="sxs-lookup"><span data-stu-id="2d05d-201">g.</span></span> <span data-ttu-id="2d05d-202">**ID 공급자 로그인 URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2d05d-203">h.</span><span class="sxs-lookup"><span data-stu-id="2d05d-203">h.</span></span> <span data-ttu-id="2d05d-204">**ID 공급자 로그인 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그아웃 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2d05d-205">i.</span><span class="sxs-lookup"><span data-stu-id="2d05d-205">i.</span></span> <span data-ttu-id="2d05d-206">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="2d05d-207">j.</span><span class="sxs-lookup"><span data-stu-id="2d05d-207">j.</span></span> <span data-ttu-id="2d05d-208">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-208">Click **Save**.</span></span>

16. <span data-ttu-id="2d05d-209">Work.com 클래식 포털의 왼쪽 탐색창에서 **도메인 관리**를 클릭해 관련된 섹션을 확장한 다음 **내 도메인**을 클릭해 **내 도메인** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="2d05d-210">![내 도메인](./media/active-directory-saas-work-com-tutorial/ic794115.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="2d05d-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="2d05d-211">**내 도메인** 페이지의 **로그인 페이지 브랜딩** 섹션에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="2d05d-212">![로그인 페이지 브랜딩](./media/active-directory-saas-work-com-tutorial/ic767826.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="2d05d-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="2d05d-213">**로그인 페이지 브랜딩** 페이지의 **인증 서비스** 섹션에 **SAML SSO 설정** 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="2d05d-214">이름을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="2d05d-215">![로그인 페이지 브랜딩](./media/active-directory-saas-work-com-tutorial/ic784366.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="2d05d-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="2d05d-216">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2d05d-217">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2d05d-218">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2d05d-219">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2d05d-219">Create an Azure AD test user</span></span>
<span data-ttu-id="2d05d-220">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2d05d-222">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="2d05d-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2d05d-223">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d05d-225">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 -> 모든 사용자](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d05d-227">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![추가](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d05d-229">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자 페이지](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d05d-231">a.</span><span class="sxs-lookup"><span data-stu-id="2d05d-231">a.</span></span> <span data-ttu-id="2d05d-232">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d05d-233">b.</span><span class="sxs-lookup"><span data-stu-id="2d05d-233">b.</span></span> <span data-ttu-id="2d05d-234">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d05d-235">c.</span><span class="sxs-lookup"><span data-stu-id="2d05d-235">c.</span></span> <span data-ttu-id="2d05d-236">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2d05d-237">d.</span><span class="sxs-lookup"><span data-stu-id="2d05d-237">d.</span></span> <span data-ttu-id="2d05d-238">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="2d05d-239">Work.com 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2d05d-239">Create a Work.com test user</span></span>
<span data-ttu-id="2d05d-240">Azure Active Directory 사용자가 로그인하려면, Work.com에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="2d05d-241">Work.com의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="2d05d-242">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="2d05d-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="2d05d-243">Work.com 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="2d05d-244">**설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="2d05d-245">![설치](./media/active-directory-saas-work-com-tutorial/IC794108.png "설치")</span><span class="sxs-lookup"><span data-stu-id="2d05d-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="2d05d-246">**사용자 관리 \> 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="2d05d-247">![사용자 관리](./media/active-directory-saas-work-com-tutorial/IC784369.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="2d05d-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="2d05d-248">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-248">Click **New User**.</span></span>
   
    <span data-ttu-id="2d05d-249">![모든 사용자](./media/active-directory-saas-work-com-tutorial/IC794117.png "모든 사용자")</span><span class="sxs-lookup"><span data-stu-id="2d05d-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="2d05d-250">사용자 편집 섹션에서, 관련 텍스트 상자에 프로비전하려는 유효한 Azure AD 계정의 특성에 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="2d05d-251">![사용자 편집](./media/active-directory-saas-work-com-tutorial/ic794118.png "사용자 편집")</span><span class="sxs-lookup"><span data-stu-id="2d05d-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="2d05d-252">a.</span><span class="sxs-lookup"><span data-stu-id="2d05d-252">a.</span></span> <span data-ttu-id="2d05d-253">**이름** 텍스트 상자에 사용자의 **이름**을 **Britta**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="2d05d-254">b.</span><span class="sxs-lookup"><span data-stu-id="2d05d-254">b.</span></span> <span data-ttu-id="2d05d-255">**성** 텍스트 상자에 사용자의 **성**을 **Simon**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="2d05d-256">c.</span><span class="sxs-lookup"><span data-stu-id="2d05d-256">c.</span></span> <span data-ttu-id="2d05d-257">**별칭** 텍스트 상자에 사용자의 **이름**을 **BrittaS**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="2d05d-258">d.</span><span class="sxs-lookup"><span data-stu-id="2d05d-258">d.</span></span> <span data-ttu-id="2d05d-259">**전자 메일** 텍스트 상자에 사용자의 **이메일 주소** **Brittasimon@contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="2d05d-260">e.</span><span class="sxs-lookup"><span data-stu-id="2d05d-260">e.</span></span> <span data-ttu-id="2d05d-261">**사용자 이름** 텍스트 상자에 사용자의 사용자 이름(예: **Brittasimon@contoso.com**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="2d05d-262">f.</span><span class="sxs-lookup"><span data-stu-id="2d05d-262">f.</span></span> <span data-ttu-id="2d05d-263">**Nick Name**(애칭) 텍스트 상자에 사용자의 **애칭** **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="2d05d-264">g.</span><span class="sxs-lookup"><span data-stu-id="2d05d-264">g.</span></span> <span data-ttu-id="2d05d-265">**역할**, **사용자 라이선스** 및 **프로필**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="2d05d-266">h.</span><span class="sxs-lookup"><span data-stu-id="2d05d-266">h.</span></span> <span data-ttu-id="2d05d-267">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="2d05d-268">Azure AD 계정 보유자에게 계정 확인 링크가 포함한 전자 메일이 발송되며, 확인을 마치면 계정이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2d05d-269">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2d05d-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="2d05d-270">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Work.com에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2d05d-272">**Britta Simon을 Work.com에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d05d-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="2d05d-273">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2d05d-275">응용 프로그램 목록에서 **Work.com**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-275">In the applications list, select **Work.com**.</span></span>

    ![앱 목록의 Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="2d05d-277">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-277">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2d05d-279">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-279">Click **Add** button.</span></span> <span data-ttu-id="2d05d-280">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2d05d-282">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2d05d-283">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d05d-284">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2d05d-285">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2d05d-285">Test single sign-on</span></span>

<span data-ttu-id="2d05d-286">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2d05d-287">액세스 패널에서 Work.com 타일을 클릭하면 Work.com 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d05d-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="2d05d-288">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d05d-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d05d-289">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2d05d-289">Additional resources</span></span>

* [<span data-ttu-id="2d05d-290">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="2d05d-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d05d-291">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2d05d-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

