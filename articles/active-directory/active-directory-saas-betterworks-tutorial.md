---
title: "자습서: BetterWorks와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 BetterWorks 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="a28b1-103">자습서: BetterWorks와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a28b1-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="a28b1-104">이 자습서에서는 Azure AD(Azure Active Directory)와 BetterWorks를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a28b1-105">BetterWorks를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a28b1-106">BetterWorks에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="a28b1-107">사용자가 해당 Azure AD 계정으로 BetterWorks에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a28b1-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a28b1-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a28b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a28b1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a28b1-110">Prerequisites</span></span>

<span data-ttu-id="a28b1-111">BetterWorks와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="a28b1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a28b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a28b1-113">BetterWorks Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a28b1-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a28b1-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a28b1-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a28b1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a28b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a28b1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a28b1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a28b1-118">Scenario description</span></span>
<span data-ttu-id="a28b1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a28b1-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a28b1-121">갤러리에서 BetterWorks 추가</span><span class="sxs-lookup"><span data-stu-id="a28b1-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="a28b1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a28b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="a28b1-123">갤러리에서 BetterWorks 추가</span><span class="sxs-lookup"><span data-stu-id="a28b1-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="a28b1-124">BetterWorks의 Azure AD 통합을 구성하려면 갤러리의 BetterWorks를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a28b1-125">**갤러리에서 BetterWorks를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a28b1-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a28b1-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a28b1-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a28b1-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a28b1-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a28b1-133">검색 상자에 **BetterWorks**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-133">In the search box, type **BetterWorks**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="a28b1-135">결과 패널에서 **BetterWorks**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a28b1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a28b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a28b1-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BetterWorks에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a28b1-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 BetterWorks 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="a28b1-140">즉, Azure AD 사용자와 BetterWorks의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="a28b1-141">BetterWorks에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a28b1-142">BetterWorks에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a28b1-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a28b1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a28b1-145">**[BetterWorks 테스트 사용자 만들기](#creating-a-betterworks-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 BetterWorks에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a28b1-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a28b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a28b1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a28b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a28b1-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 BetterWorks 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="a28b1-150">**BetterWorks에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a28b1-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="a28b1-151">Azure Portal의 **BetterWorks** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a28b1-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="a28b1-155">**BetterWorks 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="a28b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="a28b1-157">a.</span></span> <span data-ttu-id="a28b1-158">**식별자** 텍스트 상자에서 `https://app.betterworks.com/saml2/metadata/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="a28b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="a28b1-159">b.</span></span> <span data-ttu-id="a28b1-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="a28b1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="a28b1-161">**BetterWorks 도메인 및 URL** 섹션에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="a28b1-163">a.</span><span class="sxs-lookup"><span data-stu-id="a28b1-163">a.</span></span> <span data-ttu-id="a28b1-164">**고급 URL 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a28b1-165">b.</span><span class="sxs-lookup"><span data-stu-id="a28b1-165">b.</span></span> <span data-ttu-id="a28b1-166">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://app.betterworks.com`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a28b1-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-167">These are not real values.</span></span> <span data-ttu-id="a28b1-168">회신 URL, 식별자 및 실제 로그온 URL로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="a28b1-169">이러한 값을 가져오려면 [BetterWorks 지원팀](mailto:support@betterworks.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a28b1-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="a28b1-170">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="a28b1-172">BetterWorks 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a28b1-173">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-173">Configure the following claims for this application.</span></span> <span data-ttu-id="a28b1-174">응용 프로그램의 **"특성"** 탭에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="a28b1-175">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-175">The following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="a28b1-177">**SAML 토큰 특성** 대화 상자에서 아래 테이블의 각 행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="a28b1-178">특성 이름</span><span class="sxs-lookup"><span data-stu-id="a28b1-178">Attribute Name</span></span> | <span data-ttu-id="a28b1-179">특성 값</span><span class="sxs-lookup"><span data-stu-id="a28b1-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="a28b1-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="a28b1-180">saml_token</span></span>     | <span data-ttu-id="a28b1-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="a28b1-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="a28b1-182">a.</span><span class="sxs-lookup"><span data-stu-id="a28b1-182">a.</span></span> <span data-ttu-id="a28b1-183">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="a28b1-186">b.</span><span class="sxs-lookup"><span data-stu-id="a28b1-186">b.</span></span> <span data-ttu-id="a28b1-187">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="a28b1-188">c.</span><span class="sxs-lookup"><span data-stu-id="a28b1-188">c.</span></span> <span data-ttu-id="a28b1-189">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="a28b1-190">d.</span><span class="sxs-lookup"><span data-stu-id="a28b1-190">d.</span></span> <span data-ttu-id="a28b1-191">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-191">Click **Ok**.</span></span>

7. <span data-ttu-id="a28b1-192">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-192">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a28b1-194">**BetterWorks** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [BetterWorks 지원팀](mailto:support@betterworks.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="a28b1-195">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a28b1-196">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a28b1-197">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a28b1-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a28b1-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="a28b1-199">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a28b1-201">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a28b1-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a28b1-202">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a28b1-204">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a28b1-206">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a28b1-208">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a28b1-210">a.</span><span class="sxs-lookup"><span data-stu-id="a28b1-210">a.</span></span> <span data-ttu-id="a28b1-211">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a28b1-212">b.</span><span class="sxs-lookup"><span data-stu-id="a28b1-212">b.</span></span> <span data-ttu-id="a28b1-213">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a28b1-214">c.</span><span class="sxs-lookup"><span data-stu-id="a28b1-214">c.</span></span> <span data-ttu-id="a28b1-215">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a28b1-216">d.</span><span class="sxs-lookup"><span data-stu-id="a28b1-216">d.</span></span> <span data-ttu-id="a28b1-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="a28b1-218">BetterWorks 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a28b1-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="a28b1-219">이 섹션에서는 BetterWorks에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="a28b1-220">BetterWorks 플랫폼에 사용자를 추가하려면 [BetterWorks 지원팀](mailto:support@betterworks.com)과 함께 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="a28b1-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a28b1-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a28b1-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a28b1-222">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 BetterWorks에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a28b1-224">**Britta Simon을 BetterWorks에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a28b1-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="a28b1-225">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a28b1-227">응용 프로그램 목록에서 **BetterWorks**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-227">In the applications list, select **BetterWorks**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="a28b1-229">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-229">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a28b1-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-231">Click **Add** button.</span></span> <span data-ttu-id="a28b1-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a28b1-234">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a28b1-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a28b1-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a28b1-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a28b1-237">Testing single sign-on</span></span>

<span data-ttu-id="a28b1-238">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a28b1-239">액세스 패널에서 BetterWorks 타일을 클릭하면 BetterWorks 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a28b1-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a28b1-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a28b1-240">Additional resources</span></span>

* [<span data-ttu-id="a28b1-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a28b1-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a28b1-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a28b1-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

