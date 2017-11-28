---
title: "자습서: StatusPage와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 StatusPage 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="94137-103">자습서: StatusPage와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="94137-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="94137-104">이 자습서에서는 Azure AD(Azure Active Directory)와 StatusPage를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94137-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94137-105">StatusPage를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="94137-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94137-106">StatusPage에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="94137-107">사용자가 해당 Azure AD 계정으로 StatusPage에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94137-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="94137-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94137-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94137-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="94137-110">Prerequisites</span></span>

<span data-ttu-id="94137-111">StatusPage와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="94137-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="94137-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94137-113">StatusPage One Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="94137-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94137-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94137-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94137-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="94137-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94137-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94137-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="94137-118">Scenario description</span></span>
<span data-ttu-id="94137-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94137-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94137-121">갤러리에서 StatusPage 추가</span><span class="sxs-lookup"><span data-stu-id="94137-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="94137-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="94137-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="94137-123">갤러리에서 StatusPage 추가</span><span class="sxs-lookup"><span data-stu-id="94137-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="94137-124">StatusPage의 Azure AD 통합을 구성하려면 갤러리의 StatusPage를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94137-125">**갤러리에서 StatusPage를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94137-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94137-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94137-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94137-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="94137-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="94137-133">검색 상자에 **StatusPage**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-133">In the search box, type **StatusPage**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="94137-135">결과 창에서 **StatusPage**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94137-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="94137-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94137-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 StatusPage에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94137-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 StatusPage 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="94137-140">즉, Azure AD 사용자와 StatusPage의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="94137-141">StatusPage에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94137-142">StatusPage에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94137-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94137-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94137-145">**[StatusPage 테스트 사용자 만들기](#creating-a-statuspage-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 StatusPage에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94137-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94137-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94137-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94137-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="94137-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94137-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 StatusPage 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="94137-150">**StatusPage에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94137-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="94137-151">Azure Portal의 **StatusPage** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="94137-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="94137-155">**StatusPage 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="94137-157">a.</span><span class="sxs-lookup"><span data-stu-id="94137-157">a.</span></span> <span data-ttu-id="94137-158">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="94137-159">b.</span><span class="sxs-lookup"><span data-stu-id="94137-159">b.</span></span> <span data-ttu-id="94137-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="94137-161">[SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)에서 StatusPage 지원 팀에 문의하여 Single Sign-On을 구성하는 데 필요한 메타데이터를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="94137-162">a.</span><span class="sxs-lookup"><span data-stu-id="94137-162">a.</span></span> <span data-ttu-id="94137-163">메타데이터에서 발급자 값을 복사한 다음 **식별자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="94137-164">b.</span><span class="sxs-lookup"><span data-stu-id="94137-164">b.</span></span> <span data-ttu-id="94137-165">메타데이터에서 회신 URL을 복사한 다음 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="94137-166">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="94137-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94137-170">**StatusPage 구성** 섹션에서 **StatusPage 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="94137-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94137-171">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="94137-173">다른 웹 브라우저 창에서 StatusPage 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="94137-174">주 도구 모음에서 **계정 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="94137-176">**Single Sign-On** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Single Sign-On 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="94137-178">SSO 설정 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Single Sign-On 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="94137-181">a.</span><span class="sxs-lookup"><span data-stu-id="94137-181">a.</span></span> <span data-ttu-id="94137-182">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SSO 대상 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="94137-183">b.</span><span class="sxs-lookup"><span data-stu-id="94137-183">b.</span></span> <span data-ttu-id="94137-184">다운로드된 인증서를 메모장에서 열고, 내용을 복사한 다음 전체 인증서를 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="94137-185">c.</span><span class="sxs-lookup"><span data-stu-id="94137-185">c.</span></span> <span data-ttu-id="94137-186">**구성 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="94137-187">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94137-188">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94137-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94137-189">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94137-190">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="94137-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="94137-191">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94137-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="94137-193">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="94137-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94137-194">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94137-196">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94137-198">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94137-200">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94137-202">a.</span><span class="sxs-lookup"><span data-stu-id="94137-202">a.</span></span> <span data-ttu-id="94137-203">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94137-204">b.</span><span class="sxs-lookup"><span data-stu-id="94137-204">b.</span></span> <span data-ttu-id="94137-205">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94137-206">c.</span><span class="sxs-lookup"><span data-stu-id="94137-206">c.</span></span> <span data-ttu-id="94137-207">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="94137-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="94137-208">d.</span><span class="sxs-lookup"><span data-stu-id="94137-208">d.</span></span> <span data-ttu-id="94137-209">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="94137-210">StatusPage 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="94137-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="94137-211">이 섹션은 StatusPage에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94137-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="94137-212">StatusPage는 적시에 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="94137-213">이미 [Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)에서 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="94137-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="94137-214">**StatusPage에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94137-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="94137-215">StatusPage 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="94137-216">위쪽 메뉴에서 **계정 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="94137-218">**팀 멤버** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-218">Click the **Team Members** tab.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="94137-220">**팀 멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="94137-222">관련된 텍스트 상자에 프로비전할 유효한 사용자의 **메일 주소**, **이름** 및 **성**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="94137-224">**역할**로 **클라이언트 관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="94137-225">**계정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="94137-226">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="94137-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="94137-227">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 StatusPage에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![사용자 할당][200] 

<span data-ttu-id="94137-229">**Britta Simon을 StatusPage에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="94137-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="94137-230">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="94137-232">응용 프로그램 목록에서 **StatusPage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-232">In the applications list, select **StatusPage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="94137-234">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-234">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="94137-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-236">Click **Add** button.</span></span> <span data-ttu-id="94137-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="94137-239">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94137-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94137-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94137-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94137-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="94137-242">Testing single sign-on</span></span>

<span data-ttu-id="94137-243">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94137-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94137-244">액세스 패널에서 StatusPage 타일을 클릭하면 StatusPage 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="94137-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94137-245">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="94137-245">Additional resources</span></span>

* [<span data-ttu-id="94137-246">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="94137-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94137-247">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="94137-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

