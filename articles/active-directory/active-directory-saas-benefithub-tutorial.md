---
title: "자습서: BenefitHub와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 BenefitHub 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="7d5ca-103">자습서: BenefitHub와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7d5ca-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="7d5ca-104">이 자습서에서는 Azure AD(Azure Active Directory)와 BenefitHub를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d5ca-105">BenefitHub를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7d5ca-106">BenefitHub에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="7d5ca-107">사용자가 해당 Azure AD 계정으로 BenefitHub에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d5ca-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7d5ca-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d5ca-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7d5ca-110">Prerequisites</span></span>

<span data-ttu-id="7d5ca-111">BenefitHub와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="7d5ca-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7d5ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d5ca-113">BenefitHub Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7d5ca-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d5ca-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d5ca-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d5ca-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d5ca-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d5ca-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7d5ca-118">Scenario description</span></span>
<span data-ttu-id="7d5ca-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d5ca-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d5ca-121">갤러리에서 BenefitHub 추가</span><span class="sxs-lookup"><span data-stu-id="7d5ca-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="7d5ca-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7d5ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="7d5ca-123">갤러리에서 BenefitHub 추가</span><span class="sxs-lookup"><span data-stu-id="7d5ca-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="7d5ca-124">Azure AD와 BenefitHub 통합을 구성하려면 갤러리의 BenefitHub를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7d5ca-125">**갤러리에서 BenefitHub를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d5ca-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7d5ca-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d5ca-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7d5ca-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7d5ca-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7d5ca-133">검색 상자에 **BenefitHub**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-133">In the search box, type **BenefitHub**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="7d5ca-135">결과 패널에서 **BenefitHub**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d5ca-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7d5ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d5ca-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BenefitHub에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7d5ca-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 BenefitHub 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="7d5ca-140">즉, Azure AD 사용자와 BenefitHub의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="7d5ca-141">BenefitHub에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7d5ca-142">BenefitHub에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7d5ca-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7d5ca-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d5ca-145">**[BenefitHub 테스트 사용자 만들기](#creating-a-benefithub-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 BenefitHub에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d5ca-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d5ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d5ca-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7d5ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d5ca-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 BenefitHub 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="7d5ca-150">**BenefitHub에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d5ca-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="7d5ca-151">Azure Portal의 **BenefitHub** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7d5ca-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="7d5ca-155">**BenefitHub 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="7d5ca-157">a.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-157">a.</span></span> <span data-ttu-id="7d5ca-158">**식별자** 텍스트 상자에 `urn:benefithub:passport`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="7d5ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-159">b.</span></span> <span data-ttu-id="7d5ca-160">**회신 URL** 텍스트 상자에서 `https://passport.benefithub.info/saml/post/ac`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="7d5ca-161">BenefitHub 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="7d5ca-162">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-162">Configure the following claims for this application.</span></span> <span data-ttu-id="7d5ca-163">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="7d5ca-165">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이전의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="7d5ca-166">특성 이름</span><span class="sxs-lookup"><span data-stu-id="7d5ca-166">Attribute Name</span></span> | <span data-ttu-id="7d5ca-167">특성 값</span><span class="sxs-lookup"><span data-stu-id="7d5ca-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7d5ca-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="7d5ca-168">organizationid</span></span> | <span data-ttu-id="7d5ca-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="7d5ca-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="7d5ca-170">이 특성 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-170">This attribute value is not real.</span></span> <span data-ttu-id="7d5ca-171">실제 organizationid로 이 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="7d5ca-172">실제 organizationid를 가져오려면 [BenefitHub 지원팀](https://www.benefithub.com/Home/ContactUs)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="7d5ca-173">a.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-173">a.</span></span> <span data-ttu-id="7d5ca-174">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7d5ca-177">b.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-177">b.</span></span> <span data-ttu-id="7d5ca-178">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7d5ca-179">c.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-179">c.</span></span> <span data-ttu-id="7d5ca-180">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7d5ca-181">d.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-181">d.</span></span> <span data-ttu-id="7d5ca-182">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7d5ca-183">SAML 어설션을 구성하기 전에 [BenefitHub 지원](https://www.benefithub.com/Home/ContactUs)에 문의하고 테넌트에 대한 고유 식별자 특성 값을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="7d5ca-184">응용 프로그램에 대한 사용자 지정 클레임을 구성하려면 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="7d5ca-185">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="7d5ca-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-187">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7d5ca-189">**BenefitHub** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [BenefitHub 지원팀](https://www.benefithub.com/Home/ContactUs)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="7d5ca-190">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7d5ca-191">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7d5ca-192">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7d5ca-193">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d5ca-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7d5ca-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d5ca-195">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7d5ca-197">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7d5ca-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7d5ca-198">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d5ca-200">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d5ca-202">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d5ca-204">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d5ca-206">a.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-206">a.</span></span> <span data-ttu-id="7d5ca-207">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d5ca-208">b.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-208">b.</span></span> <span data-ttu-id="7d5ca-209">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d5ca-210">c.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-210">c.</span></span> <span data-ttu-id="7d5ca-211">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7d5ca-212">d.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-212">d.</span></span> <span data-ttu-id="7d5ca-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="7d5ca-214">BenefitHub 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7d5ca-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="7d5ca-215">이 섹션에서는 BenefitHub에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="7d5ca-216">BenefitHub 플랫폼에서 사용자를 추가하려면 [BenefitHub 지원팀](https://www.benefithub.com/Home/ContactUs)과 함께 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="7d5ca-217">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7d5ca-218">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7d5ca-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7d5ca-219">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 BenefitHub에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7d5ca-221">**Britta Simon을 BenefitHub에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d5ca-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="7d5ca-222">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7d5ca-224">응용 프로그램 목록에서 **BenefitHub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-224">In the applications list, select **BenefitHub**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="7d5ca-226">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-226">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7d5ca-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-228">Click **Add** button.</span></span> <span data-ttu-id="7d5ca-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7d5ca-231">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7d5ca-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d5ca-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d5ca-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7d5ca-234">Testing single sign-on</span></span>

<span data-ttu-id="7d5ca-235">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7d5ca-236">액세스 패널에서 BenefitHub 타일을 클릭하면 BenefitHub 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="7d5ca-237">액세스 패널에 대한 자세한 내용은 [Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d5ca-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d5ca-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7d5ca-238">Additional resources</span></span>

* [<span data-ttu-id="7d5ca-239">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7d5ca-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d5ca-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7d5ca-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

