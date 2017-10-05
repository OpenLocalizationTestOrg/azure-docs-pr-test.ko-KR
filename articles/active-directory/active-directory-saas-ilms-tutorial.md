---
title: "자습서: Azure Active Directory와 iLMS 통합 | Microsoft Docs"
description: "Azure Active Directory와 iLMS 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="b309d-103">자습서: iLMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b309d-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="b309d-104">이 자습서에서는 Azure AD(Azure Active Directory)와 iLMS를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b309d-105">iLMS를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b309d-106">iLMS에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="b309d-107">사용자의 Azure AD 계정으로 iLMS에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b309d-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b309d-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b309d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b309d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b309d-110">Prerequisites</span></span>

<span data-ttu-id="b309d-111">iLMS와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="b309d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b309d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b309d-113">iLMS Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b309d-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b309d-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b309d-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b309d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b309d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b309d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b309d-118">Scenario description</span></span>
<span data-ttu-id="b309d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b309d-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b309d-121">갤러리에서 iLMS 추가</span><span class="sxs-lookup"><span data-stu-id="b309d-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="b309d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b309d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="b309d-123">갤러리에서 iLMS 추가</span><span class="sxs-lookup"><span data-stu-id="b309d-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="b309d-124">iLMS가 Azure AD에 통합되도록 구성하려면 갤러리에서 iLMS를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b309d-125">**갤러리에서 iLMS를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b309d-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b309d-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b309d-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b309d-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b309d-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b309d-133">검색 상자에 **iLMS**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-133">In the search box, type **iLMS**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="b309d-135">결과 창에서 **iLMS**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b309d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b309d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b309d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 iLMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b309d-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 iLMS 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="b309d-140">즉, Azure AD 사용자와 iLMS의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="b309d-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 iLMS의 **Username** 값으로 할당하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="b309d-142">iLMS에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b309d-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b309d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b309d-145">**[iLMS 테스트 사용자 만들기](#creating-an-ilms-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 iLMS에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b309d-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b309d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b309d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b309d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b309d-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 iLMS 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="b309d-150">**iLMS에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b309d-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="b309d-151">Azure Portal의 **iLMS** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b309d-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="b309d-155">**iLMS 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="b309d-157">a.</span><span class="sxs-lookup"><span data-stu-id="b309d-157">a.</span></span> <span data-ttu-id="b309d-158">**식별자** 텍스트 상자에 iLMS 관리 포털에 있는 SAML 설정의 **서비스 공급자** 섹션에서 복사한 **식별자** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="b309d-159">b.</span><span class="sxs-lookup"><span data-stu-id="b309d-159">b.</span></span> <span data-ttu-id="b309d-160">**회신 URL** 텍스트 상자에 iLMS 관리 포털에 있는 SAML 설정의 **서비스 공급자** 섹션에서 복사한 다음과 같은 패턴의 **끝점(URL)** 값을 붙여 넣습니다. `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="b309d-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="b309d-161">여기서 '123456'은 식별자 값의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="b309d-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="b309d-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="b309d-164">**로그온 URL** 텍스트 상자에 iLMS 관리 포털에 있는 SAML 설정의 **서비스 공급자** 섹션에서 복사한 **끝점(URL)** 값을 다음과 같은 패턴으로 붙여 넣습니다. `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="b309d-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="b309d-165">JIT 프로비전을 사용하도록 설정하려면 iLMS 응용 프로그램에 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b309d-166">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-166">Configure the following claims for this application.</span></span> <span data-ttu-id="b309d-167">응용 프로그램 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="b309d-168">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-168">The following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="b309d-170">iLMS에서 **부서, 지역** 및 **국** 특성을 만들고 이러한 특성의 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="b309d-171">위에 표시된 모든 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="b309d-172">이러한 특성을 매핑하려면 iLMS에서 **Create Un-recognized User Account(인식할 수 없는 사용자 계정 만들기)**를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="b309d-173">특성 구성을 이해하려면 [여기](http://support.inspiredelearning.com/customer/portal/articles/2204526)의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b309d-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="b309d-174">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="b309d-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="b309d-175">Attribute Name</span></span> | <span data-ttu-id="b309d-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="b309d-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="b309d-177">division</span><span class="sxs-lookup"><span data-stu-id="b309d-177">division</span></span> | <span data-ttu-id="b309d-178">user.department</span><span class="sxs-lookup"><span data-stu-id="b309d-178">user.department</span></span> |
    | <span data-ttu-id="b309d-179">region</span><span class="sxs-lookup"><span data-stu-id="b309d-179">region</span></span> | <span data-ttu-id="b309d-180">user.state</span><span class="sxs-lookup"><span data-stu-id="b309d-180">user.state</span></span> |
    | <span data-ttu-id="b309d-181">department</span><span class="sxs-lookup"><span data-stu-id="b309d-181">department</span></span> | <span data-ttu-id="b309d-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="b309d-182">user.jobtitle</span></span> |

    <span data-ttu-id="b309d-183">a.</span><span class="sxs-lookup"><span data-stu-id="b309d-183">a.</span></span> <span data-ttu-id="b309d-184">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="b309d-187">b.</span><span class="sxs-lookup"><span data-stu-id="b309d-187">b.</span></span> <span data-ttu-id="b309d-188">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b309d-189">c.</span><span class="sxs-lookup"><span data-stu-id="b309d-189">c.</span></span> <span data-ttu-id="b309d-190">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b309d-191">d.</span><span class="sxs-lookup"><span data-stu-id="b309d-191">d.</span></span> <span data-ttu-id="b309d-192">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-192">Click **Ok**</span></span>

7. <span data-ttu-id="b309d-193">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="b309d-195">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-195">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="b309d-197">다른 웹 브라우저 창에서 **iLMS 관리 포털**에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="b309d-198">**Settings(설정)** 탭에서 **SSO:SAML**을 클릭하여 SAML 설정을 열고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="b309d-200">a.</span><span class="sxs-lookup"><span data-stu-id="b309d-200">a.</span></span> <span data-ttu-id="b309d-201">**Service Provider(서비스 공급자)** 섹션을 확장하고 **Identifier(식별자)** 및 **Endpoint (URL)(끝점 URL)** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="b309d-203">b.</span><span class="sxs-lookup"><span data-stu-id="b309d-203">b.</span></span> <span data-ttu-id="b309d-204">**Identity Provider(ID 공급자)** 섹션에서 **Import Metadata(메타데이터 가져오기)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="b309d-205">c.</span><span class="sxs-lookup"><span data-stu-id="b309d-205">c.</span></span> <span data-ttu-id="b309d-206">Azure Portal에서 다운로드한 **메타데이터** 파일을 **SAML 서명 인증서** 섹션에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="b309d-208">d.</span><span class="sxs-lookup"><span data-stu-id="b309d-208">d.</span></span> <span data-ttu-id="b309d-209">인식할 수 없는 사용자의 iLMS 계정을 만들기 위해 JIT 프로비전을 사용하도록 설정하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="b309d-210">**Create Un-recognized User Account(인식할 수 없는 사용자 계정 만들기)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="b309d-212">Azure AD의 특성을 iLMS의 특성과 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="b309d-213">특성 열에 특성 이름 또는 기본값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="b309d-214">e.</span><span class="sxs-lookup"><span data-stu-id="b309d-214">e.</span></span> <span data-ttu-id="b309d-215">**Business Rules(비즈니스 규칙)** 탭으로 이동하여 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="b309d-217">Single Sign-on 시 존재하지 않는 지역, 국 및 부서를 만들려면 **Create Un-recognized Regions, Divisions and Departments(인식할 수 없는 지역, 국 및 부서 만들기)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="b309d-218">사용자의 프로필을 Single Sign-on마다 업데이트할지 여부를 지정하려면 **Update User Profile During Sign-in(로그인하는 동안 사용자 프로필 업데이트)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="b309d-219">**“Update Blank Values for Non Mandatory Fields in User Profile”(사용자 프로필의 필수가 아닌 필드에 대한 빈 값 업데이트)** 옵션이 선택되어 있으면 로그인 시 비어 있는 선택적 프로필 필드로 인해 사용자의 iLMS 프로필에 해당 필드에 대한 빈 값을 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="b309d-220">**Send Error Notification Email(오류 알림 전자 메일 보내기)**를 선택하고 오류 알림 전자 메일을 수신할 사용자의 전자 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="b309d-221">**저장** 단추를 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-221">Click **Save** button to save the settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="b309d-223">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b309d-224">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b309d-225">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b309d-226">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b309d-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="b309d-227">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b309d-229">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b309d-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b309d-230">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b309d-232">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b309d-234">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b309d-236">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b309d-238">a.</span><span class="sxs-lookup"><span data-stu-id="b309d-238">a.</span></span> <span data-ttu-id="b309d-239">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b309d-240">b.</span><span class="sxs-lookup"><span data-stu-id="b309d-240">b.</span></span> <span data-ttu-id="b309d-241">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b309d-242">c.</span><span class="sxs-lookup"><span data-stu-id="b309d-242">c.</span></span> <span data-ttu-id="b309d-243">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b309d-244">d.</span><span class="sxs-lookup"><span data-stu-id="b309d-244">d.</span></span> <span data-ttu-id="b309d-245">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="b309d-246">iLMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b309d-246">Creating an iLMS test user</span></span>

<span data-ttu-id="b309d-247">응용 프로그램이 Just-In-Time 사용자 프로비전을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="b309d-248">JIT는 iLMS 관리 포털에서 SAML 구성을 설정하는 동안 **Create Un-recognized User Account(인식할 수 없는 사용자 계정 만들기)** 확인란을 클릭한 경우에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="b309d-249">사용자를 수동으로 만들어야 하는 경우에는 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="b309d-250">iLMS 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="b309d-251">**Users(사용자)** 탭에서 **“Register User”(사용자 등록)**를 클릭하여 **Register User(사용자 등록)** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![직원 추가](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="b309d-253">**“Register User”(사용자 등록)** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![직원 추가](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="b309d-255">a.</span><span class="sxs-lookup"><span data-stu-id="b309d-255">a.</span></span> <span data-ttu-id="b309d-256">**First Name(이름)** 텍스트 상자에 이름 Britta를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="b309d-257">b.</span><span class="sxs-lookup"><span data-stu-id="b309d-257">b.</span></span> <span data-ttu-id="b309d-258">**Last Name(성)** 텍스트 상자에 성 Simon을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="b309d-259">c.</span><span class="sxs-lookup"><span data-stu-id="b309d-259">c.</span></span> <span data-ttu-id="b309d-260">**Email ID(전자 메일 ID)** 텍스트 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="b309d-261">d.</span><span class="sxs-lookup"><span data-stu-id="b309d-261">d.</span></span> <span data-ttu-id="b309d-262">**Region(지역)** 드롭다운에서 지역에 대한 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="b309d-263">e.</span><span class="sxs-lookup"><span data-stu-id="b309d-263">e.</span></span> <span data-ttu-id="b309d-264">**Division(국)** 드롭다운에서 국에 대한 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="b309d-265">f.</span><span class="sxs-lookup"><span data-stu-id="b309d-265">f.</span></span> <span data-ttu-id="b309d-266">**Department(부서)** 드롭다운에서 부서에 대한 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="b309d-267">g.</span><span class="sxs-lookup"><span data-stu-id="b309d-267">g.</span></span> <span data-ttu-id="b309d-268">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b309d-269">**Send Registration Mail(등록 메일 보내기)** 확인란을 선택하여 사용자에게 등록 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b309d-270">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b309d-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b309d-271">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 iLMS에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b309d-273">**Britta Simon을 iLMS에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b309d-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="b309d-274">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b309d-276">응용 프로그램 목록에서 **iLMS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-276">In the applications list, select **iLMS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="b309d-278">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-278">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b309d-280">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-280">Click **Add** button.</span></span> <span data-ttu-id="b309d-281">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b309d-283">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b309d-284">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b309d-285">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b309d-286">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b309d-286">Testing single sign-on</span></span>

<span data-ttu-id="b309d-287">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b309d-288">액세스 패널에서 iLMS 타일을 클릭하면 iLMS 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b309d-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b309d-289">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b309d-289">Additional resources</span></span>

* [<span data-ttu-id="b309d-290">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b309d-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b309d-291">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b309d-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

