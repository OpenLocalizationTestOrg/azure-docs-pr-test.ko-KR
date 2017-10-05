---
title: "자습서: Pluralsight와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Pluralsight 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="fced1-103">자습서: Pluralsight와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="fced1-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="fced1-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Pluralsight를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fced1-105">Pluralsight를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fced1-106">Pluralsight에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="fced1-107">사용자가 해당 Azure AD 계정으로 Pluralsight에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fced1-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fced1-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fced1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fced1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fced1-110">Prerequisites</span></span>

<span data-ttu-id="fced1-111">Pluralsight와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="fced1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="fced1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fced1-113">Pluralsight Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="fced1-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fced1-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fced1-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fced1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="fced1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fced1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fced1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="fced1-118">Scenario description</span></span>
<span data-ttu-id="fced1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fced1-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fced1-121">갤러리에서 Pluralsight 추가</span><span class="sxs-lookup"><span data-stu-id="fced1-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="fced1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fced1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="fced1-123">갤러리에서 Pluralsight 추가</span><span class="sxs-lookup"><span data-stu-id="fced1-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="fced1-124">Pluralsight의 Azure AD 통합을 구성하려면 갤러리의 Pluralsight를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fced1-125">**갤러리에서 Pluralsight를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="fced1-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fced1-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fced1-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fced1-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="fced1-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="fced1-133">검색 상자에 **Pluralsight**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-133">In the search box, type **Pluralsight**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="fced1-135">결과 패널에서 **Pluralsight**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fced1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fced1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fced1-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Pluralsight에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fced1-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Pluralsight 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="fced1-140">즉, Azure AD 사용자와 Pluralsight의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="fced1-141">Pluralsight에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fced1-142">Pluralsight에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fced1-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fced1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fced1-145">**[Pluralsight 테스트 사용자 만들기](#creating-a-pluralsight-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Pluralsight에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fced1-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fced1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fced1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="fced1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fced1-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Pluralsight 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="fced1-150">**Pluralsight에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="fced1-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="fced1-151">Azure Portal의 **Pluralsight** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="fced1-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="fced1-155">**Pluralsight 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="fced1-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="fced1-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fced1-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-158">This value is not real.</span></span> <span data-ttu-id="fced1-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fced1-160">이 값을 얻으려면 [Pluralsight 클라이언트 지원 팀](mailto:support@pluralsight.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="fced1-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="fced1-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="fced1-163">이 섹션의 목표는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Pluralsight 응용 프로그램에서 SSO를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="fced1-164">Pluralsight 응용 프로그램에는 특정 형식의 SAML 어설션이 필요하며, SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="fced1-165">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-165">The following screenshot shows an example for this.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="fced1-167">조직에 맞는 EmployeeID 등과 같은 적절한 값으로 **"고유 ID"** 특성을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="fced1-168">또한 이는 필수 특성이 아니지만 고유한 사용자를 식별하기 위해 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="fced1-169">필요한 **SAML 토큰 특성**을 추가하려면 아래 테이블의 각 행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="fced1-170">특성 이름</span><span class="sxs-lookup"><span data-stu-id="fced1-170">Attribute Name</span></span> | <span data-ttu-id="fced1-171">특성 값</span><span class="sxs-lookup"><span data-stu-id="fced1-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="fced1-172">이름</span><span class="sxs-lookup"><span data-stu-id="fced1-172">First Name</span></span> |<span data-ttu-id="fced1-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="fced1-173">user.givenname</span></span> |
   | <span data-ttu-id="fced1-174">성</span><span class="sxs-lookup"><span data-stu-id="fced1-174">Last Name</span></span> |<span data-ttu-id="fced1-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="fced1-175">user.surname</span></span> |
   | <span data-ttu-id="fced1-176">Email</span><span class="sxs-lookup"><span data-stu-id="fced1-176">Email</span></span> |<span data-ttu-id="fced1-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="fced1-177">user.mail</span></span> |
   
   <span data-ttu-id="fced1-178">a.</span><span class="sxs-lookup"><span data-stu-id="fced1-178">a.</span></span> <span data-ttu-id="fced1-179">**사용자 특성 추가**를 클릭하여 **사용자 특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Single Sign-On 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="fced1-181">b.</span><span class="sxs-lookup"><span data-stu-id="fced1-181">b.</span></span> <span data-ttu-id="fced1-182">**특성 이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="fced1-183">c.</span><span class="sxs-lookup"><span data-stu-id="fced1-183">c.</span></span> <span data-ttu-id="fced1-184">**특성 값** 목록에서 해당 행에 표시된 특성 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="fced1-185">d.</span><span class="sxs-lookup"><span data-stu-id="fced1-185">d.</span></span> <span data-ttu-id="fced1-186">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="fced1-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-187">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fced1-189">응용 프로그램에 대해 SSO를 구성하려면 [Pluralsight 전문 서비스](mailTo:professionalservices@pluralsight.com) 팀에 연락하여 다운로드한 메타데이터 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="fced1-190">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fced1-191">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fced1-192">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fced1-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fced1-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="fced1-194">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="fced1-196">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="fced1-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fced1-197">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fced1-199">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fced1-201">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fced1-203">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fced1-205">a.</span><span class="sxs-lookup"><span data-stu-id="fced1-205">a.</span></span> <span data-ttu-id="fced1-206">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fced1-207">b.</span><span class="sxs-lookup"><span data-stu-id="fced1-207">b.</span></span> <span data-ttu-id="fced1-208">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fced1-209">c.</span><span class="sxs-lookup"><span data-stu-id="fced1-209">c.</span></span> <span data-ttu-id="fced1-210">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fced1-211">d.</span><span class="sxs-lookup"><span data-stu-id="fced1-211">d.</span></span> <span data-ttu-id="fced1-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="fced1-213">Pluralsight 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fced1-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="fced1-214">이 섹션은 Pluralsight에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="fced1-215">Pluralsight 계정에 사용자를 추가하려면 [Pluralsight 클라이언트 지원 팀](mailto:support@pluralsight.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="fced1-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fced1-216">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="fced1-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fced1-217">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Pluralsight에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![사용자 할당][200] 

<span data-ttu-id="fced1-219">**Britta Simon을 Pluralsight에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="fced1-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="fced1-220">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="fced1-222">응용 프로그램 목록에서 **Pluralsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-222">In the applications list, select **Pluralsight**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="fced1-224">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-224">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="fced1-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-226">Click **Add** button.</span></span> <span data-ttu-id="fced1-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="fced1-229">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fced1-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fced1-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fced1-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="fced1-232">Testing single sign-on</span></span>

<span data-ttu-id="fced1-233">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fced1-234">액세스 패널에서 Pluralsight 타일을 클릭하면 Pluralsight 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="fced1-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="fced1-235">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fced1-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fced1-236">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fced1-236">Additional resources</span></span>

* [<span data-ttu-id="fced1-237">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="fced1-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fced1-238">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="fced1-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

