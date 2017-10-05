---
title: "자습서: ServiceNow와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 ServiceNow 및 ServiceNow Express 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="4a0d2-103">자습서: ServiceNow와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4a0d2-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="4a0d2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ServiceNow 및 ServiceNow Express를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a0d2-105">ServiceNow 및 ServiceNow Express를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4a0d2-106">ServiceNow 및 ServiceNow Express에 대한 액세스 권한이 있는 사용자는 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="4a0d2-107">사용자가 해당 Azure AD 계정으로 ServiceNow 및 ServiceNow Express에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="4a0d2-108">단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4a0d2-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a0d2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4a0d2-110">Prerequisites</span></span>
<span data-ttu-id="4a0d2-111">ServiceNow 및 ServiceNow Express와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="4a0d2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4a0d2-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4a0d2-113">ServiceNow의 경우 ServiceNow의 인스턴스 또는 테넌트, Calgary 버전 이상</span><span class="sxs-lookup"><span data-stu-id="4a0d2-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="4a0d2-114">ServiceNow Express의 경우 ServiceNow Express의 인스턴스, Helsinki 버전 이상</span><span class="sxs-lookup"><span data-stu-id="4a0d2-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="4a0d2-115">ServiceNow 테넌트에서 [여러 공급자 Single Sign-On 플러그 인](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0)을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="4a0d2-116">[서비스 요청을 제출](https://hi.service-now.com)하면 이렇게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="4a0d2-117">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="4a0d2-118">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4a0d2-119">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4a0d2-120">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a0d2-121">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4a0d2-121">Scenario description</span></span>
<span data-ttu-id="4a0d2-122">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a0d2-123">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a0d2-124">갤러리에서 ServiceNow 추가</span><span class="sxs-lookup"><span data-stu-id="4a0d2-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="4a0d2-125">ServiceNow 또는 ServiceNow Express에 대한 Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4a0d2-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="4a0d2-126">갤러리에서 ServiceNow 추가</span><span class="sxs-lookup"><span data-stu-id="4a0d2-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="4a0d2-127">ServiceNow 또는 ServiceNow Express의 Azure AD 통합을 구성하려면 갤러리의 ServiceNow를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="4a0d2-128">**갤러리에서 ServiceNow를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4a0d2-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4a0d2-129">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="4a0d2-131">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4a0d2-132">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2]
4. <span data-ttu-id="4a0d2-134">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-134">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="4a0d2-136">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4]
6. <span data-ttu-id="4a0d2-138">검색 상자에 **ServiceNow**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="4a0d2-140">결과 창에서 **ServiceNow**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a0d2-142">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4a0d2-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a0d2-143">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ServiceNow 또는 ServiceNow Express에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a0d2-144">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ServiceNow 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="4a0d2-145">즉, Azure AD 사용자와 ServiceNow의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="4a0d2-146">이 연결 관계는 Azure AD의 **사용자 이름** 값을 ServiceNow의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="4a0d2-147">ServiceNow에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4a0d2-148">**[ServiceNow에 대한 Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on-for-servicenow)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4a0d2-149">**[ServiceNow Express에 대한 Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="4a0d2-150">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="4a0d2-151">**[ServiceNow 테스트 사용자 만들기](#creating-a-servicenow-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ServiceNow에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="4a0d2-152">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="4a0d2-153">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0d2-154">ServiceNow를 구성하려는 경우 2단계를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="4a0d2-155">마찬가지로 ServiceNow Express를 구성하려는 경우 1단계를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="4a0d2-156">ServiceNow에 대한 Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4a0d2-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="4a0d2-157">Azure AD 클래식 포털의 **ServiceNow** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="4a0d2-158">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="4a0d2-159">**ServiceNow에 대한 사용자 로그온 방법 선택** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="4a0d2-160">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="4a0d2-161">**앱 설정 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4a0d2-162">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC769497.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4a0d2-163">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-163">a.</span></span> <span data-ttu-id="4a0d2-164">**ServiceNow 로그인 URL** 텍스트 상자에 다음 패턴 `https://<instance-name>.service-now.com`을 따라 사용자가 ServiceNow 응용 프로그램에 로그인하는 데 사용한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4a0d2-165">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-165">b.</span></span> <span data-ttu-id="4a0d2-166">**식별자** 텍스트 상자에 다음 패턴 `https://<instance-name>.service-now.com`을 따라 사용자가 ServiceNow 응용 프로그램에 로그인하는 데 사용한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4a0d2-167">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-167">c.</span></span> <span data-ttu-id="4a0d2-168">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="4a0d2-168">Click **Next**</span></span>

4. <span data-ttu-id="4a0d2-169">Azure AD에서 SAML 기반 인증용으로 ServiceNow를 자동으로 구성하도록 하려면 ServiceNow 인스턴스 이름, 관리자 사용자 이름 및 관리자 암호를 **Single Sign-On 자동 구성** 양식에 입력하고 *구성*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="4a0d2-170">입력하는 관리자 사용자 이름에 ServiceNow의 **security_admin** 역할이 할당되어 있어야 이 절차를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="4a0d2-171">이 방법을 사용하지 않고 ServiceNow가 SAML ID 공급자로 Azure AD를 사용하도록 수동으로 구성하려면 **응용 프로그램을 Single Sign-On에 대해 수동 구성**을 클릭하고 **다음**을 클릭하여 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="4a0d2-172">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="4a0d2-173">**ServiceNow에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭하고 컴퓨터에 로컬로 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="4a0d2-174">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="4a0d2-175">ServiceNow 응용 프로그램에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="4a0d2-176">다음 단계를 따라 *통합 - 여러 공급자 Single Sign-On 설치 관리자* 플러그 인을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="4a0d2-177">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-177">a.</span></span> <span data-ttu-id="4a0d2-178">왼쪽 탐색 창에서 **시스템 정의** 섹션으로 이동한 다음 **플러그 인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="4a0d2-179">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "플러그 인 활성화")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="4a0d2-180">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-180">b.</span></span> <span data-ttu-id="4a0d2-181">*통합 - 여러 공급자 Single Sign-On 설치 관리자*를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="4a0d2-182">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "플러그 인 활성화")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="4a0d2-183">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-183">c.</span></span> <span data-ttu-id="4a0d2-184">플러그 인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-184">Select the plugin.</span></span> <span data-ttu-id="4a0d2-185">마우스 오른쪽을 클릭하고 **활성화/업그레이드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="4a0d2-186">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-186">d.</span></span> <span data-ttu-id="4a0d2-187">**활성화** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="4a0d2-188">왼쪽의 탐색 창에서 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="4a0d2-189">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="4a0d2-190">**여러 공급자 SSO 속성** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="4a0d2-191">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4a0d2-192">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-192">a.</span></span> <span data-ttu-id="4a0d2-193">**여러 공급자 SSO 사용**을 **예**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="4a0d2-194">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-194">b.</span></span> <span data-ttu-id="4a0d2-195">**디버그 로깅에 여러 공급자 SSO 통합을 사용**하도록 설정을 **예**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="4a0d2-196">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-196">c.</span></span> <span data-ttu-id="4a0d2-197">**...하는 사용자 테이블의 필드** 텍스트 상자에서 **user_name**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="4a0d2-198">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-198">d.</span></span> <span data-ttu-id="4a0d2-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-199">Click **Save**.</span></span>

10. <span data-ttu-id="4a0d2-200">왼쪽의 탐색 창에서 **x509 Certificates**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="4a0d2-201">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="4a0d2-202">**X.509 인증서** 대화 상자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="4a0d2-203">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="4a0d2-204">**X.509 Certificates** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="4a0d2-205">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="4a0d2-206">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-206">a.</span></span> <span data-ttu-id="4a0d2-207">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-207">Click **New**.</span></span>
    
     <span data-ttu-id="4a0d2-208">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-208">b.</span></span> <span data-ttu-id="4a0d2-209">**이름** 텍스트 상자에서 구성할 이름을 입력합니다(예: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="4a0d2-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="4a0d2-210">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-210">c.</span></span> <span data-ttu-id="4a0d2-211">**활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-211">Select **Active**.</span></span>
    
     <span data-ttu-id="4a0d2-212">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-212">d.</span></span> <span data-ttu-id="4a0d2-213">**형식**으로 **PEM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="4a0d2-214">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-214">e.</span></span> <span data-ttu-id="4a0d2-215">**형식**으로 **저장소 인증서 신뢰**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="4a0d2-216">f.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-216">f.</span></span> <span data-ttu-id="4a0d2-217">Base64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **PEM 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="4a0d2-218">g.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-218">g.</span></span> <span data-ttu-id="4a0d2-219">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-219">Click **Update**.</span></span>

13. <span data-ttu-id="4a0d2-220">왼쪽의 탐색 창에서 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="4a0d2-221">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="4a0d2-222">**ID 공급자** 대화 상자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="4a0d2-223">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="4a0d2-224">**ID 공급자** 대화 상자에서 **SAML2 Update1?**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="4a0d2-225">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="4a0d2-226">SAML2 Update1 속성 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="4a0d2-227">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="4a0d2-228">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-228">a.</span></span> <span data-ttu-id="4a0d2-229">**이름** 텍스트 상자에서 구성할 이름을 입력합니다(예: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="4a0d2-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="4a0d2-230">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-230">b.</span></span> <span data-ttu-id="4a0d2-231">ServiceNow 배포에서 사용자를 고유하게 식별하는 데 사용되는 필드에 따라 **사용자 필드** 텍스트 상자에 **email** 또는 **user_name**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="4a0d2-232">Azure 클래식 포털의 **ServiceNow > 특성 > Single Sign-On** 섹션으로 이동한 다음 원하는 필드를 **nameidentifier** 특성에 매핑하면 Azure AD 사용자 ID(사용자 계정 이름) 또는 전자 메일 주소를 SAML 토큰의 고유 식별자로 내보내도록 Azure AD를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="4a0d2-233">Azure AD에서 선택한 특성에 대해 저장되는 값(예: 사용자 계정 이름)은 입력하는 필드에 대해 ServiceNow에 저장된 값(예: user_name)과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="4a0d2-234">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-234">c.</span></span> <span data-ttu-id="4a0d2-235">Azure AD 클래식 포털에서 **ID 공급자 ID** 값을 복사한 다음 **ID 공급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="4a0d2-236">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-236">d.</span></span> <span data-ttu-id="4a0d2-237">Azure AD 클래식 포털에서 **인증 요청 URL** 값을 복사한 다음 **ID 공급자의 AuthnRequest** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="4a0d2-238">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-238">e.</span></span> <span data-ttu-id="4a0d2-239">Azure AD 클래식 포털에서 **Single Sign-Out 서비스 URL** 값을 복사한 다음 **ID 공급자의 SingleLogoutRequest 텍스트 상자**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="4a0d2-240">f.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-240">f.</span></span> <span data-ttu-id="4a0d2-241">**ServiceNow 홈페이지** 텍스트 상자에 ServiceNow 인스턴스 홈페이지의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a0d2-242">ServiceNow 인스턴스 홈페이지의 URL은 **ServieNow 테넌트 URL** 및 **/navpage.do**의 연결입니다(예: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="4a0d2-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="4a0d2-243">g.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-243">g.</span></span> <span data-ttu-id="4a0d2-244">**엔터티 ID/발급자** 텍스트 상자에 ServiceNow 테넌트의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="4a0d2-245">h.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-245">h.</span></span> <span data-ttu-id="4a0d2-246">**대상 URL** 텍스트 상자에 ServiceNow 테넌트의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="4a0d2-247">i.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-247">i.</span></span> <span data-ttu-id="4a0d2-248">**IDP의 SingleLogoutRequest에 대한 프로토콜 바인딩** 텍스트 상자에 **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="4a0d2-249">j.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-249">j.</span></span> <span data-ttu-id="4a0d2-250">NameID 정책 텍스트 상자에 **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="4a0d2-251">k.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-251">k.</span></span> <span data-ttu-id="4a0d2-252">**AuthnContextClass 만들기**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="4a0d2-253">l.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-253">l.</span></span> <span data-ttu-id="4a0d2-254">**AuthnContextClassRef 메서드**에 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="4a0d2-255">클라우드 전용 조직인 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="4a0d2-256">인증으로 온-프레미스 ADFS 또는 MFA를 사용하는 경우 이 값을 구성하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="4a0d2-257">m.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-257">m.</span></span> <span data-ttu-id="4a0d2-258">**시계 기울이기** 텍스트 상자에 **60**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="4a0d2-259">n.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-259">n.</span></span> <span data-ttu-id="4a0d2-260">**Single Sign On 스크립트**로 **MultiSSO_SAML2_Update1**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="4a0d2-261">o.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-261">o.</span></span> <span data-ttu-id="4a0d2-262">**x509 인증서**로 이전 단계에서 만든 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="4a0d2-263">p.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-263">p.</span></span> <span data-ttu-id="4a0d2-264">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="4a0d2-265">Azure AD 클래식 포털에서 Single Sign-On을 구성했음을 확인한다는 확인란을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="4a0d2-266">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="4a0d2-267">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="4a0d2-268">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="4a0d2-269">ServiceNow Express에 대한 Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4a0d2-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="4a0d2-270">Azure AD 클래식 포털의 **ServiceNow** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="4a0d2-271">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="4a0d2-272">**ServiceNow에 대한 사용자 로그온 방법 선택** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="4a0d2-273">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="4a0d2-274">**앱 설정 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4a0d2-275">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC769497.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4a0d2-276">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-276">a.</span></span> <span data-ttu-id="4a0d2-277">**ServiceNow 로그인 URL** 텍스트 상자에 다음 패턴 `https://<instance-name>.service-now.com`을 따라 사용자가 ServiceNow 응용 프로그램에 로그인하는 데 사용한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4a0d2-278">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-278">b.</span></span> <span data-ttu-id="4a0d2-279">**발급자 URL** 텍스트 상자에 다음 패턴 `https://<instance-name>.service-now.com`을 따라 사용자가 ServiceNow 응용 프로그램에 로그인하는 데 사용한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4a0d2-280">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-280">c.</span></span> <span data-ttu-id="4a0d2-281">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="4a0d2-281">Click **Next**</span></span>

4. <span data-ttu-id="4a0d2-282">**Single Sign-On에 대한 응용 프로그램을 수동으로 구성**을 클릭한 후 **다음**을 클릭하고 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="4a0d2-283">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="4a0d2-284">**ServiceNow에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭하고 컴퓨터에 로컬로 인증서 파일을 저장한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="4a0d2-285">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="4a0d2-286">ServiceNow Express 응용 프로그램에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="4a0d2-287">왼쪽 탐색 창에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="4a0d2-288">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="4a0d2-289">**Single Sign-on** 대화 상자에서 오른쪽 위의 구성 아이콘을 클릭하고 다음 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="4a0d2-290">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4a0d2-291">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-291">a.</span></span> <span data-ttu-id="4a0d2-292">**여러 공급자 SSO 사용**을 오른쪽으로 설정/해제합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="4a0d2-293">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-293">b.</span></span> <span data-ttu-id="4a0d2-294">**여러 공급자 SSO 통합에 대한 디버그 로깅 활성화**를 오른쪽으로 설정/해제합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="4a0d2-295">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-295">c.</span></span> <span data-ttu-id="4a0d2-296">**...하는 사용자 테이블의 필드** 텍스트 상자에서 **user_name**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="4a0d2-297">**Single Sign-On** 대화 상자에서 **새 인증서 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="4a0d2-298">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="4a0d2-299">**X.509 Certificates** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="4a0d2-300">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="4a0d2-301">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-301">a.</span></span> <span data-ttu-id="4a0d2-302">**이름** 텍스트 상자에서 구성할 이름을 입력합니다(예: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="4a0d2-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="4a0d2-303">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-303">b.</span></span> <span data-ttu-id="4a0d2-304">**활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-304">Select **Active**.</span></span>
    
    <span data-ttu-id="4a0d2-305">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-305">c.</span></span> <span data-ttu-id="4a0d2-306">**형식**으로 **PEM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="4a0d2-307">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-307">d.</span></span> <span data-ttu-id="4a0d2-308">**형식**으로 **저장소 인증서 신뢰**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="4a0d2-309">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-309">e.</span></span> <span data-ttu-id="4a0d2-310">다운로드한 인증서에서 Base64로 인코딩된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4a0d2-311">자세한 내용은 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="4a0d2-312">f.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-312">f.</span></span> <span data-ttu-id="4a0d2-313">Base64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **PEM 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="4a0d2-314">g.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-314">g.</span></span> <span data-ttu-id="4a0d2-315">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-315">Click **Update**.</span></span>
11. <span data-ttu-id="4a0d2-316">**Single Sign-On** 대화 상자에서 **새 IdP 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="4a0d2-317">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="4a0d2-318">**새 ID 공급자 추가** 대화 상자의 **ID 공급자 구성** 아래에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="4a0d2-319">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="4a0d2-320">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-320">a.</span></span> <span data-ttu-id="4a0d2-321">**이름** 텍스트 상자에서 구성할 이름을 입력합니다(예: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="4a0d2-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="4a0d2-322">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-322">b.</span></span> <span data-ttu-id="4a0d2-323">Azure AD 클래식 포털에서 **ID 공급자 ID** 값을 복사한 다음 **ID 공급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="4a0d2-324">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-324">c.</span></span> <span data-ttu-id="4a0d2-325">Azure AD 클래식 포털에서 **인증 요청 URL** 값을 복사한 다음 **ID 공급자의 AuthnRequest** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="4a0d2-326">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-326">d.</span></span> <span data-ttu-id="4a0d2-327">Azure AD 클래식 포털에서 **Single Sign-Out 서비스 URL** 값을 복사한 다음 **ID 공급자의 SingleLogoutRequest 텍스트 상자**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="4a0d2-328">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-328">e.</span></span> <span data-ttu-id="4a0d2-329">**ID 공급자 인증서**로 이전 단계에서 만든 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="4a0d2-330">**고급 설정**을 클릭하고 **추가 ID 공급자 속성** 아래에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="4a0d2-331">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a0d2-332">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-332">a.</span></span> <span data-ttu-id="4a0d2-333">**IDP의 SingleLogoutRequest에 대한 프로토콜 바인딩** 텍스트 상자에 **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="4a0d2-334">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-334">b.</span></span> <span data-ttu-id="4a0d2-335">**NameID 정책** 텍스트 상자에 **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="4a0d2-336">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-336">c.</span></span> <span data-ttu-id="4a0d2-337">**AuthnContextClassRef 메서드**에, **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="4a0d2-338">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-338">d.</span></span> <span data-ttu-id="4a0d2-339">**AuthnContextClass 만들기**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="4a0d2-340">**추가 서비스 공급자 속성** 아래에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="4a0d2-341">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a0d2-342">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-342">a.</span></span> <span data-ttu-id="4a0d2-343">**ServiceNow 홈페이지** 텍스트 상자에 ServiceNow 인스턴스 홈페이지의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="4a0d2-344">ServiceNow 인스턴스 홈페이지의 URL은 **ServieNow 테넌트 URL** 및 **/navpage.do**의 연결입니다(예: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="4a0d2-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="4a0d2-345">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-345">b.</span></span> <span data-ttu-id="4a0d2-346">**엔터티 ID/발급자** 텍스트 상자에 ServiceNow 테넌트의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="4a0d2-347">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-347">c.</span></span> <span data-ttu-id="4a0d2-348">**대상 URI** 텍스트 상자에 ServiceNow 테넌트의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="4a0d2-349">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-349">d.</span></span> <span data-ttu-id="4a0d2-350">**시계 기울이기** 텍스트 상자에 **60**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="4a0d2-351">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-351">e.</span></span> <span data-ttu-id="4a0d2-352">ServiceNow 배포에서 사용자를 고유하게 식별하는 데 사용되는 필드에 따라 **사용자 필드** 텍스트 상자에 **email** 또는 **user_name**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="4a0d2-353">Azure 클래식 포털의 **ServiceNow > 특성 > Single Sign-On** 섹션으로 이동한 다음 원하는 필드를 **nameidentifier** 특성에 매핑하면 Azure AD 사용자 ID(사용자 계정 이름) 또는 전자 메일 주소를 SAML 토큰의 고유 식별자로 내보내도록 Azure AD를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="4a0d2-354">Azure AD에서 선택한 특성에 대해 저장되는 값(예: 사용자 계정 이름)은 입력하는 필드에 대해 ServiceNow에 저장된 값(예: user_name)과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="4a0d2-355">f.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-355">f.</span></span> <span data-ttu-id="4a0d2-356">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-356">Click **Save**.</span></span> 

3. <span data-ttu-id="4a0d2-357">Azure AD 클래식 포털에서 Single Sign-On을 구성했음을 확인한다는 확인란을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="4a0d2-358">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="4a0d2-359">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="4a0d2-360">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="4a0d2-361">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="4a0d2-361">Configuring user provisioning</span></span>
<span data-ttu-id="4a0d2-362">이 섹션에서는 ServiceNow에 Active Directory 사용자 계정을 프로비저닝할 수 있도록 설정하는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="4a0d2-363">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="4a0d2-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="4a0d2-364">Azure 관리 클래식 포털의 **ServiceNow** 응용 프로그램 통합 페이지에서 **사용자 프로비전 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="4a0d2-365">![사용자 프로비전](./media/active-directory-saas-servicenow-tutorial/IC769498.png "사용자 프로비전")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="4a0d2-366">**ServiceNow 자격 증명을 입력하여 자동 사용자 프로비전 사용** 페이지에서 다음 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="4a0d2-367">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-367">a.</span></span> <span data-ttu-id="4a0d2-368">**ServiceNow 인스턴스 이름** 텍스트 상자에 ServiceNow 인스턴스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="4a0d2-369">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-369">b.</span></span> <span data-ttu-id="4a0d2-370">**ServiceNow 관리자 사용자 이름** 텍스트 상자에 ServiceNow 관리자 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="4a0d2-371">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-371">c.</span></span> <span data-ttu-id="4a0d2-372">**ServiceNow 관리자 암호** 텍스트 상자에 이 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="4a0d2-373">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-373">d.</span></span> <span data-ttu-id="4a0d2-374">**유효성 검사** 를 클릭하여 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="4a0d2-375">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-375">e.</span></span> <span data-ttu-id="4a0d2-376">**다음** 단추를 클릭하여 **다음 단계** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="4a0d2-377">f.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-377">f.</span></span> <span data-ttu-id="4a0d2-378">이 응용 프로그램에 모든 사용자를 프로비전하려는 경우 "**이 응용 프로그램에 대한 디렉터리의 모든 사용자 계정을 자동으로 프로비전**"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="4a0d2-379">![다음 단계](./media/active-directory-saas-servicenow-tutorial/IC698804.png "다음 단계")</span><span class="sxs-lookup"><span data-stu-id="4a0d2-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="4a0d2-380">g.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-380">g.</span></span> <span data-ttu-id="4a0d2-381">**다음 단계** 페이지에서 **완료**를 클릭하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a0d2-382">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4a0d2-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a0d2-383">이 섹션에서는 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="4a0d2-385">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="4a0d2-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4a0d2-386">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="4a0d2-388">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4a0d2-389">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a0d2-391">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="4a0d2-393">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="4a0d2-395">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-395">a.</span></span> <span data-ttu-id="4a0d2-396">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="4a0d2-397">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-397">b.</span></span> <span data-ttu-id="4a0d2-398">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="4a0d2-399">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-399">c.</span></span> <span data-ttu-id="4a0d2-400">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-400">Click **Next**.</span></span>

6. <span data-ttu-id="4a0d2-401">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="4a0d2-403">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-403">a.</span></span> <span data-ttu-id="4a0d2-404">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="4a0d2-405">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-405">b.</span></span> <span data-ttu-id="4a0d2-406">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="4a0d2-407">c.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-407">c.</span></span> <span data-ttu-id="4a0d2-408">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="4a0d2-409">d.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-409">d.</span></span> <span data-ttu-id="4a0d2-410">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="4a0d2-411">e.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-411">e.</span></span> <span data-ttu-id="4a0d2-412">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-412">Click **Next**.</span></span>

7. <span data-ttu-id="4a0d2-413">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="4a0d2-415">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="4a0d2-417">a.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-417">a.</span></span> <span data-ttu-id="4a0d2-418">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="4a0d2-419">b.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-419">b.</span></span> <span data-ttu-id="4a0d2-420">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="4a0d2-421">ServiceNow 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4a0d2-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="4a0d2-422">이 섹션에서는 ServiceNow에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="4a0d2-423">이 섹션에서는 ServiceNow에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="4a0d2-424">ServiceNow 또는 ServiceNow Express 계정에 사용자를 추가하는 방법을 모르는 경우 ServiceNow 지원 팀에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4a0d2-425">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="4a0d2-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="4a0d2-426">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ServiceNow에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4a0d2-428">**Britta Simon을 ServiceNow에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4a0d2-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="4a0d2-429">클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![사용자 할당][201] 

2. <span data-ttu-id="4a0d2-431">응용 프로그램 목록에서 **ServiceNow**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="4a0d2-433">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-433">In the menu on the top, click **Users**.</span></span>
   
    ![사용자 할당][203] 

4. <span data-ttu-id="4a0d2-435">모든 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="4a0d2-436">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="4a0d2-438">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4a0d2-438">Testing single sign-on</span></span>
<span data-ttu-id="4a0d2-439">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4a0d2-440">액세스 패널에서 ServiceNow 타일을 클릭하면 ServiceNow 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0d2-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a0d2-441">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4a0d2-441">Additional resources</span></span>
* [<span data-ttu-id="4a0d2-442">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="4a0d2-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a0d2-443">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4a0d2-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
