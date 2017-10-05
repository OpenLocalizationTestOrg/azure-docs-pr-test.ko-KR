---
title: "자습서: Trello와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Trello 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="8e74a-103">자습서: Trello와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="8e74a-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="8e74a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Trello를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e74a-105">Trello를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e74a-106">Trello에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="8e74a-107">사용자가 해당 Azure AD 계정으로 Trello에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e74a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e74a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e74a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e74a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e74a-110">Prerequisites</span></span>

<span data-ttu-id="8e74a-111">Trello와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="8e74a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="8e74a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e74a-113">Trello Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="8e74a-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e74a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e74a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e74a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8e74a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e74a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e74a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="8e74a-118">Scenario description</span></span>
<span data-ttu-id="8e74a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e74a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e74a-121">갤러리에서 Trello 추가</span><span class="sxs-lookup"><span data-stu-id="8e74a-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="8e74a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8e74a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="8e74a-123">갤러리에서 Trello 추가</span><span class="sxs-lookup"><span data-stu-id="8e74a-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="8e74a-124">Trello의 Azure AD 통합을 구성하려면 갤러리의 Trello를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e74a-125">**갤러리에서 Trello를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8e74a-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e74a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e74a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e74a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="8e74a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="8e74a-133">검색 상자에 **Trello**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-133">In the search box, type **Trello**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="8e74a-135">결과 창에서 **Trello**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e74a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8e74a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e74a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Trello에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e74a-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Trello 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="8e74a-140">즉, Azure AD 사용자와 Trello의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="8e74a-141">Trello에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e74a-142">Trello에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e74a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e74a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e74a-145">**[Trello 테스트 사용자 만들기](#creating-a-trello-test-user)** - Azure AD 표현과 연결된 Trello의 Britta Simon에 해당하는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e74a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e74a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e74a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="8e74a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e74a-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Trello 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="8e74a-150">**Trello에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8e74a-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="8e74a-151">Azure Portal의 **Trello** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="8e74a-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="8e74a-155">**Trello 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="8e74a-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="8e74a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="8e74a-158">**Trello 도메인 및 URL** 섹션에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="8e74a-160">a.</span><span class="sxs-lookup"><span data-stu-id="8e74a-160">a.</span></span> <span data-ttu-id="8e74a-161">**고급 URL 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="8e74a-162">b.</span><span class="sxs-lookup"><span data-stu-id="8e74a-162">b.</span></span> <span data-ttu-id="8e74a-163">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://trello.com/auth/saml/consume/<enterprise>`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="8e74a-164">Trello에서 **\<enterprise\>** 동적 필드를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="8e74a-165">동적 필드 값이 없는 경우 [Trello 지원 팀](mailto:support@trello.com)에 문의하여 엔터프라이즈의 동적 필드를 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="8e74a-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="8e74a-166">Trello 응용 프로그램은 특정 특성을 포함하는 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="8e74a-167">이 응용 프로그램에 대한 다음 특성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="8e74a-168">응용 프로그램의 **"사용자 특성"**에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="8e74a-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-169">The following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="8e74a-171">**SAML 토큰 특성** 대화 상자에서 아래 테이블의 각 행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="8e74a-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="8e74a-172">Attribute Name</span></span> | <span data-ttu-id="8e74a-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="8e74a-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8e74a-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="8e74a-174">User.Email</span></span> | <span data-ttu-id="8e74a-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="8e74a-175">user.mail</span></span> |
    | <span data-ttu-id="8e74a-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="8e74a-176">User.FirstName</span></span> | <span data-ttu-id="8e74a-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8e74a-177">user.givenname</span></span> |
    | <span data-ttu-id="8e74a-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="8e74a-178">User.LastName</span></span> | <span data-ttu-id="8e74a-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="8e74a-179">user.surname</span></span> |

    <span data-ttu-id="8e74a-180">a.</span><span class="sxs-lookup"><span data-stu-id="8e74a-180">a.</span></span> <span data-ttu-id="8e74a-181">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="8e74a-184">b.</span><span class="sxs-lookup"><span data-stu-id="8e74a-184">b.</span></span> <span data-ttu-id="8e74a-185">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="8e74a-186">c.</span><span class="sxs-lookup"><span data-stu-id="8e74a-186">c.</span></span> <span data-ttu-id="8e74a-187">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8e74a-188">d.</span><span class="sxs-lookup"><span data-stu-id="8e74a-188">d.</span></span> <span data-ttu-id="8e74a-189">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="8e74a-190">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="8e74a-192">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-192">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e74a-194">**Trello 구성** 섹션에서 **Trello 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e74a-195">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="8e74a-197">응용 프로그램에 구성된 SSO를 가져오려면 [Trello Enterprise SSO 구성](https://trello.com/sso-configuration) 페이지로 이동하여 [Trello 지원 팀](mailto:support@trello.com)에 **SAML Single Sign-On 서비스 URL**을 보내고 **인증서(Base64)**를 첨부합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="8e74a-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e74a-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e74a-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e74a-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8e74a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e74a-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="8e74a-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="8e74a-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e74a-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e74a-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e74a-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e74a-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e74a-213">a.</span><span class="sxs-lookup"><span data-stu-id="8e74a-213">a.</span></span> <span data-ttu-id="8e74a-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e74a-215">b.</span><span class="sxs-lookup"><span data-stu-id="8e74a-215">b.</span></span> <span data-ttu-id="8e74a-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e74a-217">c.</span><span class="sxs-lookup"><span data-stu-id="8e74a-217">c.</span></span> <span data-ttu-id="8e74a-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e74a-219">d.</span><span class="sxs-lookup"><span data-stu-id="8e74a-219">d.</span></span> <span data-ttu-id="8e74a-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="8e74a-221">Trello 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8e74a-221">Creating a Trello test user</span></span>

<span data-ttu-id="8e74a-222">이 섹션에서는 Trello에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="8e74a-223">이 섹션에서는 Trello에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="8e74a-224">Trello는 Just-In-Time 프로비전을 지원하고 Azure AD에서 처음으로 로그인할 때 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e74a-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="8e74a-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e74a-226">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Trello에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![사용자 할당][200] 

<span data-ttu-id="8e74a-228">**Britta Simon을 Trello에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8e74a-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="8e74a-229">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="8e74a-231">응용 프로그램 목록에서 **Trello**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-231">In the applications list, select **Trello**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="8e74a-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-233">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="8e74a-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-235">Click **Add** button.</span></span> <span data-ttu-id="8e74a-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="8e74a-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e74a-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e74a-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e74a-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="8e74a-241">Testing single sign-on</span></span>

<span data-ttu-id="8e74a-242">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8e74a-243">액세스 패널에서 Trello 타일을 클릭하면 Trello 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e74a-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e74a-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8e74a-244">Additional resources</span></span>

* [<span data-ttu-id="8e74a-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="8e74a-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e74a-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8e74a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

