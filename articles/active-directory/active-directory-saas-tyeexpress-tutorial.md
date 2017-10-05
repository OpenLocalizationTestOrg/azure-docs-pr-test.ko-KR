---
title: "자습서: T&E Express와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 T&E Express 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 869e5284c71904fcc817ceee0f39d94fab1bc6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="5520a-103">자습서: T&E Express와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5520a-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="5520a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 T&E Express를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5520a-105">T&E Express를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5520a-106">T&E Express에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="5520a-107">사용자가 해당 Azure AD 계정으로 T&E Express에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5520a-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5520a-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5520a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5520a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5520a-110">Prerequisites</span></span>

<span data-ttu-id="5520a-111">T&E Express와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="5520a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5520a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5520a-113">T&E Express Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5520a-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5520a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5520a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5520a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5520a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5520a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5520a-118">Scenario description</span></span>
<span data-ttu-id="5520a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5520a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5520a-121">갤러리에서 T&E Express 추가</span><span class="sxs-lookup"><span data-stu-id="5520a-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="5520a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5520a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="5520a-123">갤러리에서 T&E Express 추가</span><span class="sxs-lookup"><span data-stu-id="5520a-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="5520a-124">T&E Express의 Azure AD 통합을 구성하려면 갤러리의 T&E Express를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5520a-125">**갤러리에서 T&E Express를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5520a-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5520a-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5520a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5520a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5520a-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5520a-133">검색 상자에 **T&E Express**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-133">In the search box, type **T&E Express**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="5520a-135">결과 창에서 **T&E Express**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5520a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5520a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5520a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 T&E Express에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5520a-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 T&E Express 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="5520a-140">즉, Azure AD 사용자와 T&E Express의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="5520a-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 T&E Express의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="5520a-142">T&E Express에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5520a-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5520a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5520a-145">**[T&E Express 테스트 사용자 만들기](#creating-a-te-express-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 T&E Express에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5520a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5520a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5520a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5520a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5520a-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 T&E Express 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="5520a-150">**T&E Express에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5520a-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="5520a-151">Azure 관리 포털의 **T&E Express** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성][4]

2. <span data-ttu-id="5520a-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="5520a-155">**T&E Express 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="5520a-157">a.</span><span class="sxs-lookup"><span data-stu-id="5520a-157">a.</span></span> <span data-ttu-id="5520a-158">**식별자** 텍스트 상자에 해당 값으로 `https://<domain>.tyeexpress.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="5520a-159">b.</span><span class="sxs-lookup"><span data-stu-id="5520a-159">b.</span></span> <span data-ttu-id="5520a-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="5520a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5520a-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="5520a-162">실제 식별자 및 회신 URL로 해당 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5520a-163">식별자에는 고유한 문자열 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="5520a-164">이러한 값을 얻으려면 [T&E Express 지원 팀](http://www.tyeexpress.com/contacto.aspx)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5520a-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="5520a-165">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="5520a-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5520a-169">**T&E Express** 측에 Single Sign-On을 구성하려면 관리자 자격 증명을 사용하여 SAML Single Sign-On 없이 T&E express 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="5520a-170">**관리** 탭 아래에서 **SAML 도메인**을 클릭하여 SAML 설정 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="5520a-172">**Activar(활성화)** 옵션을 **아니요**에서 **SI(예)**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="5520a-173">**ID 공급자 메타데이터** 텍스트 상자에 Azure Portal에서 다운로드한 메타데이터 XML을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="5520a-175">**Guardar(저장)** 단추를 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5520a-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5520a-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="5520a-177">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5520a-179">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5520a-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5520a-180">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5520a-182">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5520a-184">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5520a-186">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5520a-188">a.</span><span class="sxs-lookup"><span data-stu-id="5520a-188">a.</span></span> <span data-ttu-id="5520a-189">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5520a-190">b.</span><span class="sxs-lookup"><span data-stu-id="5520a-190">b.</span></span> <span data-ttu-id="5520a-191">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5520a-192">c.</span><span class="sxs-lookup"><span data-stu-id="5520a-192">c.</span></span> <span data-ttu-id="5520a-193">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5520a-194">d.</span><span class="sxs-lookup"><span data-stu-id="5520a-194">d.</span></span> <span data-ttu-id="5520a-195">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="5520a-196">T&E Express 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5520a-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="5520a-197">Azure AD 사용자가 T&E Express에 로그인할 수 있도록 하려면 T&E Express로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="5520a-198">T&E Express의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="5520a-199">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5520a-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="5520a-200">T&E Express 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="5520a-201">관리 탭 아래에서 사용자를 클릭하여 사용자 마스터 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="5520a-203">홈 페이지에서 **+**를 클릭하여 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-203">On the home page, click on **+** to add the users.</span></span>

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="5520a-205">양식에서 요청한 대로 모든 필수 세부 정보를 입력하고 저장 단추를 클릭하여 세부 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5520a-208">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5520a-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5520a-209">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 T&E Express에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5520a-211">**Britta Simon을 T&E Express에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5520a-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="5520a-212">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5520a-214">응용 프로그램 목록에서 **T&E Express**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-214">In the applications list, select **T&E Express**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="5520a-216">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-216">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5520a-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-218">Click **Add** button.</span></span> <span data-ttu-id="5520a-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5520a-221">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5520a-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5520a-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5520a-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5520a-224">Testing single sign-on</span></span>

<span data-ttu-id="5520a-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5520a-226">액세스 패널에서 T&E Express 타일을 클릭하면 T&E Express 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5520a-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5520a-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5520a-227">Additional resources</span></span>

* [<span data-ttu-id="5520a-228">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5520a-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5520a-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5520a-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

