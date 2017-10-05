---
title: "자습서: Bambu by Sprout Social과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Bambu by Sprout Social 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="f52d9-103">자습서: Bambu by Sprout Social과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f52d9-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="f52d9-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Bambu by Sprout Social을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f52d9-105">Bambu by Sprout Social을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f52d9-106">Bambu by Sprout Social에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="f52d9-107">사용자가 해당 Azure AD 계정으로 Bambu by Sprout Social에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f52d9-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f52d9-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52d9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="f52d9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f52d9-110">Prerequisites</span></span>

<span data-ttu-id="f52d9-111">Bambu by Sprout Social과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="f52d9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f52d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f52d9-113">Bambu by Sprout Social Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f52d9-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f52d9-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f52d9-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f52d9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f52d9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f52d9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f52d9-118">Scenario description</span></span>
<span data-ttu-id="f52d9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f52d9-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f52d9-121">갤러리에서 Bambu by Sprout Social 추가</span><span class="sxs-lookup"><span data-stu-id="f52d9-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="f52d9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f52d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="f52d9-123">갤러리에서 Bambu by Sprout Social 추가</span><span class="sxs-lookup"><span data-stu-id="f52d9-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="f52d9-124">Bambu by Sprout Social의 Azure AD 통합을 구성하려면 갤러리의 Bambu by Sprout Social을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f52d9-125">**갤러리에서 Bambu by Sprout Social을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f52d9-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f52d9-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f52d9-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f52d9-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f52d9-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭하여 새 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f52d9-133">검색 상자에 **Bambu by Sprout Social**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="f52d9-135">결과 패널에서 **Bambu by Sprout Social**을 클릭한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f52d9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f52d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f52d9-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Bambu by Sprout Social에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f52d9-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Bambu by Sprout Social 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="f52d9-140">즉, Azure AD 사용자와 Bambu by Sprout Social의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="f52d9-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Bambu by Sprout Social의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="f52d9-142">Bambu by Sprout Social에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f52d9-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f52d9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f52d9-145">**[Bambu by Sprout Social 테스트 사용자 만들기](#creating-a-bambu-by-sprout-social-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Bambu by Sprout Social에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f52d9-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f52d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f52d9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f52d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f52d9-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Bambu by Sprout Social 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="f52d9-150">**Bambu by Sprout Social에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f52d9-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="f52d9-151">Azure Portal의 **Bambu by Sprout Social** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성][4]

2. <span data-ttu-id="f52d9-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="f52d9-155">**Bambu by Sprout Social 도메인 및 URL** 섹션에서 앱이 Azure와 이미 사전 통합되었으므로 사용자는 아무 단계도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="f52d9-157">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="f52d9-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-159">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f52d9-161">**Bambu by Sprout Social 구성** 섹션에서 **Bambu by Sprout Social 구성**을 클릭하여 **로그인 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f52d9-162">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="f52d9-164">**Bambu by Sprout Social** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML** 및 **SAML Single Sign-On 서비스 URL**을 [Bambu by Sprout Social 지원](mailto:support@getbambu.com)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="f52d9-165">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f52d9-166">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f52d9-167">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f52d9-168">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f52d9-169">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f52d9-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="f52d9-170">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f52d9-172">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f52d9-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f52d9-173">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f52d9-175">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f52d9-177">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f52d9-179">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f52d9-181">a.</span><span class="sxs-lookup"><span data-stu-id="f52d9-181">a.</span></span> <span data-ttu-id="f52d9-182">**이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="f52d9-183">b.</span><span class="sxs-lookup"><span data-stu-id="f52d9-183">b.</span></span> <span data-ttu-id="f52d9-184">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f52d9-185">c.</span><span class="sxs-lookup"><span data-stu-id="f52d9-185">c.</span></span> <span data-ttu-id="f52d9-186">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f52d9-187">d.</span><span class="sxs-lookup"><span data-stu-id="f52d9-187">d.</span></span> <span data-ttu-id="f52d9-188">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="f52d9-189">Bambu by Sprout Social 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f52d9-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="f52d9-190">응용 프로그램이 Just-In-Time 사용자 프로비전을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f52d9-191">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f52d9-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f52d9-192">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Bambu by Sprout Social에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f52d9-194">**Britta Simon을 Bambu by Sprout Social에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f52d9-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="f52d9-195">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f52d9-197">응용 프로그램 목록에서 **Bambu by Sprout Social**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="f52d9-199">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-199">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f52d9-201">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-201">Click **Add** button.</span></span> <span data-ttu-id="f52d9-202">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f52d9-204">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f52d9-205">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f52d9-206">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f52d9-207">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f52d9-207">Testing single sign-on</span></span>

<span data-ttu-id="f52d9-208">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f52d9-209">액세스 패널에서 Bambu by Sprout Social 타일을 클릭하면 Bambu by Sprout Social 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f52d9-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="f52d9-210">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52d9-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f52d9-211">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f52d9-211">Additional resources</span></span>

* [<span data-ttu-id="f52d9-212">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f52d9-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f52d9-213">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f52d9-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

