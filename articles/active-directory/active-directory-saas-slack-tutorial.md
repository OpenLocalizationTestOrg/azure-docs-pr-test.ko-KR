---
title: "자습서: Slack과 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Slack 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="8f5f5-103">자습서: Slack과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="8f5f5-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="8f5f5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Slack을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f5f5-105">Slack과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f5f5-106">Azure AD에서는 Slack에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="8f5f5-107">사용자가 Azure AD 계정으로 Slack에 자동으로 로그인(Single Sign-On)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f5f5-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f5f5-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f5f5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8f5f5-110">Prerequisites</span></span>

<span data-ttu-id="8f5f5-111">Slack과 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="8f5f5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="8f5f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f5f5-113">Slack Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="8f5f5-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f5f5-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f5f5-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f5f5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f5f5-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f5f5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="8f5f5-118">Scenario description</span></span>
<span data-ttu-id="8f5f5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f5f5-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f5f5-121">갤러리에서 Slack 추가</span><span class="sxs-lookup"><span data-stu-id="8f5f5-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="8f5f5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8f5f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="8f5f5-123">갤러리에서 Slack 추가</span><span class="sxs-lookup"><span data-stu-id="8f5f5-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="8f5f5-124">Azure AD에 Slack을 통합하도록 구성하려면 갤러리의 Slack을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f5f5-125">**갤러리에서 Slack을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8f5f5-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5f5-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f5f5-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f5f5-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="8f5f5-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="8f5f5-133">검색 상자에서 **Slack**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-133">In the search box, type **Slack**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="8f5f5-135">결과 창에서 **Slack**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f5f5-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8f5f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f5f5-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Slack에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8f5f5-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Slack 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="8f5f5-140">즉 Azure AD 사용자와 Slack의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="8f5f5-141">Slack에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8f5f5-142">Slack에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f5f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f5f5-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f5f5-145">**[Slack 테스트 사용자 만들기](#creating-a-slack-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Slack에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f5f5-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f5f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f5f5-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="8f5f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f5f5-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Slack 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="8f5f5-150">**Slack에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8f5f5-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5f5-151">Azure Portal의 **Slack** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="8f5f5-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="8f5f5-155">**Slack 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="8f5f5-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-157">a.</span></span> <span data-ttu-id="8f5f5-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="8f5f5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="8f5f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-159">b.</span></span> <span data-ttu-id="8f5f5-160">**식별자** 텍스트 상자에 URL `https://slack.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f5f5-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-161">The value is not real.</span></span> <span data-ttu-id="8f5f5-162">이 값은 실제 로그인 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="8f5f5-163">이러한 값을 얻으려면 [Slack 지원 팀](https://slack.com/help/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="8f5f5-164">Slack 응용 프로그램에는 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8f5f5-165">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-165">Configure the following claims for this application.</span></span> <span data-ttu-id="8f5f5-166">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8f5f5-167">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-167">The following screenshot shows an example for this.</span></span>
    
    ![Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="8f5f5-169">**Single sign on** 대화 상자의 **사용자 특성** 섹션에서 **사용자 식별자**로 **user.mail**을 선택하고 아래 표에 표시되는 각 행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="8f5f5-170">특성 이름</span><span class="sxs-lookup"><span data-stu-id="8f5f5-170">Attribute Name</span></span> | <span data-ttu-id="8f5f5-171">특성 값</span><span class="sxs-lookup"><span data-stu-id="8f5f5-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8f5f5-172">first_name</span><span class="sxs-lookup"><span data-stu-id="8f5f5-172">first_name</span></span> | <span data-ttu-id="8f5f5-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8f5f5-173">user.givenname</span></span> |
    | <span data-ttu-id="8f5f5-174">last_name</span><span class="sxs-lookup"><span data-stu-id="8f5f5-174">last_name</span></span> | <span data-ttu-id="8f5f5-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="8f5f5-175">user.surname</span></span> |
    | <span data-ttu-id="8f5f5-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="8f5f5-176">User.Email</span></span> | <span data-ttu-id="8f5f5-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="8f5f5-177">user.mail</span></span> |  
    | <span data-ttu-id="8f5f5-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="8f5f5-178">User.Username</span></span> | <span data-ttu-id="8f5f5-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8f5f5-179">user.userprincipalname</span></span> |

    <span data-ttu-id="8f5f5-180">a.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-180">a.</span></span> <span data-ttu-id="8f5f5-181">**특성**을 클릭하여 **특성 편집** 대화 상자를 열고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="8f5f5-183">a.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-183">a.</span></span> <span data-ttu-id="8f5f5-184">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8f5f5-185">b.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-185">b.</span></span> <span data-ttu-id="8f5f5-186">**값** 목록에서 해당 행에 표시된 특성 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8f5f5-187">c.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-187">c.</span></span> <span data-ttu-id="8f5f5-188">**확인**</span><span class="sxs-lookup"><span data-stu-id="8f5f5-188">Click **OK**</span></span>

6. <span data-ttu-id="8f5f5-189">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="8f5f5-191">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-191">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8f5f5-193">**Slack 구성** 섹션에서 **Slack 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8f5f5-194">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="8f5f5-196">다른 웹 브라우저 창에서 Slack 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="8f5f5-197">**Microsoft Azure AD**, **팀 설정**으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="8f5f5-199">**팀 설정** 섹션에서 **인증** 탭을 클릭한 다음 **설정 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="8f5f5-201">**SAML 인증 설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="8f5f5-203">a.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-203">a.</span></span>  <span data-ttu-id="8f5f5-204">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SAML 2.0 끝점(HTTP)** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8f5f5-205">b.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-205">b.</span></span>  <span data-ttu-id="8f5f5-206">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **ID 공급자 발급자** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8f5f5-207">c.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-207">c.</span></span>  <span data-ttu-id="8f5f5-208">다운로드한 인증서 파일을 메모장에서 열고 내용을 클립보드에 복사한 다음 **공용 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="8f5f5-209">d.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-209">d.</span></span> <span data-ttu-id="8f5f5-210">위의 세 가지 설정을 Slack 팀에 적합하게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="8f5f5-211">설정에 대한 자세한 내용은 **Slack의 SSO 구성 가이드**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="8f5f5-212">e.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-212">e.</span></span>  <span data-ttu-id="8f5f5-213">**구성 저장**을 클릭하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="8f5f5-214">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f5f5-215">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f5f5-216">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f5f5-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8f5f5-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f5f5-218">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="8f5f5-220">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="8f5f5-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5f5-221">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f5f5-223">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f5f5-225">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f5f5-227">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f5f5-229">a.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-229">a.</span></span> <span data-ttu-id="8f5f5-230">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f5f5-231">b.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-231">b.</span></span> <span data-ttu-id="8f5f5-232">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f5f5-233">c.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-233">c.</span></span> <span data-ttu-id="8f5f5-234">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f5f5-235">d.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-235">d.</span></span> <span data-ttu-id="8f5f5-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="8f5f5-237">Slack 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8f5f5-237">Creating a Slack test user</span></span>

<span data-ttu-id="8f5f5-238">이 섹션에서는 Slack에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="8f5f5-239">Slack은 just-in-time 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8f5f5-240">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-240">There is no action item for you in this section.</span></span> <span data-ttu-id="8f5f5-241">새 사용자가 아직 존재하지 않는 경우 Slack에 액세스하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="8f5f5-242">사용자를 수동으로 만들어야 하는 경우 [Slack 지원 팀](https://slack.com/help/contact)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f5f5-243">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="8f5f5-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f5f5-244">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Slack에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![사용자 할당][200] 

<span data-ttu-id="8f5f5-246">**Britta Simon을 Slack에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8f5f5-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="8f5f5-247">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="8f5f5-249">응용 프로그램 목록에서 **Slack**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-249">In the applications list, select **Slack**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="8f5f5-251">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-251">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="8f5f5-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-253">Click **Add** button.</span></span> <span data-ttu-id="8f5f5-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="8f5f5-256">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8f5f5-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f5f5-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f5f5-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="8f5f5-259">Testing single sign-on</span></span>

<span data-ttu-id="8f5f5-260">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8f5f5-261">[액세스 패널]에서 [Slack] 타일을 클릭하면 Slack 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f5f5-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f5f5-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8f5f5-262">Additional resources</span></span>

* [<span data-ttu-id="8f5f5-263">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="8f5f5-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f5f5-264">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8f5f5-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

