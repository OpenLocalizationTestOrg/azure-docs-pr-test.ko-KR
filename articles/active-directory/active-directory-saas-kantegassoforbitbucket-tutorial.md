---
title: "자습서: Kantega SSO for Bitbucket과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Kantega SSO for Bitbucket 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 6656c9abf8483ee98c0cb1a16c06d078e32240f2
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a><span data-ttu-id="c1d24-103">자습서: Kantega SSO for Bitbucket과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c1d24-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span></span>

<span data-ttu-id="c1d24-104">이 자습서에서는 Kantega SSO for Bitbucket을 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-104">In this tutorial, you learn how to integrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1d24-105">Kantega SSO for Bitbucket을 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1d24-106">Kantega SSO for Bitbucket에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-106">You can control in Azure AD who has access to Kantega SSO for Bitbucket</span></span>
- <span data-ttu-id="c1d24-107">사용자가 자신의 Azure AD 계정으로 Kantega SSO for Bitbucket에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-107">You can enable your users to automatically get signed-on to Kantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1d24-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c1d24-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1d24-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1d24-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c1d24-110">Prerequisites</span></span>

<span data-ttu-id="c1d24-111">Kantega SSO for Bitbucket과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-111">To configure Azure AD integration with Kantega SSO for Bitbucket, you need the following items:</span></span>

- <span data-ttu-id="c1d24-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c1d24-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1d24-113">Kantega SSO for Bitbucket Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c1d24-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1d24-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1d24-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1d24-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c1d24-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1d24-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1d24-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c1d24-118">Scenario description</span></span>
<span data-ttu-id="c1d24-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1d24-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1d24-121">갤러리에서 Kantega SSO for Bitbucket 추가</span><span class="sxs-lookup"><span data-stu-id="c1d24-121">Adding Kantega SSO for Bitbucket from the gallery</span></span>
2. <span data-ttu-id="c1d24-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c1d24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bitbucket-from-the-gallery"></a><span data-ttu-id="c1d24-123">갤러리에서 Kantega SSO for Bitbucket 추가</span><span class="sxs-lookup"><span data-stu-id="c1d24-123">Adding Kantega SSO for Bitbucket from the gallery</span></span>
<span data-ttu-id="c1d24-124">Kantega SSO for Bitbucket이 Azure AD에 통합되도록 구성하려면 갤러리에서 Kantega SSO for Bitbucket을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-124">To configure the integration of Kantega SSO for Bitbucket into Azure AD, you need to add Kantega SSO for Bitbucket from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1d24-125">**갤러리에서 Kantega SSO for Bitbucket을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1d24-125">**To add Kantega SSO for Bitbucket from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1d24-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1d24-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1d24-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c1d24-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c1d24-133">검색 상자에 **Kantega SSO for Bitbucket**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-133">In the search box, type **Kantega SSO for Bitbucket**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. <span data-ttu-id="c1d24-135">결과 창에서 **Kantega SSO for Bitbucket**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-135">In the results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1d24-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c1d24-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1d24-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Kantega SSO for Bitbucket에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1d24-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Kantega SSO for Bitbucket 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bitbucket is to a user in Azure AD.</span></span> <span data-ttu-id="c1d24-140">즉, Azure AD 사용자와 Kantega SSO for Bitbucket의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bitbucket needs to be established.</span></span>

<span data-ttu-id="c1d24-141">Kantega SSO for Bitbucket에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-141">In Kantega SSO for Bitbucket, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1d24-142">Kantega SSO for Bitbucket에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-142">To configure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1d24-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1d24-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1d24-145">**[Kantega SSO for Bitbucket 테스트 사용자 만들기](#creating-a-kantega-sso-for-bitbucket-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Kantega SSO for Bitbucket에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1d24-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1d24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1d24-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c1d24-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1d24-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Kantega SSO for Bitbucket 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span></span>

<span data-ttu-id="c1d24-150">**Kantega SSO for Bitbucket에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1d24-150">**To configure Azure AD single sign-on with Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="c1d24-151">Azure Portal의 **Kantega SSO for Bitbucket** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-151">In the Azure portal, on the **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c1d24-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. <span data-ttu-id="c1d24-155">**IDP** 시작 모드로 **Kantega SSO for Bitbucket 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-155">In **IDP** initiated mode, on the **Kantega SSO for Bitbucket Domain and URLs** section perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    <span data-ttu-id="c1d24-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-157">a.</span></span> <span data-ttu-id="c1d24-158">**식별자** 텍스트 상자에서 `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="c1d24-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-159">b.</span></span> <span data-ttu-id="c1d24-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="c1d24-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="c1d24-161">**SP** 시작 모드에서 **고급 URL 설정 표시**를 확인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    <span data-ttu-id="c1d24-163">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="c1d24-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1d24-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-164">These values are not real.</span></span> <span data-ttu-id="c1d24-165">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c1d24-166">이러한 값은 Bitbucket 플러그 인 구성 중에 수신되며 자습서의 뒷부분에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-166">These values are recieved during the configuration of Bitbucket plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="c1d24-167">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. <span data-ttu-id="c1d24-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c1d24-171">다른 웹 브라우저 창에서 Bitbucket 관리 포털에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-171">In a different web browser window, log in to your Bitbucket admin portal as an administrator.</span></span>

8. <span data-ttu-id="c1d24-172">톱니바퀴를 클릭하고 **Find new add-ons**(새 추가 기능 찾기)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-172">Click cog and click the **Find new add-ons**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. <span data-ttu-id="c1d24-174">**Kantega SSO for Bitbucket SAML & Kerberos**를 검색하고 **설치** 단추를 클릭하여 새 SAML 플러그 인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. <span data-ttu-id="c1d24-176">플러그 인 설치가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-176">The plugin installation starts.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. <span data-ttu-id="c1d24-178">설치가 완료되면</span><span class="sxs-lookup"><span data-stu-id="c1d24-178">Once the installation is complete.</span></span> <span data-ttu-id="c1d24-179">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-179">Click **Close**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. <span data-ttu-id="c1d24-181">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-181">Click **Manage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. <span data-ttu-id="c1d24-183">**구성**을 클릭하여 새 플러그 인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-183">Click **Configure** to configure the new plugin.</span></span>    

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. <span data-ttu-id="c1d24-185">**SAML** 섹션의</span><span class="sxs-lookup"><span data-stu-id="c1d24-185">In the **SAML** section.</span></span> <span data-ttu-id="c1d24-186">**ID 공급자 추가** 드롭다운에서 **Azure AD(Azure Active Directory)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-186">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. <span data-ttu-id="c1d24-188">구독 수준을 **기본**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-188">Select subscription level as **Basic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. <span data-ttu-id="c1d24-190">**앱 속성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-190">On the **App properties** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    <span data-ttu-id="c1d24-192">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-192">a.</span></span> <span data-ttu-id="c1d24-193">**앱 ID URI**을 복사하여 Azure Portal의 **Kantega SSO for Bitbucket 도메인 및 URL** 섹션에서 **식별자, 회신 URL 및 로그온 URL**로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-193">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="c1d24-194">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-194">b.</span></span> <span data-ttu-id="c1d24-195">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-195">Click **Next**.</span></span>

17. <span data-ttu-id="c1d24-196">**Metadata import**(메타데이터 가져오기) 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-196">On the **Metadata import** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    <span data-ttu-id="c1d24-198">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-198">a.</span></span> <span data-ttu-id="c1d24-199">**Metadata file on my computer**(내 컴퓨터의 메타데이터 파일)를 클릭하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="c1d24-200">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-200">b.</span></span> <span data-ttu-id="c1d24-201">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-201">Click **Next**.</span></span>

18. <span data-ttu-id="c1d24-202">**Name and SSO location**(이름 및 SSO 위치) 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-202">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    <span data-ttu-id="c1d24-204">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-204">a.</span></span> <span data-ttu-id="c1d24-205">**ID 공급자 이름** 텍스트 상자에 ID 공급자의 이름(예: Azure AD)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-205">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="c1d24-206">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-206">b.</span></span> <span data-ttu-id="c1d24-207">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-207">Click **Next**.</span></span>

19. <span data-ttu-id="c1d24-208">서명 인증서를 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-208">Verify the Signing certificate and click **Next**.</span></span>  

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. <span data-ttu-id="c1d24-210">**Bitbucket 사용자 계정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-210">On the **Bitbucket user accounts** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    <span data-ttu-id="c1d24-212">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-212">a.</span></span> <span data-ttu-id="c1d24-213">선택 **필요한 경우 Bitbucket의 내부 디렉터리에서 사용자를 만들려면** 사용자에 대 한 그룹의 적절 한 이름을 입력 하 고 (수 여러 아니요.</span><span class="sxs-lookup"><span data-stu-id="c1d24-213">Select **Create users in Bitbucket's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="c1d24-214">그룹의 쉼표로 구분).</span><span class="sxs-lookup"><span data-stu-id="c1d24-214">of groups separated by comma).</span></span>

    <span data-ttu-id="c1d24-215">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-215">b.</span></span> <span data-ttu-id="c1d24-216">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-216">Click **Next**.</span></span>

21. <span data-ttu-id="c1d24-217">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-217">Click **Finish**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. <span data-ttu-id="c1d24-219">**Known domains for Azure AD**(Azure AD에 알려진 도메인) 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-219">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    <span data-ttu-id="c1d24-221">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-221">a.</span></span> <span data-ttu-id="c1d24-222">페이지의 왼쪽 창에서 **Known domains**(알려진 도메인)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-222">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="c1d24-223">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-223">b.</span></span> <span data-ttu-id="c1d24-224">**Known domains**(알려진 도메인) 텍스트 상자에 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-224">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="c1d24-225">c.</span><span class="sxs-lookup"><span data-stu-id="c1d24-225">c.</span></span> <span data-ttu-id="c1d24-226">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-226">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="c1d24-227">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-227">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1d24-228">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-228">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1d24-229">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-229">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1d24-230">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c1d24-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1d24-231">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-231">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c1d24-233">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c1d24-233">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1d24-234">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-234">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1d24-236">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-236">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1d24-238">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-238">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1d24-240">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-240">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1d24-242">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-242">a.</span></span> <span data-ttu-id="c1d24-243">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-243">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1d24-244">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-244">b.</span></span> <span data-ttu-id="c1d24-245">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-245">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1d24-246">c.</span><span class="sxs-lookup"><span data-stu-id="c1d24-246">c.</span></span> <span data-ttu-id="c1d24-247">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-247">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c1d24-248">d.</span><span class="sxs-lookup"><span data-stu-id="c1d24-248">d.</span></span> <span data-ttu-id="c1d24-249">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-249">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a><span data-ttu-id="c1d24-250">Kantega SSO for Bitbucket 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c1d24-250">Creating a Kantega SSO for Bitbucket test user</span></span>

<span data-ttu-id="c1d24-251">Azure AD 사용자가 Bitbucket에 로그인할 수 있도록 하려면 Bitbucket으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-251">To enable Azure AD users to log in to Bitbucket, they must be provisioned into Bitbucket.</span></span> <span data-ttu-id="c1d24-252">Kantega SSO for Bitbucket에서는 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span></span>

<span data-ttu-id="c1d24-253">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1d24-253">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c1d24-254">Bitbucket 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-254">Log in to your Bitbucket company site as an administrator.</span></span>

2. <span data-ttu-id="c1d24-255">설정 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-255">Click on settings icon.</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. <span data-ttu-id="c1d24-257">**관리** 탭 섹션에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-257">Under **Administration** tab section, click **Users**.</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. <span data-ttu-id="c1d24-259">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-259">Click **Create user**.</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. <span data-ttu-id="c1d24-261">**사용자 만들기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-261">On the **Create User** dialog page, perform the following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    <span data-ttu-id="c1d24-263">a.</span><span class="sxs-lookup"><span data-stu-id="c1d24-263">a.</span></span> <span data-ttu-id="c1d24-264">**사용자 이름** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="c1d24-265">b.</span><span class="sxs-lookup"><span data-stu-id="c1d24-265">b.</span></span> <span data-ttu-id="c1d24-266">**전체 이름** 텍스트 상자에서 Britta Simon과 같은 사용자의 전체 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="c1d24-267">c.</span><span class="sxs-lookup"><span data-stu-id="c1d24-267">c.</span></span> <span data-ttu-id="c1d24-268">**이메일 주소** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="c1d24-269">d.</span><span class="sxs-lookup"><span data-stu-id="c1d24-269">d.</span></span> <span data-ttu-id="c1d24-270">**암호** 텍스트 상자에서 사용자에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="c1d24-271">e.</span><span class="sxs-lookup"><span data-stu-id="c1d24-271">e.</span></span> <span data-ttu-id="c1d24-272">**암호 확인** 텍스트 상자에 사용자의 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="c1d24-273">f.</span><span class="sxs-lookup"><span data-stu-id="c1d24-273">f.</span></span> <span data-ttu-id="c1d24-274">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-274">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c1d24-275">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c1d24-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c1d24-276">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Kantega SSO for Bitbucket에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bitbucket.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c1d24-278">**Britta Simon을 Kantega SSO for Bitbucket에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c1d24-278">**To assign Britta Simon to Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="c1d24-279">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c1d24-281">응용 프로그램 목록에서 **Kantega SSO for Bitbucket**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-281">In the applications list, select **Kantega SSO for Bitbucket**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. <span data-ttu-id="c1d24-283">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-283">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c1d24-285">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-285">Click **Add** button.</span></span> <span data-ttu-id="c1d24-286">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c1d24-288">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1d24-289">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1d24-290">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1d24-291">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c1d24-291">Testing single sign-on</span></span>

<span data-ttu-id="c1d24-292">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c1d24-293">액세스 패널에서 Kantega SSO for Bitbucket 타일을 클릭하면 Kantega SSO for Bitbucket 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d24-293">When you click the Kantega SSO for Bitbucket tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bitbucket application.</span></span>
<span data-ttu-id="c1d24-294">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1d24-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c1d24-295">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c1d24-295">Additional resources</span></span>

* [<span data-ttu-id="c1d24-296">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c1d24-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1d24-297">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c1d24-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

