---
title: "자습서: ArcGIS Online과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 ArcGIS Online 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="5f2a5-103">자습서: ArcGIS Online과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5f2a5-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="5f2a5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 ArcGIS Online을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f2a5-105">ArcGIS Online을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5f2a5-106">ArcGIS Online에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="5f2a5-107">사용자가 해당 Azure AD 계정으로 ArcGIS Online에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f2a5-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5f2a5-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="5f2a5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5f2a5-110">Prerequisites</span></span>

<span data-ttu-id="5f2a5-111">ArcGIS Online과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="5f2a5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5f2a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f2a5-113">ArcGIS Online Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5f2a5-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f2a5-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f2a5-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f2a5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f2a5-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f2a5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5f2a5-118">Scenario description</span></span>
<span data-ttu-id="5f2a5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f2a5-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f2a5-121">갤러리에서 ArcGIS Online 추가</span><span class="sxs-lookup"><span data-stu-id="5f2a5-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="5f2a5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5f2a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="5f2a5-123">갤러리에서 ArcGIS Online 추가</span><span class="sxs-lookup"><span data-stu-id="5f2a5-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="5f2a5-124">ArcGIS Online의 Azure AD 통합을 구성하려면 갤러리의 ArcGIS Online을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5f2a5-125">**갤러리에서 ArcGIS Online을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5f2a5-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5f2a5-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5f2a5-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5f2a5-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5f2a5-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭하여 새 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5f2a5-133">검색 상자에 **ArcGIS Online**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="5f2a5-135">결과 패널에서 **ArcGIS Online**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f2a5-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5f2a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f2a5-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ArcGIS Online에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5f2a5-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 ArcGIS Online 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="5f2a5-140">즉, Azure AD 사용자와 ArcGIS Online의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="5f2a5-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 ArcGIS Online의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="5f2a5-142">ArcGIS Online에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5f2a5-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5f2a5-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f2a5-145">**[ArcGIS Online 테스트 사용자 만들기](#creating-an-arcgis-online-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 ArcGIS Online에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f2a5-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f2a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f2a5-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5f2a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f2a5-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 ArcGIS Online 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="5f2a5-150">**ArcGIS Online에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5f2a5-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="5f2a5-151">Azure Portal의 **ArcGIS Online** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5f2a5-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="5f2a5-155">**ArcGIS Online 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="5f2a5-157">**로그온 URL** 텍스트 상자에 다음 패턴으로 값을 입력합니다. `https://<company>.maps.arcgis.com` </span><span class="sxs-lookup"><span data-stu-id="5f2a5-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f2a5-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-158">This value is not the real.</span></span> <span data-ttu-id="5f2a5-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="5f2a5-160">이 값을 가져오려면 [ArcGIS Online 클라이언트 지원팀](http://support.esri.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="5f2a5-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="5f2a5-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f2a5-165">다른 웹 브라우저 창에서 ArcGIS 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="5f2a5-166">**설정 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="5f2a5-167">![설정 편집](./media/active-directory-saas-arcgis-tutorial/ic784742.png "설정 편집")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="5f2a5-168">**보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-168">Click **Security**.</span></span>

    <span data-ttu-id="5f2a5-169">![보안](./media/active-directory-saas-arcgis-tutorial/ic784743.png "보안")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="5f2a5-170">**회사 로그인**에서 **ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="5f2a5-171">![회사 로그인](./media/active-directory-saas-arcgis-tutorial/ic784744.png "회사 로그인")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="5f2a5-172">**ID 공급자 설정** 구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="5f2a5-173">![ID 공급자 설정](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ID 공급자 설정")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="5f2a5-174">a.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-174">a.</span></span> <span data-ttu-id="5f2a5-175">**이름** 텍스트 상자에 조직의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="5f2a5-176">b.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-176">b.</span></span> <span data-ttu-id="5f2a5-177">**회사 ID 공급자에 대한 메타데이터를 다음을 사용하여 제공합니다**에서 **파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="5f2a5-178">c.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-178">c.</span></span> <span data-ttu-id="5f2a5-179">다운로드한 메타데이터 파일을 업로드하려면 **파일 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="5f2a5-180">d.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-180">d.</span></span> <span data-ttu-id="5f2a5-181">**ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="5f2a5-182">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5f2a5-183">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5f2a5-184">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f2a5-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5f2a5-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f2a5-186">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5f2a5-188">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5f2a5-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5f2a5-189">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f2a5-191">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f2a5-193">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f2a5-195">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f2a5-197">a.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-197">a.</span></span> <span data-ttu-id="5f2a5-198">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f2a5-199">b.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-199">b.</span></span> <span data-ttu-id="5f2a5-200">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="5f2a5-201">c.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-201">c.</span></span> <span data-ttu-id="5f2a5-202">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5f2a5-203">d.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-203">d.</span></span> <span data-ttu-id="5f2a5-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="5f2a5-205">ArcGIS Online 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5f2a5-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="5f2a5-206">Azure AD 사용자가 ArcGIS Online에 로그인할 수 있도록 하려면 ArcGIS Online으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="5f2a5-207">ArcGIS Online의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="5f2a5-208">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5f2a5-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5f2a5-209">**ArcGIS** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="5f2a5-210">**멤버 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="5f2a5-211">![멤버 초대](./media/active-directory-saas-arcgis-tutorial/ic784747.png "멤버 초대")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="5f2a5-212">**전자 메일을 보내지 않고 멤버를 자동으로 추가**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="5f2a5-213">![멤버를 자동으로 추가](./media/active-directory-saas-arcgis-tutorial/ic784748.png "멤버를 자동으로 추가")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="5f2a5-214">**멤버** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="5f2a5-215">![추가 및 검토](./media/active-directory-saas-arcgis-tutorial/ic784749.png "추가 및 검토")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="5f2a5-216">a.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-216">a.</span></span> <span data-ttu-id="5f2a5-217">프로비전하려는 유효한 AAD 계정의 **전자 메일**, **이름** 및 **성**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="5f2a5-218">b.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-218">b.</span></span> <span data-ttu-id="5f2a5-219">**추가 및 검토**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="5f2a5-220">입력한 데이터를 검토한 다음 **멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="5f2a5-221">![멤버 추가](./media/active-directory-saas-arcgis-tutorial/ic784750.png "멤버 추가")</span><span class="sxs-lookup"><span data-stu-id="5f2a5-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="5f2a5-222">Azure Active Directory 계정 보유자는 활성화되기 전에 전자 메일을 받고 링크를 따라 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5f2a5-223">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5f2a5-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5f2a5-224">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 ArcGIS Online에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5f2a5-226">**Britta Simon을 ArcGIS Online에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5f2a5-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="5f2a5-227">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5f2a5-229">응용 프로그램 목록에서 **ArcGIS Online**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="5f2a5-231">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-231">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5f2a5-233">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-233">Click **Add** button.</span></span> <span data-ttu-id="5f2a5-234">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5f2a5-236">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5f2a5-237">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f2a5-238">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f2a5-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5f2a5-239">Testing single sign-on</span></span>

<span data-ttu-id="5f2a5-240">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5f2a5-241">액세스 패널에서 ArcGIS Online 타일을 클릭하면 ArcGIS Online 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="5f2a5-242">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f2a5-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f2a5-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5f2a5-243">Additional resources</span></span>

* [<span data-ttu-id="5f2a5-244">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5f2a5-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f2a5-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5f2a5-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

