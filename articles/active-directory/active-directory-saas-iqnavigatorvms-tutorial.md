---
title: "자습서: IQNavigator VMS와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 IQNavigator VMS 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 1164723a171843541098f6adbda0e65f7e82a0cb
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="55ff8-103">자습서: IQNavigator VMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="55ff8-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="55ff8-104">이 자습서에서는 Azure AD(Azure Active Directory)와 IQNavigator VMS를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-104">In this tutorial, you learn how to integrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55ff8-105">IQNavigator VMS를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-105">Integrating IQNavigator VMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="55ff8-106">IQNavigator VMS에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-106">You can control in Azure AD who has access to IQNavigator VMS</span></span>
- <span data-ttu-id="55ff8-107">사용자가 자신의 Azure AD 계정으로 IQNavigator VMS에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-107">You can enable your users to automatically get signed-on to IQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55ff8-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="55ff8-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ff8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55ff8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="55ff8-110">Prerequisites</span></span>

<span data-ttu-id="55ff8-111">IQNavigator VMS와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-111">To configure Azure AD integration with IQNavigator VMS, you need the following items:</span></span>

- <span data-ttu-id="55ff8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="55ff8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55ff8-113">IQNavigator VMS Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="55ff8-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55ff8-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55ff8-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55ff8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="55ff8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55ff8-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55ff8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="55ff8-118">Scenario description</span></span>
<span data-ttu-id="55ff8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55ff8-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55ff8-121">갤러리에서 IQNavigator VMS 추가</span><span class="sxs-lookup"><span data-stu-id="55ff8-121">Adding IQNavigator VMS from the gallery</span></span>
2. <span data-ttu-id="55ff8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="55ff8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-the-gallery"></a><span data-ttu-id="55ff8-123">갤러리에서 IQNavigator VMS 추가</span><span class="sxs-lookup"><span data-stu-id="55ff8-123">Adding IQNavigator VMS from the gallery</span></span>
<span data-ttu-id="55ff8-124">IQNavigator VMS가 Azure AD에 통합되도록 구성하려면 갤러리에서 IQNavigator VMS를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-124">To configure the integration of IQNavigator VMS into Azure AD, you need to add IQNavigator VMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="55ff8-125">**갤러리에서 IQNavigator VMS를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="55ff8-125">**To add IQNavigator VMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="55ff8-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55ff8-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="55ff8-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="55ff8-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="55ff8-133">검색 상자에서 **IQNavigator VMS**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-133">In the search box, type **IQNavigator VMS**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="55ff8-135">결과 창에서 **IQNavigator VMS**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-135">In the results panel, select **IQNavigator VMS**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55ff8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="55ff8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55ff8-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 IQNavigator VMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55ff8-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 IQNavigator VMS 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IQNavigator VMS is to a user in Azure AD.</span></span> <span data-ttu-id="55ff8-140">즉, Azure AD 사용자와 IQNavigator VMS의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-140">In other words, a link relationship between an Azure AD user and the related user in IQNavigator VMS needs to be established.</span></span>

<span data-ttu-id="55ff8-141">IQNavigator VMS에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-141">In IQNavigator VMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="55ff8-142">IQNavigator VMS에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-142">To configure and test Azure AD single sign-on with IQNavigator VMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="55ff8-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="55ff8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55ff8-145">**[IQNavigator VMS 테스트 사용자 만들기](#creating-a-iqnavigator-vms-test-user)** - Britta Simon의 Azure AD 표현과 연결된 사용자를 IQNavigator VMS에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - to have a counterpart of Britta Simon in IQNavigator VMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="55ff8-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55ff8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55ff8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="55ff8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55ff8-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 IQNavigator VMS 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="55ff8-150">**IQNavigator VMS에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="55ff8-150">**To configure Azure AD single sign-on with IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="55ff8-151">Azure Portal의 **IQNavigator VMS** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-151">In the Azure portal, on the **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="55ff8-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="55ff8-155">**IQNavigator VMS 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-155">On the **IQNavigator VMS Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="55ff8-157">a.</span><span class="sxs-lookup"><span data-stu-id="55ff8-157">a.</span></span> <span data-ttu-id="55ff8-158">**식별자** 텍스트 상자에 URL `iqn.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-158">In the **Identifier** textbox, type the URL:`iqn.com`</span></span>

    <span data-ttu-id="55ff8-159">b.</span><span class="sxs-lookup"><span data-stu-id="55ff8-159">b.</span></span> <span data-ttu-id="55ff8-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="55ff8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="55ff8-161">**고급 URL 설정 표시**를 확인하고, 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-161">Check **Show advanced URL settings**, perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="55ff8-163">**릴레이 상태** 텍스트 상자에서 `https://<subdomain>.iqnavigator.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-163">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55ff8-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-164">These values are not real.</span></span> <span data-ttu-id="55ff8-165">실제 회신 URL 및 릴레이 상태로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-165">Update these values with the actual Reply URL and Relay state.</span></span> <span data-ttu-id="55ff8-166">이러한 값을 얻으려면 [IQNavigator VMS 클라이언트 지원 팀](https://www.beeline.com/iqn-product-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="55ff8-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) to get these values.</span></span> 

5. <span data-ttu-id="55ff8-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55ff8-169">**메타데이터** URL을 생성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-169">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="55ff8-170">a.</span><span class="sxs-lookup"><span data-stu-id="55ff8-170">a.</span></span> <span data-ttu-id="55ff8-171">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-171">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="55ff8-173">b.</span><span class="sxs-lookup"><span data-stu-id="55ff8-173">b.</span></span> <span data-ttu-id="55ff8-174">**끝점**을 클릭하여 **끝점** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-174">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="55ff8-176">c.</span><span class="sxs-lookup"><span data-stu-id="55ff8-176">c.</span></span> <span data-ttu-id="55ff8-177">복사 단추를 클릭하여 **페더레이션 메타데이터 문서** URL을 복사하여 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-177">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="55ff8-179">d.</span><span class="sxs-lookup"><span data-stu-id="55ff8-179">d.</span></span> <span data-ttu-id="55ff8-180">이제 **IQNavigator VMS**의 속성 페이지로 이동하고 **복사** 단추를 사용하여 **응용 프로그램 ID**를 복사하여 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-180">Now go to the property page of **IQNavigator VMS** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="55ff8-182">e.</span><span class="sxs-lookup"><span data-stu-id="55ff8-182">e.</span></span> <span data-ttu-id="55ff8-183">`<FEDERATION METADATA DOCUMENT url>?appid=<application id>` 패턴을 사용하여 **메타데이터 URL**을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-183">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="55ff8-184">IQNavigator 응용 프로그램은 이름 식별자 클레임에 고유한 사용자 ID 값을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-184">IQNavigator application expect the unique user identifier value in the Name Identifier claim.</span></span> <span data-ttu-id="55ff8-185">고객은 이름 식별자 클레임에 대한 올바른 값을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-185">Customer can map the correct value for the Name Identifier claim.</span></span> <span data-ttu-id="55ff8-186">이 경우 데모 목적으로 user.UserPrincipalName을 매핑했습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-186">In this case we have mapped the user.UserPrincipalName for the demo purpose.</span></span> <span data-ttu-id="55ff8-187">그러나 조직 설정에 따라 올바른 값을 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-187">But according to your organization settings you should map the correct value for it.</span></span>   

    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="55ff8-189">**IQNavigator VMS 구성** 섹션에서 **IQNavigator VMS 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-189">On the **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="55ff8-190">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-190">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="55ff8-192">**IQNavigator VMS** 쪽에서 Single Sign-On을 구성하려면 **메타데이터 URL**, **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 [IQNavigator VMS 지원 팀](https://www.beeline.com/iqn-product-support/)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-192">To configure single sign-on on **IQNavigator VMS** side, you need to send the **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="55ff8-193">그러면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="55ff8-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="55ff8-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="55ff8-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55ff8-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="55ff8-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="55ff8-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="55ff8-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="55ff8-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="55ff8-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55ff8-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55ff8-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55ff8-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55ff8-209">a.</span><span class="sxs-lookup"><span data-stu-id="55ff8-209">a.</span></span> <span data-ttu-id="55ff8-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55ff8-211">b.</span><span class="sxs-lookup"><span data-stu-id="55ff8-211">b.</span></span> <span data-ttu-id="55ff8-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55ff8-213">c.</span><span class="sxs-lookup"><span data-stu-id="55ff8-213">c.</span></span> <span data-ttu-id="55ff8-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="55ff8-215">d.</span><span class="sxs-lookup"><span data-stu-id="55ff8-215">d.</span></span> <span data-ttu-id="55ff8-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="55ff8-217">IQNavigator VMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="55ff8-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="55ff8-218">이 섹션의 목적은 IQNavigator VMS에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-218">The objective of this section is to create a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="55ff8-219">IQNavigator VMS 계정에서 사용자를 추가하려면 [IQNavigator VMS 지원 팀](https://www.beeline.com/iqn-product-support/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="55ff8-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) to add the users in the IQNavigator VMS account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="55ff8-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="55ff8-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="55ff8-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 IQNavigator VMS에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IQNavigator VMS.</span></span>

![사용자 할당][200] 

<span data-ttu-id="55ff8-223">**Britta Simon을 IQNavigator VMS에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="55ff8-223">**To assign Britta Simon to IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="55ff8-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="55ff8-226">응용 프로그램 목록에서 **IQNavigator VMS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-226">In the applications list, select **IQNavigator VMS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="55ff8-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-228">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="55ff8-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-230">Click **Add** button.</span></span> <span data-ttu-id="55ff8-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="55ff8-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="55ff8-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55ff8-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55ff8-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="55ff8-236">Testing single sign-on</span></span>

<span data-ttu-id="55ff8-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="55ff8-238">액세스 패널에서 IQNavigator VMS 타일을 클릭하면 IQNavigator VMS 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ff8-238">When you click the IQNavigator VMS tile in the Access Panel, you should get automatically signed-on to your IQNavigator VMS application.</span></span>
<span data-ttu-id="55ff8-239">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ff8-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55ff8-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="55ff8-240">Additional resources</span></span>

* [<span data-ttu-id="55ff8-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="55ff8-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55ff8-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="55ff8-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

