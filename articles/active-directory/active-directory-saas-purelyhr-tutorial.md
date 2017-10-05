---
title: "자습서: PurelyHR과 Azure Active Directory 통합| Microsoft 문서"
description: "Azure Active Directory 및 PurelyHR 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="a8ec7-103">자습서: PurelyHR과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a8ec7-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="a8ec7-104">이 자습서에서는 Azure AD(Azure Active Directory)와 PurelyHR을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8ec7-105">PurelyHR을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8ec7-106">Azure AD에서는 PurelyHR에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="a8ec7-107">사용자가 Azure AD 계정으로 PurelyHR에 자동으로 로그인(Single Sign-On)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8ec7-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8ec7-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8ec7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a8ec7-110">Prerequisites</span></span>

<span data-ttu-id="a8ec7-111">PurelyHR과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="a8ec7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a8ec7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8ec7-113">PurelyHR Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a8ec7-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8ec7-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8ec7-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8ec7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8ec7-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8ec7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a8ec7-118">Scenario description</span></span>
<span data-ttu-id="a8ec7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8ec7-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8ec7-121">갤러리에서 PurelyHR 추가</span><span class="sxs-lookup"><span data-stu-id="a8ec7-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="a8ec7-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a8ec7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="a8ec7-123">갤러리에서 PurelyHR 추가</span><span class="sxs-lookup"><span data-stu-id="a8ec7-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="a8ec7-124">PurelyHR의 Azure AD 통합을 구성하려면 갤러리의 PurelyHR을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8ec7-125">**갤러리에서 PurelyHR을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a8ec7-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8ec7-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8ec7-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8ec7-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a8ec7-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a8ec7-133">검색 상자에 **PurelyHR**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-133">In the search box, type **PurelyHR**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="a8ec7-135">결과 패널에서 **PurelyHR**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8ec7-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a8ec7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8ec7-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 PurelyHR에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8ec7-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 PurelyHR 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="a8ec7-140">즉, Azure AD 사용자와 PurelyHR의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="a8ec7-141">PurelyHR에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a8ec7-142">PurelyHR에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8ec7-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8ec7-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8ec7-145">**[PurelyHR 테스트 사용자 만들기](#creating-a-purelyhr-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 PurelyHR에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8ec7-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8ec7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8ec7-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a8ec7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8ec7-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 PurelyHR 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="a8ec7-150">**PurelyHR에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a8ec7-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="a8ec7-151">Azure Portal의 **PurelyHR** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a8ec7-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="a8ec7-155">**PurelyHR 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="a8ec7-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="a8ec7-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="a8ec7-158">**SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="a8ec7-160">**로그온 URL** 텍스트 상자에 다음 패턴으로 값을 입력합니다. `https://<companyID>.purelyhr.com/sso-initiate` </span><span class="sxs-lookup"><span data-stu-id="a8ec7-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="a8ec7-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-161">These values are not the real.</span></span> <span data-ttu-id="a8ec7-162">실제 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="a8ec7-163">이러한 값을 얻으려면 [PurelyHR 클라이언트 지원 팀](http://support.purelyhr.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="a8ec7-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="a8ec7-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a8ec7-168">**PurelyHR 구성** 섹션에서 **PurelyHR 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a8ec7-169">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="a8ec7-171">**PurelyHR** 쪽에서 Single Sign-On을 구성하려면 관리자 권한으로 웹 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="a8ec7-172">도구 모음의 옵션에서 **대시보드**를 열고 **SSO 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="a8ec7-173">아래 설명에 따라 값을 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-173">Paste the values in the boxes as described below-</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="a8ec7-175">a.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-175">a.</span></span> <span data-ttu-id="a8ec7-176">Azure Portal에서 다운로드한 **인증서(Bas64)**를 메모장에서 열고 인증서 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="a8ec7-177">복사한 값을 **X.509 인증서** 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="a8ec7-178">b.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-178">b.</span></span> <span data-ttu-id="a8ec7-179">**IDP 발급자 URL** 상자에 Azure Portal에서 복사한 **SAML 엔터티 ID**를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="a8ec7-180">c.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-180">c.</span></span> <span data-ttu-id="a8ec7-181">**IDP 끝점 URL** 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="a8ec7-182">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-182">d.</span></span> <span data-ttu-id="a8ec7-183">**사용자 자동 생성** 확인란을 선택하여 PurelyHR에서 자동 사용자 프로비전을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="a8ec7-184">e.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-184">e.</span></span> <span data-ttu-id="a8ec7-185">**변경 내용 저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="a8ec7-186">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8ec7-187">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8ec7-188">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8ec7-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a8ec7-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8ec7-190">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a8ec7-192">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a8ec7-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8ec7-193">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8ec7-195">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8ec7-197">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8ec7-199">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8ec7-201">a.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-201">a.</span></span> <span data-ttu-id="a8ec7-202">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8ec7-203">b.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-203">b.</span></span> <span data-ttu-id="a8ec7-204">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8ec7-205">c.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-205">c.</span></span> <span data-ttu-id="a8ec7-206">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8ec7-207">d.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-207">d.</span></span> <span data-ttu-id="a8ec7-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="a8ec7-209">PurelyHR 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a8ec7-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="a8ec7-210">Azure AD 사용자가 PurelyHR에 로그인할 수 있도록 하려면 PurelyHR로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="a8ec7-211">PurelyHR에서 프로비전은 자동 작업이고 자동 사용자 프로비전이 사용되면 수동 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8ec7-212">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a8ec7-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8ec7-213">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 PurelyHR에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a8ec7-215">**Britta Simon을 PurelyHR에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a8ec7-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="a8ec7-216">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a8ec7-218">응용 프로그램 목록에서 **PurelyHR**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-218">In the applications list, select **PurelyHR**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="a8ec7-220">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-220">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a8ec7-222">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-222">Click **Add** button.</span></span> <span data-ttu-id="a8ec7-223">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a8ec7-225">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8ec7-226">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8ec7-227">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8ec7-228">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a8ec7-228">Testing single sign-on</span></span>

<span data-ttu-id="a8ec7-229">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a8ec7-230">액세스 패널에서 Absorb LMS 타일을 클릭하면 Absorb LMS 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="a8ec7-231">액세스 패널에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="a8ec7-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="a8ec7-232">[Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8ec7-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8ec7-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a8ec7-233">Additional resources</span></span>

* [<span data-ttu-id="a8ec7-234">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a8ec7-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8ec7-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a8ec7-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

