---
title: "자습서: Velpic SAML과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Velpic SAML 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="765db-103">자습서: Velpic SAML과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="765db-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="765db-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Velpic SAML을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="765db-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="765db-105">Azure AD에 Velpic SAML을 통합하면 다음과 같은 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="765db-106">Velpic SAML에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="765db-107">사용자가 해당 Azure AD 계정으로 Velpic SAML에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="765db-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="765db-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="765db-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="765db-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="765db-110">Prerequisites</span></span>

<span data-ttu-id="765db-111">Velpic SAML과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="765db-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="765db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="765db-113">Velpic SAML Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="765db-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="765db-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="765db-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="765db-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="765db-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="765db-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="765db-118">Scenario description</span></span>
<span data-ttu-id="765db-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="765db-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="765db-121">갤러리에서 Velpic SAML 추가</span><span class="sxs-lookup"><span data-stu-id="765db-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="765db-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="765db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="765db-123">갤러리에서 Velpic SAML 추가</span><span class="sxs-lookup"><span data-stu-id="765db-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="765db-124">Velpic SAML의 Azure AD 통합을 구성하려면 갤러리의 Velpic SAML을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="765db-125">**갤러리에서 Velpic SAML을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="765db-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="765db-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="765db-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="765db-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="765db-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="765db-133">검색 상자에 **Velpic SAML**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-133">In the search box, type **Velpic SAML**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="765db-135">결과 창에서 **Velpic SAML**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="765db-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="765db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="765db-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Velpic SAML에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="765db-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Velpic SAML 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="765db-140">즉, Azure AD 사용자와 Velpic SAML의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="765db-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Velpic SAML의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="765db-142">Velpic SAML에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="765db-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="765db-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="765db-145">**[Velpic SAML 테스트 사용자 만들기](#creating-a-velpic-saml-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Velpic SAML에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="765db-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="765db-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="765db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="765db-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="765db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="765db-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Velpic SAML 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="765db-150">**Velpic SAML에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="765db-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="765db-151">Azure 관리 포털의 **Velpic SAML** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="765db-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="765db-155">**Velpic SAML 도메인 및 URL** 섹션에 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="765db-157">a.</span><span class="sxs-lookup"><span data-stu-id="765db-157">a.</span></span> <span data-ttu-id="765db-158">**로그인 URL** 텍스트 상자에서 값으로 `https://<sub-domain>.velpicsaml.net`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="765db-159">b.</span><span class="sxs-lookup"><span data-stu-id="765db-159">b.</span></span> <span data-ttu-id="765db-160">**식별자** 텍스트 상자에 **'Single Sign-On URL'** 값 `https://auth.velpic.com/saml/v2/<entity-id>/login`을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="765db-161">Velpic SAML 쪽에서 SSO 플러그 인을 구성한 경우 로그온 URL은 Velpic SAML 팀에서 제공하고 식별자 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="765db-162">Velpic SAML 응용 프로그램 페이지에서 해당 값을 복사하고 여기에 붙여 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="765db-163">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="765db-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="765db-167">Velpic SAML 구성 섹션에서 Velpic SAML 구성을 클릭하여 로그온 구성 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="765db-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="765db-168">빠른 참조 섹션에서 SAML 엔터티 ID를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="765db-169">다른 웹 브라우저 창에서 Velpic SAML 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="765db-170">**관리** 탭을 클릭하고 **플러그 인** 단추를 클릭해야 하는 **통합** 섹션으로 이동하여 로그인을 위한 새 플러그 인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="765db-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="765db-172">**‘플로그 인 추가’** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="765db-174">플러그 인 추가 페이지에서 **SAML** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="765db-176">새 SAML 플러그 인의 이름을 입력하고 **'추가'** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="765db-178">세부 정보를 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-178">Enter the details as follows:</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="765db-180">a.</span><span class="sxs-lookup"><span data-stu-id="765db-180">a.</span></span> <span data-ttu-id="765db-181">**이름** 텍스트 상자에 SAML 플러그 인의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="765db-182">b.</span><span class="sxs-lookup"><span data-stu-id="765db-182">b.</span></span> <span data-ttu-id="765db-183">**발급자 URL** 텍스트 상자에 Azure Portal의 **로그온 구성** 창에서 복사한 **SAML 엔터티 ID**를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="765db-184">c.</span><span class="sxs-lookup"><span data-stu-id="765db-184">c.</span></span> <span data-ttu-id="765db-185">**공급자 메타데이터 구성**에 Azure Portal에서 다운로드한 메타데이터 XML 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="765db-186">d.</span><span class="sxs-lookup"><span data-stu-id="765db-186">d.</span></span> <span data-ttu-id="765db-187">**'새 사용자 자동 만들기'** 확인란을 활성화하여 SAML JIT(Just-In-Time) 프로비전을 활성화하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="765db-188">사용자자 Velpic에 없는 경우 이 플래그는 활성화되지 않으며 Azure에서 로그인에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="765db-189">플래그가 활성화된 경우 사용자는 로그인 시 자동으로 Velpic으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="765db-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="765db-190">e.</span><span class="sxs-lookup"><span data-stu-id="765db-190">e.</span></span> <span data-ttu-id="765db-191">텍스트 상자에서 **Single Sign-On URL**을 복사하고 Azure Portal에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="765db-192">f.</span><span class="sxs-lookup"><span data-stu-id="765db-192">f.</span></span> <span data-ttu-id="765db-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="765db-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="765db-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="765db-195">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="765db-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="765db-197">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="765db-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="765db-198">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="765db-200">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="765db-202">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="765db-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="765db-204">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="765db-206">a.</span><span class="sxs-lookup"><span data-stu-id="765db-206">a.</span></span> <span data-ttu-id="765db-207">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="765db-208">b.</span><span class="sxs-lookup"><span data-stu-id="765db-208">b.</span></span> <span data-ttu-id="765db-209">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="765db-210">c.</span><span class="sxs-lookup"><span data-stu-id="765db-210">c.</span></span> <span data-ttu-id="765db-211">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="765db-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="765db-212">d.</span><span class="sxs-lookup"><span data-stu-id="765db-212">d.</span></span> <span data-ttu-id="765db-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="765db-214">Velpic SAML 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="765db-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="765db-215">응용 프로그램은 JIT(Just-In-Time) 사용자 프로비전을 지원하므로 이 단계는 일반적으로 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="765db-216">자동 사용자 프로비전이 활성화되지 않은 경우 수동 사용자 만들기는 아래에서 설명한 대로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="765db-217">Velpic SAML 회사 사이트에 관리자 권한으로 로그인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="765db-218">관리 탭을 클릭하고 사용자 섹션으로 이동한 다음 새로 만들기 단추를 클릭하여 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![사용자 추가](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="765db-220">**“새 사용자 만들기”** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![사용자](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="765db-222">a.</span><span class="sxs-lookup"><span data-stu-id="765db-222">a.</span></span> <span data-ttu-id="765db-223">**이름** 텍스트 상자에 Britta Simon의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="765db-224">b.</span><span class="sxs-lookup"><span data-stu-id="765db-224">b.</span></span> <span data-ttu-id="765db-225">**성** 텍스트 상자에 Britta Simon의 성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="765db-226">c.</span><span class="sxs-lookup"><span data-stu-id="765db-226">c.</span></span> <span data-ttu-id="765db-227">**사용자 이름** 텍스트 상자에 Britta Simon의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="765db-228">d.</span><span class="sxs-lookup"><span data-stu-id="765db-228">d.</span></span> <span data-ttu-id="765db-229">**전자 메일** 텍스트 상자에 Britta Simon 계정의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="765db-230">e.</span><span class="sxs-lookup"><span data-stu-id="765db-230">e.</span></span> <span data-ttu-id="765db-231">나머지 정보는 선택 사항이며 필요한 경우 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="765db-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="765db-232">f.</span><span class="sxs-lookup"><span data-stu-id="765db-232">f.</span></span> <span data-ttu-id="765db-233">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="765db-234">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="765db-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="765db-235">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Velpic SAML에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![사용자 할당][200] 

<span data-ttu-id="765db-237">**Britta Simon을 Velpic SAML에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="765db-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="765db-238">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="765db-240">응용 프로그램 목록에서 **Velpic SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="765db-242">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-242">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="765db-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-244">Click **Add** button.</span></span> <span data-ttu-id="765db-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="765db-247">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="765db-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="765db-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="765db-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="765db-250">Testing single sign-on</span></span>

<span data-ttu-id="765db-251">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="765db-252">액세스 패널에서 Velpic SAML 타일을 클릭할 때 Velpic SAML 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="765db-253">로그인 페이지에 **'Azure AD를 사용하여 로그인'** 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="765db-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="765db-255">**'Azure AD를 사용하여 로그인'** 단추를 클릭하여 Azure AD 계정을 사용하여 Velpic에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="765db-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="765db-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="765db-256">Additional resources</span></span>

* [<span data-ttu-id="765db-257">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="765db-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="765db-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="765db-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

