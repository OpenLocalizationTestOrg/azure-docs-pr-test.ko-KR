---
title: "자습서: FilesAnywhere와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 FilesAnywhere 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="db557-103">자습서:FilesAnywhere와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="db557-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="db557-104">이 자습서에서는 Azure AD(Azure Active Directory)와 FilesAnywhere를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db557-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db557-105">FilesAnywhere를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="db557-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="db557-106">FilesAnywhere에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="db557-107">사용자가 해당 Azure AD 계정으로 FilesAnywhere에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db557-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="db557-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db557-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db557-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db557-110">Prerequisites</span></span>

<span data-ttu-id="db557-111">FilesAnywhere와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="db557-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="db557-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db557-113">FilesAnywhere Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="db557-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="db557-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="db557-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db557-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="db557-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="db557-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="db557-118">Scenario description</span></span>
<span data-ttu-id="db557-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db557-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db557-121">갤러리에서 FilesAnywhere 추가</span><span class="sxs-lookup"><span data-stu-id="db557-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="db557-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db557-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="db557-123">갤러리에서 FilesAnywhere 추가</span><span class="sxs-lookup"><span data-stu-id="db557-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="db557-124">FilesAnywhere를 Azure AD로 통합하도록 구성하려면 갤러리에서 FilesAnywhere를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="db557-125">**갤러리에서 FilesAnywhere를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db557-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="db557-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db557-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="db557-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="db557-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="db557-133">검색 상자에 **FilesAnywhere**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="db557-135">결과 창에서 **FilesAnywhere**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db557-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db557-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db557-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FilesAnywhere에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="db557-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 FilesAnywhere 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="db557-140">즉, Azure AD 사용자와 FilesAnywhere의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="db557-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 FilesAnywhere의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="db557-142">FilesAnywhere에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="db557-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="db557-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db557-145">**[FilesAnywhere 테스트 사용자 만들기](#creating-a-filesanywhere-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 FilesAnywhere에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db557-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="db557-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="db557-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db557-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="db557-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db557-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 FilesAnywhere 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="db557-150">**FilesAnywhere에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db557-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="db557-151">Azure 관리 포털의 **FilesAnywhere** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="db557-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="db557-155">**FilesAnywhere 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="db557-157">a.</span><span class="sxs-lookup"><span data-stu-id="db557-157">a.</span></span> <span data-ttu-id="db557-158">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="db557-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="db557-159">값 **215**가 **clientid**이지만 이것은 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="db557-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="db557-160">이 값을 실제 clientid 값으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="db557-161">**FilesAnywhere 도메인 및 URL** 섹션에서 **SP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="db557-163">a.</span><span class="sxs-lookup"><span data-stu-id="db557-163">a.</span></span> <span data-ttu-id="db557-164">**고급 URL 설정 표시** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="db557-165">b.</span><span class="sxs-lookup"><span data-stu-id="db557-165">b.</span></span> <span data-ttu-id="db557-166">**로그온 URL** 텍스트 상자에서 다음 패턴 `https://<sub domain>.filesanywhere.com/`을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="db557-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="db557-167">Please note that these are not the real values.</span></span> <span data-ttu-id="db557-168">실제 로그온 URL 및 회신 URL로 값을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="db557-169">이러한 값을 얻으려면 [FilesAnywhere 지원 팀](mailto:support@FilesAnywhere.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="db557-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="db557-170">FilesAnywhere Software 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="db557-171">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="db557-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="db557-172">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="db557-173">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db557-173">The following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="db557-175">사용자가 FilesAnywhere로 등록할 때 [FilesAnywhere 팀](mailto:support@FilesAnywhere.com)으로부터 **clientid** 특성 값을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="db557-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="db557-176">FilesAnywhere가 제공된 고유한 값을 사용하여 "클라이언트 ID" 특성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="db557-177">위에 표시된 모든 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="db557-178">**clientid**의 값 **2331**은 예일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="db557-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="db557-179">사용자는 실제 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="db557-180">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="db557-181">특성 이름</span><span class="sxs-lookup"><span data-stu-id="db557-181">Attribute Name</span></span> | <span data-ttu-id="db557-182">특성 값</span><span class="sxs-lookup"><span data-stu-id="db557-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="db557-183">clientid</span><span class="sxs-lookup"><span data-stu-id="db557-183">clientid</span></span> | <span data-ttu-id="db557-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="db557-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="db557-185">a.</span><span class="sxs-lookup"><span data-stu-id="db557-185">a.</span></span> <span data-ttu-id="db557-186">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db557-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="db557-189">b.</span><span class="sxs-lookup"><span data-stu-id="db557-189">b.</span></span> <span data-ttu-id="db557-190">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="db557-191">c.</span><span class="sxs-lookup"><span data-stu-id="db557-191">c.</span></span> <span data-ttu-id="db557-192">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="db557-193">d.</span><span class="sxs-lookup"><span data-stu-id="db557-193">d.</span></span> <span data-ttu-id="db557-194">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-194">Click **Ok**</span></span>

7. <span data-ttu-id="db557-195">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-195">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="db557-197">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="db557-199">**FilesAnywhere 구성** 섹션에서 **FilesAnywhere 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db557-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="db557-202">FilesAnywhere 쪽에서 응용 프로그램에 대한 SSO 구성이 완료되도록 하려면 [FilesAnywhere 지원 팀](mailto:support@FilesAnywhere.com)에 문의하고 다운로드된 SAML 토큰 서명 인증서 및 SSO(Single Sign On) URL을 제공하십시오.</span><span class="sxs-lookup"><span data-stu-id="db557-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db557-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db557-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="db557-204">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db557-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="db557-206">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="db557-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="db557-207">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db557-209">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db557-211">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db557-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db557-213">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db557-215">a.</span><span class="sxs-lookup"><span data-stu-id="db557-215">a.</span></span> <span data-ttu-id="db557-216">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db557-217">b.</span><span class="sxs-lookup"><span data-stu-id="db557-217">b.</span></span> <span data-ttu-id="db557-218">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db557-219">c.</span><span class="sxs-lookup"><span data-stu-id="db557-219">c.</span></span> <span data-ttu-id="db557-220">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="db557-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="db557-221">d.</span><span class="sxs-lookup"><span data-stu-id="db557-221">d.</span></span> <span data-ttu-id="db557-222">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="db557-223">FilesAnywhere 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db557-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="db557-224">응용 프로그램이 JIT(Just-in-time) 사용자 프로비저닝을 지원하며 인증 후에 응용 프로그램에서 사용자가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db557-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="db557-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="db557-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="db557-226">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 FilesAnywhere에 대한 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![사용자 할당][200] 

<span data-ttu-id="db557-228">**Britta Simon을 FilesAnywhere에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="db557-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="db557-229">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="db557-231">응용 프로그램 목록에서 **FilesAnywhere**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="db557-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-233">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="db557-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-235">Click **Add** button.</span></span> <span data-ttu-id="db557-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="db557-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="db557-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db557-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="db557-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="db557-241">Testing single sign-on</span></span>

<span data-ttu-id="db557-242">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db557-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="db557-243">액세스 패널에서 FilesAnywhere 타일을 클릭하면 FilesAnywhere 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="db557-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="db557-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="db557-244">Additional resources</span></span>

* [<span data-ttu-id="db557-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="db557-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db557-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="db557-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
