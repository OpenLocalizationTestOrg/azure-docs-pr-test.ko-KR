---
title: "자습서: Lynda.com과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Lynda.com 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="f3eec-103">자습서: Lynda.com과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f3eec-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="f3eec-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Lynda.com을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3eec-105">Lynda.com을 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3eec-106">Lynda.com에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="f3eec-107">사용자가 해당 Azure AD 계정으로 Lynda.com에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3eec-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3eec-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3eec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3eec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f3eec-110">Prerequisites</span></span>

<span data-ttu-id="f3eec-111">Lynda.com과 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="f3eec-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f3eec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3eec-113">Lynda.com Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f3eec-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3eec-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3eec-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3eec-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f3eec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3eec-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3eec-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f3eec-118">Scenario description</span></span>
<span data-ttu-id="f3eec-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3eec-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3eec-121">갤러리에서 Lynda.com 추가</span><span class="sxs-lookup"><span data-stu-id="f3eec-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="f3eec-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f3eec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="f3eec-123">갤러리에서 Lynda.com 추가</span><span class="sxs-lookup"><span data-stu-id="f3eec-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="f3eec-124">Lynda.com의 Azure AD 통합을 구성하려면 갤러리의 Lynda.com을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3eec-125">**갤러리에서 Lynda.com을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f3eec-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3eec-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3eec-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3eec-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f3eec-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f3eec-133">검색 상자에 **Lynda.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-133">In the search box, type **Lynda.com**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="f3eec-135">결과 패널에서 **Lynda.com**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3eec-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f3eec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3eec-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lynda.com에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f3eec-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Lynda.com 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="f3eec-140">즉, Azure AD 사용자와 Lynda.com의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="f3eec-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Lynda.com의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="f3eec-142">Lynda.com에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3eec-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3eec-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3eec-145">**[Lynda.com 테스트 사용자 만들기](#creating-a-lyndacom-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Lynda.com에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3eec-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3eec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3eec-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f3eec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3eec-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Lynda.com 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="f3eec-150">**Lynda.com에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f3eec-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="f3eec-151">Azure Portal의 **Lynda.com** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f3eec-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="f3eec-155">**Lynda.com 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="f3eec-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="f3eec-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3eec-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-158">This value is not real.</span></span> <span data-ttu-id="f3eec-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f3eec-160">이러한 값을 얻으려면 [Lynda.com 클라이언트 지원 팀](https://www.linkedin.com/help/lynda/ask)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f3eec-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="f3eec-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="f3eec-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3eec-165">**Lynda.com** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Lynda.com 지원 팀](https://www.linkedin.com/help/lynda/ask)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3eec-166">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f3eec-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3eec-167">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f3eec-169">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f3eec-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3eec-170">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3eec-172">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3eec-174">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3eec-176">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3eec-178">a.</span><span class="sxs-lookup"><span data-stu-id="f3eec-178">a.</span></span> <span data-ttu-id="f3eec-179">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3eec-180">b.</span><span class="sxs-lookup"><span data-stu-id="f3eec-180">b.</span></span> <span data-ttu-id="f3eec-181">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3eec-182">c.</span><span class="sxs-lookup"><span data-stu-id="f3eec-182">c.</span></span> <span data-ttu-id="f3eec-183">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3eec-184">d.</span><span class="sxs-lookup"><span data-stu-id="f3eec-184">d.</span></span> <span data-ttu-id="f3eec-185">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="f3eec-186">Lynda.com 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f3eec-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="f3eec-187">Lynda.com을 프로비전하는 사용자를 구성할 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="f3eec-188">할당된 사용자가 액세스 패널을 사용하여 Lynda.com에 로그인하려는 경우 Lynda.com은 사용자가 존재하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="f3eec-189">사용할 수 있는 사용자 계정이 없으면 자동으로 Lynda.com에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="f3eec-190">다른 Lynda.com 사용자 계정 생성 도구 또는 Lynda.com이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3eec-191">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f3eec-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3eec-192">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Lynda.com에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f3eec-194">**Britta Simon을 Lynda.com에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f3eec-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="f3eec-195">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f3eec-197">응용 프로그램 목록에서 **Lynda.com**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-197">In the applications list, select **Lynda.com**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="f3eec-199">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-199">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f3eec-201">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-201">Click **Add** button.</span></span> <span data-ttu-id="f3eec-202">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f3eec-204">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3eec-205">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3eec-206">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3eec-207">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f3eec-207">Testing single sign-on</span></span>

<span data-ttu-id="f3eec-208">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3eec-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f3eec-209">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3eec-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f3eec-210">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f3eec-210">Additional resources</span></span>

* [<span data-ttu-id="f3eec-211">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f3eec-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3eec-212">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f3eec-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

