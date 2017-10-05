---
title: "자습서: ServiceChannel과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 ServiceChannel 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="e4676-103">자습서: ServiceChannel과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e4676-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="e4676-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ServiceChannel을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4676-105">ServiceChannel을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e4676-106">ServiceChannel에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="e4676-107">사용자가 해당 Azure AD 계정으로 ServiceChannel(Single Sign-On)에 자동으로 로그인하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4676-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e4676-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4676-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4676-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e4676-110">Prerequisites</span></span>

<span data-ttu-id="e4676-111">ServiceChannel과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="e4676-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e4676-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4676-113">ServiceChannel Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e4676-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4676-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4676-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4676-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e4676-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4676-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e4676-118">Scenario description</span></span>
<span data-ttu-id="e4676-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4676-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4676-121">갤러리에서 ServiceChannel 추가</span><span class="sxs-lookup"><span data-stu-id="e4676-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="e4676-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e4676-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="e4676-123">갤러리에서 ServiceChannel 추가</span><span class="sxs-lookup"><span data-stu-id="e4676-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="e4676-124">ServiceChannel의 Azure AD 통합을 구성하려면 갤러리의 ServiceChannel을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e4676-125">**갤러리에서 ServiceChannel을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4676-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e4676-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4676-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e4676-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e4676-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e4676-133">검색 상자에 **ServiceChannel**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-133">In the search box, type **ServiceChannel**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="e4676-135">결과 창에서 **ServiceChannel**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4676-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e4676-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4676-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ServiceChannel에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e4676-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ServiceChannel 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="e4676-140">즉, Azure AD 사용자 및 ServiceChannel의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="e4676-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 ServiceChannel의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="e4676-142">ServiceChannel에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e4676-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e4676-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4676-145">**[ServiceChannel 테스트 사용자 만들기](#creating-a-servicechannel-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="e4676-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4676-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4676-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e4676-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4676-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 ServiceChannel 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="e4676-150">**ServiceChannel에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4676-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="e4676-151">Azure 관리 포털의 **ServiceChannel** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e4676-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="e4676-155">**ServiceChannel 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="e4676-157">a.</span><span class="sxs-lookup"><span data-stu-id="e4676-157">a.</span></span> <span data-ttu-id="e4676-158">**식별자** 텍스트 상자에 해당 값으로 `http://adfs.<domain>.com/adfs/service/trust`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="e4676-159">b.</span><span class="sxs-lookup"><span data-stu-id="e4676-159">b.</span></span> <span data-ttu-id="e4676-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="e4676-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e4676-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-161">Please note that these are not the real values.</span></span> <span data-ttu-id="e4676-162">실제 식별자 및 회신 URL로 해당 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e4676-163">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="e4676-164">이러한 값을 얻으려면 [ServiceChannel 지원 팀](https://servicechannel.zendesk.com/hc/en-us)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e4676-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="e4676-165">ServiceChannel 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="e4676-166">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="e4676-167">**NameIdentifier(사용자 식별자)**는 유일한 필수 클레임이며 기본값은 **user.userprincipalname**이지만 ServiceChannel에서는 **user.mail**과 매핑되도록 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="e4676-168">JIT(Just-In-Time) 사용자 프로비전을 활성화하려는 경우 아래와 같이 다음 클레임을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="e4676-169">**역할** 클레임은 사용자의 역할을 포함하는 **user.assignedroles**에 매핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="e4676-170">클레임에 대한 자세한 지침은 [여기](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example)에서 ServiceChannel 가이드를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="e4676-172">[여기](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/)를 클릭하여 Azure AD에서 **역할**을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="e4676-173">**사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="e4676-174">특성 이름</span><span class="sxs-lookup"><span data-stu-id="e4676-174">Attribute Name</span></span> | <span data-ttu-id="e4676-175">특성 값</span><span class="sxs-lookup"><span data-stu-id="e4676-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="e4676-176">역할</span><span class="sxs-lookup"><span data-stu-id="e4676-176">Role</span></span>| <span data-ttu-id="e4676-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="e4676-177">user.assignedroles</span></span> |

    <span data-ttu-id="e4676-178">a.</span><span class="sxs-lookup"><span data-stu-id="e4676-178">a.</span></span> <span data-ttu-id="e4676-179">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="e4676-182">b.</span><span class="sxs-lookup"><span data-stu-id="e4676-182">b.</span></span> <span data-ttu-id="e4676-183">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e4676-184">c.</span><span class="sxs-lookup"><span data-stu-id="e4676-184">c.</span></span> <span data-ttu-id="e4676-185">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e4676-186">d.</span><span class="sxs-lookup"><span data-stu-id="e4676-186">d.</span></span> <span data-ttu-id="e4676-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="e4676-188">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="e4676-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-190">Click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e4676-192">**ServiceChannel 구성** 섹션에서 **ServiceChannel 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e4676-193">**빠른 참조** 섹션에서 **SAML 엔터티 ID**를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="e4676-194">**ServiceChannel** 측에서 Single Sign-On을 구성하려면 다운로드한 **인증서(Base64)** 및 **SAML 엔터티 ID**를 [ServiceChannel 지원 팀](https://servicechannel.zendesk.com/hc/en-us)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="e4676-195">그러면 해당 팀에서 SAML SSO 연결이 양쪽에 제대로 설정되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4676-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e4676-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4676-197">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e4676-199">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="e4676-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e4676-200">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4676-202">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4676-204">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4676-206">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4676-208">a.</span><span class="sxs-lookup"><span data-stu-id="e4676-208">a.</span></span> <span data-ttu-id="e4676-209">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4676-210">b.</span><span class="sxs-lookup"><span data-stu-id="e4676-210">b.</span></span> <span data-ttu-id="e4676-211">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4676-212">c.</span><span class="sxs-lookup"><span data-stu-id="e4676-212">c.</span></span> <span data-ttu-id="e4676-213">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e4676-214">d.</span><span class="sxs-lookup"><span data-stu-id="e4676-214">d.</span></span> <span data-ttu-id="e4676-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="e4676-216">ServiceChannel 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e4676-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="e4676-217">응용 프로그램이 Just-In-Time 사용자 프로비전을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="e4676-218">전체 사용자 프로비전은 [ServiceChannel 지원 팀](https://servicechannel.zendesk.com/hc/en-us)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e4676-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e4676-219">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e4676-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e4676-220">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ServiceChannel에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e4676-222">**Britta Simon을 ServiceChannel에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e4676-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="e4676-223">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e4676-225">응용 프로그램 목록에서 **ServiceChannel**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="e4676-227">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-227">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e4676-229">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-229">Click **Add** button.</span></span> <span data-ttu-id="e4676-230">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e4676-232">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e4676-233">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4676-234">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4676-235">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e4676-235">Testing single sign-on</span></span>

<span data-ttu-id="e4676-236">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e4676-237">액세스 패널에서 ServiceChannel 타일을 클릭하면 ServiceChannel 응용 프로그램에 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4676-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4676-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e4676-238">Additional resources</span></span>

* [<span data-ttu-id="e4676-239">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e4676-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4676-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e4676-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png