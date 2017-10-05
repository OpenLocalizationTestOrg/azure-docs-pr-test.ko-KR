---
title: "자습서: Atlassian Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Atlassian Cloud 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="2ca06-103">자습서: Atlassian Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2ca06-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="2ca06-104">이 자습서에서는 Atlassian Cloud와 Azure AD(Azure Active Directory)를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ca06-105">Atlassian Cloud를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2ca06-106">Azure AD에서는 Atlassian Cloud에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="2ca06-107">사용자가 Azure AD 계정으로 Atlassian Cloud에 자동으로 로그인(Single Sign-on)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ca06-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2ca06-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ca06-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ca06-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ca06-110">Prerequisites</span></span>

<span data-ttu-id="2ca06-111">Atlassian Cloud와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="2ca06-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2ca06-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ca06-113">Atlassian Cloud Single Sign-On 사용이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2ca06-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ca06-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ca06-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ca06-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2ca06-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ca06-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ca06-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2ca06-118">Scenario description</span></span>
<span data-ttu-id="2ca06-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ca06-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ca06-121">갤러리에서 Atlassian Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="2ca06-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="2ca06-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2ca06-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="2ca06-123">갤러리에서 Atlassian Cloud 추가</span><span class="sxs-lookup"><span data-stu-id="2ca06-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="2ca06-124">Azure AD에 Atlassian Cloud와 Azure AD를 통합하도록 구성하려면 갤러리의 Atlassian Cloud를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2ca06-125">**갤러리에서 Atlassian Cloud를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2ca06-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2ca06-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ca06-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2ca06-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2ca06-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2ca06-133">검색 상자에서 **Atlassian Cloud**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="2ca06-135">결과 패널에서 **Atlassian Cloud**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ca06-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2ca06-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ca06-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 Atlassian Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ca06-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 Atlassian Cloud 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="2ca06-140">즉 Azure AD 사용자와 Atlassian Cloud의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="2ca06-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Atlassian Cloud의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="2ca06-142">Atlassian Cloud에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2ca06-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2ca06-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ca06-145">**[Atlassian Cloud 테스트 사용자 만들기](#creating-an-atlassian-cloud-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Atlassian Cloud에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ca06-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ca06-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ca06-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2ca06-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ca06-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Atlassian Cloud 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="2ca06-150">**Atlassian Cloud에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2ca06-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="2ca06-151">Azure Portal의 **Atlassian Cloud** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2ca06-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="2ca06-155">**Atlassian Cloud 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="2ca06-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ca06-157">a.</span></span> <span data-ttu-id="2ca06-158">**식별자** 텍스트 상자에서 `https://<instancename>.atlassian.net/admin/saml/edit` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="2ca06-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ca06-159">b.</span></span> <span data-ttu-id="2ca06-160">**회신 URL** 텍스트 상자에서 URL을 `https://id.atlassian.com/login/saml/acs`로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="2ca06-161">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 확인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="2ca06-163">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="2ca06-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ca06-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-164">These values are not real.</span></span> <span data-ttu-id="2ca06-165">실제 식별자 및 로그온 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="2ca06-166">Atlassian Cloud SAML 구성 화면에서 정확한 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="2ca06-167">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="2ca06-169">**Atlassian Cloud 구성** 섹션에서 **Atlassian Cloud 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2ca06-170">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="2ca06-172">응용 프로그램에 SSO를 구성하려면 관리자 권한으로 Atlassian Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="2ca06-173">왼쪽 탐색 모음의 [인증] 섹션에서 **도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="2ca06-175">a.</span><span class="sxs-lookup"><span data-stu-id="2ca06-175">a.</span></span> <span data-ttu-id="2ca06-176">텍스트 상자에서 도메인 이름을 입력한 다음 **도메인 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="2ca06-178">b.</span><span class="sxs-lookup"><span data-stu-id="2ca06-178">b.</span></span> <span data-ttu-id="2ca06-179">도메인을 확인하려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-179">To verify the domain, click **Verify**.</span></span> 

    ![Single Sign-On 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="2ca06-181">c.</span><span class="sxs-lookup"><span data-stu-id="2ca06-181">c.</span></span> <span data-ttu-id="2ca06-182">도메인 확인 HTML 파일을 다운로드하여 도메인 웹 사이트의 루트 폴더에 업로드한 다음 **도메인 확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="2ca06-184">d.</span><span class="sxs-lookup"><span data-stu-id="2ca06-184">d.</span></span> <span data-ttu-id="2ca06-185">도메인이 확인되면 **상태** 필드 값이 **확인됨**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="2ca06-187">왼쪽 탐색 모음에서 **SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="2ca06-189">SAML 구성을 만들고 ID 공급자 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="2ca06-191">a.</span><span class="sxs-lookup"><span data-stu-id="2ca06-191">a.</span></span> <span data-ttu-id="2ca06-192">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **Identity provider Entity ID**(ID 공급자 엔터티 ID) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ca06-193">b.</span><span class="sxs-lookup"><span data-stu-id="2ca06-193">b.</span></span> <span data-ttu-id="2ca06-194">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 SSO URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ca06-195">c.</span><span class="sxs-lookup"><span data-stu-id="2ca06-195">c.</span></span> <span data-ttu-id="2ca06-196">Azure Portal에서 다운로드한 인증서를 열고 시작 및 끝 행을 제외한 값을 복사하여 **공용 X509 인증서** 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="2ca06-197">d.</span><span class="sxs-lookup"><span data-stu-id="2ca06-197">d.</span></span> <span data-ttu-id="2ca06-198">**구성 저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="2ca06-199">Azure AD 설정을 업데이트하여 올바른 식별자 URL을 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="2ca06-200">a.</span><span class="sxs-lookup"><span data-stu-id="2ca06-200">a.</span></span> <span data-ttu-id="2ca06-201">SAML 화면에서 **SP Identity ID**(SP ID)를 복사하여 Azure AD에 **식별자** 값으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="2ca06-202">b.</span><span class="sxs-lookup"><span data-stu-id="2ca06-202">b.</span></span> <span data-ttu-id="2ca06-203">[로그인 URL]은 Atlassian Cloud의 테넌트 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="2ca06-205">Azure Portal에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-205">In the Azure portal, Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="2ca06-207">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2ca06-208">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2ca06-209">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ca06-210">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2ca06-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ca06-211">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2ca06-213">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="2ca06-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2ca06-214">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ca06-216">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ca06-218">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ca06-220">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ca06-222">a.</span><span class="sxs-lookup"><span data-stu-id="2ca06-222">a.</span></span> <span data-ttu-id="2ca06-223">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ca06-224">b.</span><span class="sxs-lookup"><span data-stu-id="2ca06-224">b.</span></span> <span data-ttu-id="2ca06-225">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ca06-226">c.</span><span class="sxs-lookup"><span data-stu-id="2ca06-226">c.</span></span> <span data-ttu-id="2ca06-227">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2ca06-228">d.</span><span class="sxs-lookup"><span data-stu-id="2ca06-228">d.</span></span> <span data-ttu-id="2ca06-229">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="2ca06-230">Atlassian Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2ca06-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="2ca06-231">Azure AD 사용자가 Atlassian Cloud에 로그인할 수 있도록 하려면 Atlassian Cloud로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="2ca06-232">Atlassian Cloud의 경우 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="2ca06-233">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2ca06-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2ca06-234">[사이트 관리] 섹션에서 **사용자** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-234">In the Site administration section, click the **Users** button</span></span>

    ![Atlassian Cloud 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="2ca06-236">Atlassian Cloud에서 사용자를 만들기 위해 **사용자 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Atlassian Cloud 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="2ca06-238">사용자의 **메일 주소**, **사용자 이름** 및 **전체 이름**을 입력하고 응용 프로그램 액세스 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Atlassian Cloud 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="2ca06-240">**사용자 만들기** 단추를 클릭하면 사용자에게 메일 초대장을 보내고 이 초대를 수락하면 해당 사용자가 시스템에서 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="2ca06-241">[사용자] 섹션에서 **대량 만들기** 단추를 클릭하여 대량으로 사용자를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2ca06-242">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="2ca06-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2ca06-243">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Atlassian Cloud에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2ca06-245">**Britta Simon을 Atlassian Cloud에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="2ca06-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="2ca06-246">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2ca06-248">응용 프로그램 목록에서 **Atlassian Cloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="2ca06-250">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-250">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2ca06-252">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-252">Click **Add** button.</span></span> <span data-ttu-id="2ca06-253">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2ca06-255">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2ca06-256">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ca06-257">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ca06-258">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2ca06-258">Testing single sign-on</span></span>

<span data-ttu-id="2ca06-259">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="2ca06-260">[액세스 패널]에서 [Atlassian Cloud] 타일을 클릭하면 Atlassian Cloud 응용 프로그램에 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ca06-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="2ca06-261">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ca06-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2ca06-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2ca06-262">Additional resources</span></span>

* [<span data-ttu-id="2ca06-263">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="2ca06-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ca06-264">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2ca06-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

