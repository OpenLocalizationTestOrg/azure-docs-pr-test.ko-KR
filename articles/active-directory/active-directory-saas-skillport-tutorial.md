---
title: "자습서: Skillport와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Skillport 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="01336-103">자습서: Skillport와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="01336-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="01336-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Skillport를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="01336-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01336-105">Skillport와 Azure AD를 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="01336-106">Skillport에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="01336-107">사용자가 해당 Azure AD 계정으로 Skillport에 자동으로 로그인(Single Sign-On)하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01336-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="01336-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01336-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01336-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="01336-110">Prerequisites</span></span>

<span data-ttu-id="01336-111">Skillport와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="01336-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="01336-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01336-113">Skillport Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="01336-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01336-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01336-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01336-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="01336-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01336-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01336-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="01336-118">Scenario description</span></span>
<span data-ttu-id="01336-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01336-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01336-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01336-121">갤러리에서 Skillport 추가</span><span class="sxs-lookup"><span data-stu-id="01336-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="01336-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="01336-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="01336-123">갤러리에서 Skillport 추가</span><span class="sxs-lookup"><span data-stu-id="01336-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="01336-124">Skillport의 Azure AD 통합을 구성하려면 갤러리의 Skillport를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="01336-125">**갤러리에서 Skillport를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="01336-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="01336-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01336-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="01336-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="01336-131">대화 상자 맨 위에서 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-131">Click **New Application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="01336-133">검색 상자에 **Skillport**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-133">In the search box, type **Skillport**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="01336-135">결과 창에서 **Skillport**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01336-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="01336-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="01336-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Skillport에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="01336-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Skillport 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="01336-140">즉, Azure AD 사용자와 Skillport의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="01336-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Skillport의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="01336-142">Skillport에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="01336-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="01336-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01336-145">**[Skillport 테스트 사용자 만들기](#creating-a-skillport-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Skillport에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01336-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="01336-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01336-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01336-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="01336-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01336-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Skillport 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="01336-150">**Skillport에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="01336-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="01336-151">Azure Portal의 **Skillport** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="01336-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="01336-155">**Skillport 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="01336-157">a.</span><span class="sxs-lookup"><span data-stu-id="01336-157">a.</span></span> <span data-ttu-id="01336-158">**로그온 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="01336-159">EU 데이터 센터: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="01336-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="01336-160">미국 데이터 센터: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="01336-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="01336-161">b.</span><span class="sxs-lookup"><span data-stu-id="01336-161">b.</span></span> <span data-ttu-id="01336-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="01336-163">EU 데이터 센터: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="01336-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="01336-164">미국 데이터 센터: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="01336-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01336-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="01336-165">These values are not the real.</span></span> <span data-ttu-id="01336-166">실제 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="01336-167">이러한 값을 얻으려면 [Skillport 클라이언트 지원 팀](https://www.skillsoft.com/contact.asp)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="01336-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="01336-168">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="01336-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01336-172">**Skillport** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Skillport 지원 팀](https://www.skillsoft.com/contact.asp)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="01336-173">그러면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="01336-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01336-174">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="01336-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="01336-175">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01336-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="01336-177">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="01336-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="01336-178">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01336-180">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01336-182">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="01336-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01336-184">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01336-186">a.</span><span class="sxs-lookup"><span data-stu-id="01336-186">a.</span></span> <span data-ttu-id="01336-187">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01336-188">b.</span><span class="sxs-lookup"><span data-stu-id="01336-188">b.</span></span> <span data-ttu-id="01336-189">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01336-190">c.</span><span class="sxs-lookup"><span data-stu-id="01336-190">c.</span></span> <span data-ttu-id="01336-191">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="01336-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="01336-192">d.</span><span class="sxs-lookup"><span data-stu-id="01336-192">d.</span></span> <span data-ttu-id="01336-193">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="01336-194">Skillport 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="01336-194">Creating a Skillport test user</span></span>

<span data-ttu-id="01336-195">Skillport 테스트 사용자를 만들려면 최종 사용자의 요구 사항에 따른 여러 비즈니스 시나리오를 갖고 있는 [Skillport 지원 팀](https://www.skillsoft.com/contact.asp)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="01336-196">지원 팀에서 사용자와 논의한 후 테스트 사용자를 구성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01336-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="01336-197">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="01336-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="01336-198">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Skillport에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![사용자 할당][200] 

<span data-ttu-id="01336-200">**Britta Simon을 Skillport에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="01336-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="01336-201">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="01336-203">응용 프로그램 목록에서 **Skillport**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-203">In the applications list, select **Skillport**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="01336-205">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-205">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="01336-207">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-207">Click **Add** button.</span></span> <span data-ttu-id="01336-208">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="01336-210">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="01336-211">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01336-212">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01336-213">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="01336-213">Testing single sign-on</span></span>

<span data-ttu-id="01336-214">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="01336-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="01336-215">액세스 패널에서 Skillport 타일을 클릭하면 Skillport 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="01336-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="01336-216">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01336-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="01336-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="01336-217">Additional resources</span></span>

* [<span data-ttu-id="01336-218">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="01336-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01336-219">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="01336-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

