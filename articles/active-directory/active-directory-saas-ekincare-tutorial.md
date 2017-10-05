---
title: "자습서: eKincare와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 eKincare 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="c4e61-103">자습서: Azure Active Directory와 eKincare 통합</span><span class="sxs-lookup"><span data-stu-id="c4e61-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="c4e61-104">이 자습서에서는 Azure AD(Azure Active Directory)와 eKincare를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4e61-105">eKincare를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4e61-106">eKincare에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="c4e61-107">사용자가 해당 Azure AD 계정으로 eKincare에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4e61-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c4e61-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e61-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4e61-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4e61-110">Prerequisites</span></span>

<span data-ttu-id="c4e61-111">eKincare와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="c4e61-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c4e61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4e61-113">eKincare Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c4e61-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4e61-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4e61-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4e61-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c4e61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4e61-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4e61-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c4e61-118">Scenario description</span></span>
<span data-ttu-id="c4e61-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4e61-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4e61-121">갤러리에서 eKincare 추가</span><span class="sxs-lookup"><span data-stu-id="c4e61-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="c4e61-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c4e61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="c4e61-123">갤러리에서 eKincare 추가</span><span class="sxs-lookup"><span data-stu-id="c4e61-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="c4e61-124">eKincare의 Azure AD 통합을 구성하려면 갤러리의 eKincare을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4e61-125">**갤러리에서 eKincare를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4e61-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4e61-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4e61-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4e61-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c4e61-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c4e61-133">검색 상자에 **eKincare**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-133">In the search box, type **eKincare**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="c4e61-135">결과 창에서 **eKincare**를 선택한 다음 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4e61-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c4e61-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4e61-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 eKincare에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4e61-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 eKincare 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="c4e61-140">즉, Azure AD 사용자와 eKincare의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="c4e61-141">eKincare에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c4e61-142">eKincare에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4e61-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4e61-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4e61-145">**[eKincare 테스트 사용자 만들기](#creating-a-ekincare-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 eKincare에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4e61-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4e61-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4e61-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c4e61-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4e61-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 eKincare 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="c4e61-150">**eKincare에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4e61-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="c4e61-151">Azure Portal의 **eKincare** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c4e61-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="c4e61-155">**eKincare 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="c4e61-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4e61-157">a.</span></span> <span data-ttu-id="c4e61-158">**식별자** 텍스트 상자에서 `https://<instancename>.ekincare.com/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="c4e61-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4e61-159">b.</span></span> <span data-ttu-id="c4e61-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="c4e61-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4e61-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-161">These values are not real.</span></span> <span data-ttu-id="c4e61-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c4e61-163">이러한 값을 얻으려면 [eKincare 지원 팀](mailto:tech@ekincare.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e61-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="c4e61-164">eKincare 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c4e61-165">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-165">Configure the following claims for this application.</span></span> <span data-ttu-id="c4e61-166">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c4e61-167">다음 스크린샷은 이 구성에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="c4e61-168">클레임 이름은 항상 **"employeeid"** 및 사용자의 employeeid를 포함하는 user.extensionattribute1에 매핑한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="c4e61-169">다른 두 개의 클레임 이름인</span><span class="sxs-lookup"><span data-stu-id="c4e61-169">The other two claims' name i.e</span></span> <span data-ttu-id="c4e61-170">**"organizationid"** 및 **"organizationname"**은 항상 동일하며 해당 값에는 사용자 조직의 세부 사항이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="c4e61-172">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="c4e61-173">특성 이름</span><span class="sxs-lookup"><span data-stu-id="c4e61-173">Attribute Name</span></span> | <span data-ttu-id="c4e61-174">특성 값</span><span class="sxs-lookup"><span data-stu-id="c4e61-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="c4e61-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="c4e61-175">employeeid</span></span> | <span data-ttu-id="c4e61-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="c4e61-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="c4e61-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="c4e61-177">organizationid</span></span> | <span data-ttu-id="c4e61-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="c4e61-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="c4e61-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="c4e61-179">organizationname</span></span> | <span data-ttu-id="c4e61-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="c4e61-180">*user.companyname*</span></span> |

    <span data-ttu-id="c4e61-181">a.</span><span class="sxs-lookup"><span data-stu-id="c4e61-181">a.</span></span> <span data-ttu-id="c4e61-182">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="c4e61-185">b.</span><span class="sxs-lookup"><span data-stu-id="c4e61-185">b.</span></span> <span data-ttu-id="c4e61-186">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c4e61-187">c.</span><span class="sxs-lookup"><span data-stu-id="c4e61-187">c.</span></span> <span data-ttu-id="c4e61-188">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c4e61-189">d.</span><span class="sxs-lookup"><span data-stu-id="c4e61-189">d.</span></span> <span data-ttu-id="c4e61-190">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-190">Click **Ok**</span></span>

6. <span data-ttu-id="c4e61-191">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="c4e61-193">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-193">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c4e61-195">**eKincare** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [eKincare 지원 팀](mailto:tech@ekincare.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="c4e61-196">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c4e61-197">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4e61-198">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4e61-199">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4e61-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c4e61-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4e61-201">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c4e61-203">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c4e61-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4e61-204">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4e61-206">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4e61-208">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4e61-210">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4e61-212">a.</span><span class="sxs-lookup"><span data-stu-id="c4e61-212">a.</span></span> <span data-ttu-id="c4e61-213">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4e61-214">b.</span><span class="sxs-lookup"><span data-stu-id="c4e61-214">b.</span></span> <span data-ttu-id="c4e61-215">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4e61-216">c.</span><span class="sxs-lookup"><span data-stu-id="c4e61-216">c.</span></span> <span data-ttu-id="c4e61-217">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c4e61-218">d.</span><span class="sxs-lookup"><span data-stu-id="c4e61-218">d.</span></span> <span data-ttu-id="c4e61-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="c4e61-220">eKincare 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c4e61-220">Creating a eKincare test user</span></span>

<span data-ttu-id="c4e61-221">응용 프로그램이 Just-In-Time 사용자 프로비전을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4e61-222">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c4e61-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4e61-223">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 eKincare에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c4e61-225">**Britta Simon을 eKincare에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4e61-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="c4e61-226">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c4e61-228">응용 프로그램 목록에서 **eKincare**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-228">In the applications list, select **eKincare**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="c4e61-230">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-230">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c4e61-232">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-232">Click **Add** button.</span></span> <span data-ttu-id="c4e61-233">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c4e61-235">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4e61-236">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4e61-237">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4e61-238">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c4e61-238">Testing single sign-on</span></span>

<span data-ttu-id="c4e61-239">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c4e61-240">액세스 패널에서 eKincare 타일을 클릭하면 eKincare 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e61-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="c4e61-241">액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e61-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4e61-242">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c4e61-242">Additional resources</span></span>

* [<span data-ttu-id="c4e61-243">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c4e61-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4e61-244">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c4e61-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

