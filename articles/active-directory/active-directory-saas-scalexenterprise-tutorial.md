---
title: "자습서: ScaleX Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 ScaleX Enterprise 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="29dfe-103">자습서: ScaleX Enterprise와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="29dfe-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="29dfe-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ScaleX Enterprise를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29dfe-105">ScaleX Enterprise를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29dfe-106">Azure AD에서 사용자의 ScaleX Enterprise에 대한 액세스 권한을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="29dfe-107">사용자의 Azure AD 계정으로 ScaleX Enterprise에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29dfe-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="29dfe-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="29dfe-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="29dfe-110">[Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29dfe-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29dfe-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="29dfe-111">Prerequisites</span></span>

<span data-ttu-id="29dfe-112">ScaleX Enterprise와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="29dfe-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="29dfe-113">An Azure AD subscription</span></span>
- <span data-ttu-id="29dfe-114">ScaleX Enterprise Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="29dfe-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29dfe-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29dfe-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29dfe-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="29dfe-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="29dfe-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29dfe-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="29dfe-119">Scenario description</span></span>
<span data-ttu-id="29dfe-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29dfe-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29dfe-122">갤러리에서 ScaleX Enterprise 추가</span><span class="sxs-lookup"><span data-stu-id="29dfe-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="29dfe-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="29dfe-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="29dfe-124">갤러리에서 ScaleX Enterprise 추가</span><span class="sxs-lookup"><span data-stu-id="29dfe-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="29dfe-125">ScaleX Enterprise가 Azure AD에 통합되도록 구성하려면 갤러리에서 ScaleX Enterprise를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29dfe-126">**갤러리에서 ScaleX Enterprise를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="29dfe-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29dfe-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29dfe-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29dfe-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-130">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="29dfe-132">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-132">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="29dfe-134">검색 상자에 **ScaleX Enterprise**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="29dfe-136">결과 창에서 **ScaleX Enterprise**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29dfe-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="29dfe-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29dfe-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ScaleX Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29dfe-140">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ScaleX Enterprise 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="29dfe-141">즉, Azure AD 사용자와 ScaleX Enterprise의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="29dfe-142">이 연결 관계는 Azure AD의 **사용자 이름** 값을 ScaleX Enterprise의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="29dfe-143">ScaleX Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29dfe-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29dfe-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29dfe-146">**[ScaleX Enterprise 테스트 사용자 만들기](#creating-a-scalex-enterprise-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 ScaleX Enterprise에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29dfe-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29dfe-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29dfe-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="29dfe-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29dfe-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ScaleX Enterprise 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="29dfe-151">**ScaleX Enterprise에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="29dfe-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="29dfe-152">Azure Portal의 **ScaleX Enterprise** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="29dfe-154">**Single Sign-On** 대화 상자에서 **모드**로 **SAML 기반 로그인**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="29dfe-156">**ScaleX Enterprise 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="29dfe-158">a.</span><span class="sxs-lookup"><span data-stu-id="29dfe-158">a.</span></span> <span data-ttu-id="29dfe-159">**식별자** 텍스트 상자에 `https://platform.rescale.com/saml2/<company id>/` 패턴으로 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="29dfe-160">b.</span><span class="sxs-lookup"><span data-stu-id="29dfe-160">b.</span></span> <span data-ttu-id="29dfe-161">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="29dfe-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="29dfe-162">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="29dfe-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="29dfe-164">**로그온 URL** 텍스트 상자에 다음 패턴으로 값을 입력합니다. `https://platform.rescale.com/saml2/<company id>/sso/` </span><span class="sxs-lookup"><span data-stu-id="29dfe-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="29dfe-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-165">These are not the real values.</span></span> <span data-ttu-id="29dfe-166">실제 식별자, 회신 URL 또는 로그온 URL을 사용하여 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="29dfe-167">이러한 값을 얻으려면 [ScaleX Enterprise 클라이언트 지원 팀](http://info.rescale.com/contact_sales)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="29dfe-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="29dfe-168">ScaleX 응용 프로그램에는 특정 형식의 SAML 어설션이 필요하기 때문에 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="29dfe-169">사용자 지정 특성 설정을 열려면 **기타 모든 사용자 특성 보기 및 편집** 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="29dfe-171">a.</span><span class="sxs-lookup"><span data-stu-id="29dfe-171">a.</span></span> <span data-ttu-id="29dfe-172">**name** 특성을 마우스 오른쪽 단추로 클릭하고 삭제를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-172">Right click the attribute **name** and click delete.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="29dfe-174">b.</span><span class="sxs-lookup"><span data-stu-id="29dfe-174">b.</span></span> <span data-ttu-id="29dfe-175">**emailaddress** 특성을 클릭하여 특성 편집 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="29dfe-176">**user.mail**에서 **user.userprincipalname**으로 값을 변경하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="29dfe-178">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="29dfe-180">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-180">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="29dfe-182">**ScaleX Enterprise 구성** 섹션에서 **ScaleX Enterprise 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29dfe-183">**빠른 참조 섹션**에서 **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="29dfe-185">**ScaleX Enterprise** 쪽에서 Single Sign-On을 구성하려면 관리자 권한으로 ScaleX Enterprise 회사 웹 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="29dfe-186">오른쪽 위에 있는 메뉴를 클릭하고 **Contoso Administration(Contoso 관리)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29dfe-187">Contoso는 예일뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-187">Contoso is just an example.</span></span> <span data-ttu-id="29dfe-188">이 값은 실제 회사 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-188">This should be your actual Company Name.</span></span> 

    ![Single Sign-On 구성](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="29dfe-190">최상위 메뉴에서 **Integrations(통합)**을 선택하고 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="29dfe-192">다음과 같이 양식을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-192">Complete the form as follows:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="29dfe-194">a.</span><span class="sxs-lookup"><span data-stu-id="29dfe-194">a.</span></span> <span data-ttu-id="29dfe-195">**“Create any user who can authenticate with SSO.”(SSO로 인증할 수 있는 사용자 만들기)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="29dfe-196">b.</span><span class="sxs-lookup"><span data-stu-id="29dfe-196">b.</span></span> <span data-ttu-id="29dfe-197">**Service Provider saml(서비스 공급자 saml)**: ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent*** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="29dfe-198">c.</span><span class="sxs-lookup"><span data-stu-id="29dfe-198">c.</span></span> <span data-ttu-id="29dfe-199">**Name of Identity Provider email field in ACS response(ACS 응답의 ID 공급자 전자 메일 필드 이름)**: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="29dfe-200">d.</span><span class="sxs-lookup"><span data-stu-id="29dfe-200">d.</span></span> <span data-ttu-id="29dfe-201">**Identity Provider EntityDescriptor Entity ID(ID 공급자 EntityDescriptor 엔터티 ID):** Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="29dfe-202">e.</span><span class="sxs-lookup"><span data-stu-id="29dfe-202">e.</span></span> <span data-ttu-id="29dfe-203">**Identity Provider SingleSignOnService URL(ID 공급자 Single Sign-On URL):** Azure Portal의 **SAML Single Sign-On 서비스 URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="29dfe-204">f.</span><span class="sxs-lookup"><span data-stu-id="29dfe-204">f.</span></span> <span data-ttu-id="29dfe-205">**Identity Provider public X509 certificate(ID 공급자 공용 X509 인증서):** Azure에서 다운로드 한 X509 인증서를 메모장에서 열어서 이 상자에 내용을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="29dfe-206">인증서 내용 중간에 줄 바꿈이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="29dfe-207">g.</span><span class="sxs-lookup"><span data-stu-id="29dfe-207">g.</span></span> <span data-ttu-id="29dfe-208">다음 확인란을 선택합니다: **Enabled(사용), Encrypt NameID(NameID 암호화) 및 Sign AuthnRequests(AuthnRequests 서명)**</span><span class="sxs-lookup"><span data-stu-id="29dfe-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="29dfe-209">h.</span><span class="sxs-lookup"><span data-stu-id="29dfe-209">h.</span></span> <span data-ttu-id="29dfe-210">**Update SSO Settings(SSO 설정 업데이트)**를 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="29dfe-211">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29dfe-212">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29dfe-213">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29dfe-214">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="29dfe-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="29dfe-215">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="29dfe-217">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="29dfe-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29dfe-218">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29dfe-220">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29dfe-222">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29dfe-224">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29dfe-226">a.</span><span class="sxs-lookup"><span data-stu-id="29dfe-226">a.</span></span> <span data-ttu-id="29dfe-227">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29dfe-228">b.</span><span class="sxs-lookup"><span data-stu-id="29dfe-228">b.</span></span> <span data-ttu-id="29dfe-229">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29dfe-230">c.</span><span class="sxs-lookup"><span data-stu-id="29dfe-230">c.</span></span> <span data-ttu-id="29dfe-231">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="29dfe-232">d.</span><span class="sxs-lookup"><span data-stu-id="29dfe-232">d.</span></span> <span data-ttu-id="29dfe-233">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="29dfe-234">ScaleX Enterprise 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="29dfe-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="29dfe-235">Azure AD 사용자가 ScaleX Enterprise에 로그인할 수 있도록 하려면 ScaleX Enterprise에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="29dfe-236">ScaleX Enterprise의 경우 프로비전이 자동 작업이며 수동 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="29dfe-237">SSO 자격 증명으로 인증할 수 있는 사용자라면 누구든 ScaleX 쪽에서 자동으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="29dfe-238">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="29dfe-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="29dfe-239">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ScaleX Enterprise에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![사용자 할당][200] 

<span data-ttu-id="29dfe-241">**ScaleX Enterprise에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="29dfe-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="29dfe-242">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="29dfe-244">응용 프로그램 목록에서 **ScaleX Enterprise**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="29dfe-246">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-246">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="29dfe-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-248">Click **Add** button.</span></span> <span data-ttu-id="29dfe-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="29dfe-251">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29dfe-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29dfe-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="29dfe-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="29dfe-254">Testing single sign-on</span></span>

<span data-ttu-id="29dfe-255">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29dfe-256">액세스 패널에서 ScaleX Enterprise 타일을 클릭하면 ScaleX Enterprise 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="29dfe-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="29dfe-257">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29dfe-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="29dfe-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="29dfe-258">Additional resources</span></span>

* [<span data-ttu-id="29dfe-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="29dfe-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29dfe-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="29dfe-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

