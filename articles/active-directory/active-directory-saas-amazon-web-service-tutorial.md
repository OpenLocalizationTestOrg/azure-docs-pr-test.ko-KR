---
title: "자습서: AWS(Amazon Web Services)와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Amazon Web Services(AWS) 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="ab220-103">자습서: AWS(Amazon Web Services)와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ab220-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="ab220-104">이 자습서에서는 Amazon Web Services(AWS)를 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab220-105">AWS(Amazon Web Services)를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ab220-106">Azure AD에서는 AWS(Amazon Web Services)에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="ab220-107">사용자가 Azure AD 계정으로 AWS(Amazon Web Services)에 자동으로 로그인(Single Sign-On)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab220-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ab220-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab220-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="ab220-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ab220-110">Prerequisites</span></span>

<span data-ttu-id="ab220-111">AWS(Amazon Web Services)와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="ab220-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ab220-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab220-113">AWS(Amazon Web Services) Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ab220-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab220-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab220-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab220-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ab220-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab220-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ab220-118">Scenario description</span></span>
<span data-ttu-id="ab220-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab220-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab220-121">갤러리에서 AWS(Amazon Web Services) 추가</span><span class="sxs-lookup"><span data-stu-id="ab220-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="ab220-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ab220-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="ab220-123">갤러리에서 AWS(Amazon Web Services) 추가</span><span class="sxs-lookup"><span data-stu-id="ab220-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="ab220-124">Azure AD에 AWS(Amazon Web Services)를 통합하도록 구성하려면 갤러리의 AWS(Amazon Web Services)를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ab220-125">**갤러리에서 AWS(Amazon Web Services)를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ab220-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ab220-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab220-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ab220-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ab220-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ab220-133">검색 상자에서 **AWS(Amazon Web Services)**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="ab220-135">결과 창에서 **AWS(Amazon Web Services)**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab220-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ab220-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab220-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AWS(Amazon Web Services)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab220-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 AWS(Amazon Web Services) 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="ab220-140">즉 Azure AD 사용자와 AWS(Amazon Web Services)의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="ab220-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 AWS(Amazon Web Services)의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="ab220-142">AWS(Amazon Web Services)에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ab220-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ab220-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab220-145">**[AWS(Amazon Web Services) 테스트 사용자 만들기](#creating-an-amazon-web-services-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 AWS(Amazon Web Services)에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ab220-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab220-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab220-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ab220-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab220-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 AWS(Amazon Web Services) 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="ab220-150">**AWS(Amazon Web Services)에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ab220-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="ab220-151">Azure Portal의 **AWS(Amazon Web Services)** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ab220-153">**Single Sign-On** 대화 상자에서 **모드**로 **SAML 기반 로그인**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="ab220-155">**AWS(Amazon Web Services) 도메인 및 URL** 섹션에서 앱이 Azure와 이미 사전 통합되었으므로 사용자는 아무 단계도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="ab220-157">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Single Sign-On 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="ab220-159">AWS(Amazon Web Services) 소프트웨어 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ab220-160">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="ab220-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="ab220-161">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ab220-162">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-162">The following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="ab220-164">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="ab220-165">특성 이름</span><span class="sxs-lookup"><span data-stu-id="ab220-165">Attribute Name</span></span>  | <span data-ttu-id="ab220-166">특성 값</span><span class="sxs-lookup"><span data-stu-id="ab220-166">Attribute Value</span></span> | <span data-ttu-id="ab220-167">네임스페이스</span><span class="sxs-lookup"><span data-stu-id="ab220-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="ab220-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="ab220-168">RoleSessionName</span></span> | <span data-ttu-id="ab220-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ab220-169">user.userprincipalname</span></span> | <span data-ttu-id="ab220-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="ab220-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="ab220-171">역할</span><span class="sxs-lookup"><span data-stu-id="ab220-171">Role</span></span>            | <span data-ttu-id="ab220-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="ab220-172">user.assignedroles</span></span> |  <span data-ttu-id="ab220-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="ab220-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="ab220-174">AWS 콘솔에서 모든 역할을 가져오려면 Azure AD에서 사용자 프로비전을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="ab220-175">프로비전 단계는 아래에서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab220-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="ab220-176">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-176">a.</span></span> <span data-ttu-id="ab220-177">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ab220-179">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-179">b.</span></span> <span data-ttu-id="ab220-180">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ab220-182">c.</span><span class="sxs-lookup"><span data-stu-id="ab220-182">c.</span></span> <span data-ttu-id="ab220-183">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="ab220-184">네임스페이스 값을 위에 지정된 대로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="ab220-185">d.</span><span class="sxs-lookup"><span data-stu-id="ab220-185">d.</span></span> <span data-ttu-id="ab220-186">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-186">Click **Ok**.</span></span>

7. <span data-ttu-id="ab220-187">**저장** 단추를 클릭하여 Azure에 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ab220-189">다른 브라우저 창에서 AWS(Amazon Web Services) 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="ab220-190">**콘솔 홈**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-190">Click **Console Home**.</span></span>
   
    ![Single Sign-On 구성][11]

10. <span data-ttu-id="ab220-192">**Security, Identity & Compliance(보안, ID 및 규정 준수)** 서비스에서 **IAM**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Single Sign-on 구성][12]

11. <span data-ttu-id="ab220-194">**ID 공급자**를 클릭한 다음 **공급자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Single Sign-On 구성][13]

12. <span data-ttu-id="ab220-196">**공급자 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Single Sign-On 구성][14]
 
    <span data-ttu-id="ab220-198">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-198">a.</span></span> <span data-ttu-id="ab220-199">**공급자 유형**으로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="ab220-200">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-200">b.</span></span> <span data-ttu-id="ab220-201">**공급자 이름** 텍스트 상자에 공급자 이름(예: *WAAD*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="ab220-202">c.</span><span class="sxs-lookup"><span data-stu-id="ab220-202">c.</span></span> <span data-ttu-id="ab220-203">다운로드한 메타데이터 파일을 업로드하려면 **파일 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="ab220-204">d.</span><span class="sxs-lookup"><span data-stu-id="ab220-204">d.</span></span> <span data-ttu-id="ab220-205">**다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="ab220-206">**공급자 정보 확인** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Single Sign-On 구성][15]

14. <span data-ttu-id="ab220-208">**역할**을 클릭하고 **새 역할 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Single Sign-on 구성][16]

15. <span data-ttu-id="ab220-210">**역할 이름 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Single Sign-On 구성][17] 

    <span data-ttu-id="ab220-212">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-212">a.</span></span> <span data-ttu-id="ab220-213">**역할 이름** 텍스트 상자에 역할 이름(예: *TestUser*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="ab220-214">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-214">b.</span></span> <span data-ttu-id="ab220-215">**다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="ab220-216">**역할 유형 선택** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Single Sign-On 구성][18] 

    <span data-ttu-id="ab220-218">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-218">a.</span></span> <span data-ttu-id="ab220-219">**ID 공급자 액세스에 대한 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="ab220-220">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-220">b.</span></span> <span data-ttu-id="ab220-221">**SAML 공급자에게 WebSSO(웹 Single Sign-On) 액세스 권한 부여** 섹션에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="ab220-222">**트러스트 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Single Sign-On 구성][19] 

    <span data-ttu-id="ab220-224">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-224">a.</span></span> <span data-ttu-id="ab220-225">이전에 만든 SAML 공급자(예: *WAAD*)를 SAML 공급자로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="ab220-226">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-226">b.</span></span> <span data-ttu-id="ab220-227">**다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="ab220-228">**역할 트러스트 확인** 대화 상자에서 **다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Single Sign-on 구성][32]

19. <span data-ttu-id="ab220-230">**정책 연결** 대화 상자에서 **다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Single Sign-on 구성][33]

20. <span data-ttu-id="ab220-232">**검토** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Single Sign-On 구성][34]
 
    <span data-ttu-id="ab220-234">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-234">a.</span></span> <span data-ttu-id="ab220-235">**역할 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-235">Click **Create Role**.</span></span>

    <span data-ttu-id="ab220-236">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-236">b.</span></span> <span data-ttu-id="ab220-237">필요한 만큼 역할을 만들어서 ID 공급자에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="ab220-238">이제 AWS에서 모든 역할을 가져오도록 사용자 프로비전을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="ab220-239">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-239">a.</span></span> <span data-ttu-id="ab220-240">AWS 콘솔에서 루트 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="ab220-241">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-241">b.</span></span> <span data-ttu-id="ab220-242">오른쪽 위 모서리에서 이름을 클릭한 다음 **My Security Credentials(내 보안 자격 증명)** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="ab220-243">그러면 화면이 경고 메시지로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="ab220-244">**Security Credentials(보안 자격 증명)** 단추를 클릭하여 화면을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Single Sign-On 구성][36]

       ![Single Sign-On 구성][37]

    <span data-ttu-id="ab220-247">c.</span><span class="sxs-lookup"><span data-stu-id="ab220-247">c.</span></span> <span data-ttu-id="ab220-248">액세스 키 섹션에서 **Create New Access Key(새 액세스 키 만들기)** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="ab220-249">그러면 액세스 키 ID와 토큰 값이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Single Sign-on 구성][38]

    <span data-ttu-id="ab220-251">d.</span><span class="sxs-lookup"><span data-stu-id="ab220-251">d.</span></span> <span data-ttu-id="ab220-252">이 값을 읽어버리지 않도록 모두 복사하고 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="ab220-253">e.</span><span class="sxs-lookup"><span data-stu-id="ab220-253">e.</span></span> <span data-ttu-id="ab220-254">Azure Portal의 AWS(Amazon Web Services) 응용 프로그램 통합 페이지에서 **프로비전**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Single Sign-on 구성][35]

    <span data-ttu-id="ab220-256">f.</span><span class="sxs-lookup"><span data-stu-id="ab220-256">f.</span></span> <span data-ttu-id="ab220-257">프로비전 모드를 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Single Sign-on 구성][39]

    <span data-ttu-id="ab220-259">g.</span><span class="sxs-lookup"><span data-stu-id="ab220-259">g.</span></span> <span data-ttu-id="ab220-260">이제 **clientsecret** 및 **비밀 토큰**에 AWS 콘솔에서 복사한 해당 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="ab220-261">h.</span><span class="sxs-lookup"><span data-stu-id="ab220-261">h.</span></span> <span data-ttu-id="ab220-262">**연결 테스트** 단추를 클릭하여 연결을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="ab220-263">성공적으로 수행되면 프로비전 커넥터를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Single Sign-on 구성][40]

    <span data-ttu-id="ab220-265">i.</span><span class="sxs-lookup"><span data-stu-id="ab220-265">i.</span></span> <span data-ttu-id="ab220-266">이제 프로비전 상태를 **설정**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="ab220-267">그러면 응용 프로그램에서 역할을 가져오기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-267">This starts fetching the roles from the application.</span></span>

       ![Single Sign-on 구성][41]

    > [!NOTE]
    > <span data-ttu-id="ab220-269">Azure AD 프로비전 서비스는 일정 시간 후마다 실행되어 AWS의 역할을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="ab220-270">모든 ID 공급자가 AWS 역할을 Azure AD에 연결한 것을 볼 수 있으며 사용자 또는 그룹에 응용 프로그램을 할당하는 동안 이것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab220-271">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ab220-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab220-272">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ab220-274">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="ab220-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ab220-275">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab220-277">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab220-279">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab220-281">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab220-283">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-283">a.</span></span> <span data-ttu-id="ab220-284">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab220-285">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-285">b.</span></span> <span data-ttu-id="ab220-286">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab220-287">c.</span><span class="sxs-lookup"><span data-stu-id="ab220-287">c.</span></span> <span data-ttu-id="ab220-288">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ab220-289">d.</span><span class="sxs-lookup"><span data-stu-id="ab220-289">d.</span></span> <span data-ttu-id="ab220-290">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="ab220-291">AWS(Amazon Web Services) 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ab220-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="ab220-292">Azure AD 사용자가 AWS(Amazon Web Services)에 로그인할 수 있도록 하려면 사용자가 AWS(Amazon Web Services)에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="ab220-293">AWS(Amazon Web Services)의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="ab220-294">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ab220-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ab220-295">**AWS(Amazon Web Services)** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="ab220-296">**콘솔 홈** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-296">Click the **Console Home** icon.</span></span> 
   
    ![Single Sign-On 구성][11]

3. <span data-ttu-id="ab220-298">ID 및 액세스 관리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-298">Click Identity and Access Management.</span></span> 
   
    ![Single Sign-on 구성][28]

4. <span data-ttu-id="ab220-300">대시보드에서 **Users(사용자)**를 클릭한 다음 **Create New Users(새 사용자 만들기)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Single Sign-On 구성][29]

5. <span data-ttu-id="ab220-302">사용자 만들기 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Single Sign-On 구성][30]   
    
    <span data-ttu-id="ab220-304">a.</span><span class="sxs-lookup"><span data-stu-id="ab220-304">a.</span></span> <span data-ttu-id="ab220-305">**사용자 이름 입력** 텍스트 상자에 Azure AD의 Brita Simon 사용자 이름(userprincipalname)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="ab220-306">b.</span><span class="sxs-lookup"><span data-stu-id="ab220-306">b.</span></span> <span data-ttu-id="ab220-307">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ab220-308">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="ab220-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ab220-309">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 AWS(Amazon Web Services)에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![사용자 할당][200] 

<span data-ttu-id="ab220-311">**Britta Simon을 AWS(Amazon Web Services)에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ab220-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="ab220-312">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ab220-314">응용 프로그램 목록에서 **AWS(Amazon Web Services)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="ab220-316">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-316">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ab220-318">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-318">Click **Add** button.</span></span> <span data-ttu-id="ab220-319">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ab220-321">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ab220-322">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab220-323">**역할 선택** 탭에서 사용자에게 적합한 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="ab220-324">모든 역할은 역할 이름 및 ID 공급자 이름으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="ab220-325">이러한 방식으로 AWS에서 역할을 손쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="ab220-326">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab220-327">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ab220-327">Testing single sign-on</span></span>

<span data-ttu-id="ab220-328">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ab220-329">[액세스 패널]에서 [AWS(Amazon Web Services)] 타일을 클릭하면 AWS(Amazon Web Services) 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab220-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab220-330">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ab220-330">Additional resources</span></span>

* [<span data-ttu-id="ab220-331">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="ab220-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab220-332">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ab220-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
