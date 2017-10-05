---
title: "자습서: DigiCert와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 DigiCert 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="68715-103">자습서: Azure Active Directory와 DigiCert 통합</span><span class="sxs-lookup"><span data-stu-id="68715-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="68715-104">이 자습서에서는 Azure AD(Azure Active Directory)와 DigiCert를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68715-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68715-105">DigiCert를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="68715-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68715-106">DigiCert에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="68715-107">사용자가 해당 Azure AD 계정으로 DigiCert에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68715-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="68715-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68715-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68715-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="68715-110">Prerequisites</span></span>

<span data-ttu-id="68715-111">DigiCert와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="68715-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="68715-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68715-113">DigiCert Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="68715-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68715-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68715-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68715-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="68715-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68715-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68715-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="68715-118">Scenario description</span></span>
<span data-ttu-id="68715-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68715-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68715-121">갤러리에서 DigiCert 추가</span><span class="sxs-lookup"><span data-stu-id="68715-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="68715-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="68715-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="68715-123">갤러리에서 DigiCert 추가</span><span class="sxs-lookup"><span data-stu-id="68715-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="68715-124">DigiCert의 Azure AD 통합을 구성하려면 갤러리의 DigiCert를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68715-125">**갤러리에서 DigiCert를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="68715-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68715-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68715-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68715-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="68715-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="68715-133">검색 상자에 **DigiCert**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-133">In the search box, type **DigiCert**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="68715-135">결과 패널에서 **DigiCert**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68715-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="68715-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68715-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 DigiCert에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68715-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 DigiCert 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="68715-140">즉, Azure AD 사용자와 DigiCert의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="68715-141">DigiCert에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="68715-142">DigiCert에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68715-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="68715-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68715-145">**[DigiCert 테스트 사용자 만들기](#creating-a-digicert-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 해당 사용자를 DigiCert에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68715-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="68715-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68715-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68715-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="68715-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68715-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 DigiCert 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="68715-150">**DigiCert에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="68715-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="68715-151">Azure Portal의 **DigiCert** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="68715-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="68715-155">**DigiCert 도메인 및 URL** 섹션에서 앱이 Azure와 이미 사전 통합되었으므로 사용자는 아무 단계도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="68715-157">DigiCert 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="68715-158">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-158">Configure the following claims for this application.</span></span> <span data-ttu-id="68715-159">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="68715-160">다음 스크린샷은 이 구성에 대한 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="68715-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="68715-162">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="68715-163">특성 이름</span><span class="sxs-lookup"><span data-stu-id="68715-163">Attribute Name</span></span> | <span data-ttu-id="68715-164">특성 값</span><span class="sxs-lookup"><span data-stu-id="68715-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="68715-165">company</span><span class="sxs-lookup"><span data-stu-id="68715-165">company</span></span> | <span data-ttu-id="68715-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="68715-166">< companycode ></span></span> |
    | <span data-ttu-id="68715-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="68715-167">digicertrole</span></span> | <span data-ttu-id="68715-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="68715-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="68715-169">**company** 특성 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="68715-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="68715-170">실제 회사 코드로 이 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-170">Update this value with actual company code.</span></span> <span data-ttu-id="68715-171">**company** 특성 값을 가져오려면 [DigiCert 지원 팀](mailto:support@digicert.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="68715-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="68715-172">a.</span><span class="sxs-lookup"><span data-stu-id="68715-172">a.</span></span> <span data-ttu-id="68715-173">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68715-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="68715-176">b.</span><span class="sxs-lookup"><span data-stu-id="68715-176">b.</span></span> <span data-ttu-id="68715-177">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="68715-178">c.</span><span class="sxs-lookup"><span data-stu-id="68715-178">c.</span></span> <span data-ttu-id="68715-179">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="68715-180">d.</span><span class="sxs-lookup"><span data-stu-id="68715-180">d.</span></span> <span data-ttu-id="68715-181">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="68715-182">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="68715-184">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-184">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="68715-186">**DigiCert** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Direct 지원 팀](mailto:support@digicert.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="68715-187">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="68715-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="68715-188">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68715-189">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68715-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68715-190">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68715-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68715-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68715-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="68715-192">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68715-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="68715-194">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="68715-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68715-195">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68715-197">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68715-199">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68715-201">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68715-203">a.</span><span class="sxs-lookup"><span data-stu-id="68715-203">a.</span></span> <span data-ttu-id="68715-204">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68715-205">b.</span><span class="sxs-lookup"><span data-stu-id="68715-205">b.</span></span> <span data-ttu-id="68715-206">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68715-207">c.</span><span class="sxs-lookup"><span data-stu-id="68715-207">c.</span></span> <span data-ttu-id="68715-208">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="68715-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="68715-209">d.</span><span class="sxs-lookup"><span data-stu-id="68715-209">d.</span></span> <span data-ttu-id="68715-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="68715-211">DigiCert 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68715-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="68715-212">이 섹션에서는 DigiCert에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68715-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="68715-213">[DigiCert 지원 팀](mailto:support@digicert.com)과 함께 DigiCert에 사용자를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="68715-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="68715-214">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="68715-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="68715-215">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 DigiCert에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![사용자 할당][200] 

<span data-ttu-id="68715-217">**Britta Simon을 DigiCert에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="68715-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="68715-218">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="68715-220">응용 프로그램 목록에서 **DigiCert**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-220">In the applications list, select **DigiCert**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="68715-222">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-222">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="68715-224">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-224">Click **Add** button.</span></span> <span data-ttu-id="68715-225">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="68715-227">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="68715-228">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68715-229">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68715-230">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="68715-230">Testing single sign-on</span></span>

<span data-ttu-id="68715-231">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="68715-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="68715-232">액세스 패널에서 DigiCert 타일을 클릭하면 DigiCert 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="68715-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="68715-233">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68715-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="68715-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="68715-234">Additional resources</span></span>

* [<span data-ttu-id="68715-235">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="68715-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68715-236">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="68715-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

