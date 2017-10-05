---
title: "자습서: Azure Active Directory와 MOVEit Transfer - Azure AD 통합 통합 | Microsoft Docs"
description: "Azure Active Directory와 MOVEit Transfer - Azure AD 통합 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="f7305-103">자습서: Azure Active Directory와 MOVEit Transfer - Azure AD 통합 통합</span><span class="sxs-lookup"><span data-stu-id="f7305-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="f7305-104">이 자습서에서는 Azure AD(Azure Active Directory)와 MOVEit Transfer - Azure AD 통합을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7305-105">MOVEit Transfer - Azure AD 통합을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7305-106">MOVEit Transfer - Azure AD 통합에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="f7305-107">사용자가 해당 Azure AD 계정으로 MOVEit Transfer - Azure AD 통합에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f7305-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f7305-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7305-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7305-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7305-110">Prerequisites</span></span>

<span data-ttu-id="f7305-111">MOVEit Transfer - Azure AD 통합과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="f7305-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f7305-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7305-113">MOVEit Transfer - Azure AD 통합 Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f7305-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7305-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7305-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7305-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f7305-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7305-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7305-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f7305-118">Scenario description</span></span>
<span data-ttu-id="f7305-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7305-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7305-121">갤러리에서 MOVEit Transfer - Azure AD 통합 추가</span><span class="sxs-lookup"><span data-stu-id="f7305-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="f7305-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7305-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="f7305-123">갤러리에서 MOVEit Transfer - Azure AD 통합 추가</span><span class="sxs-lookup"><span data-stu-id="f7305-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="f7305-124">MOVEit Transfer - Azure AD 통합의 Azure AD 통합을 구성하려면 갤러리의 MOVEit Transfer - Azure AD 통합을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7305-125">**갤러리에서 MOVEit Transfer - Azure AD 통합을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7305-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7305-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="f7305-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7305-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="f7305-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="f7305-133">검색 상자에 **MOVEit Transfer - Azure AD 통합**을 입력하고 결과 패널에서 **MOVEit Transfer - Azure AD 통합**을 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 MOVEit Transfer - Azure AD 통합](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f7305-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7305-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f7305-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 MOVEit Transfer - Azure AD 통합에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7305-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 MOVEit Transfer - Azure AD 통합 사용자가 누군지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="f7305-138">즉, Azure AD 사용자와 MOVEit Transfer - Azure AD 통합의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="f7305-139">MOVEit Transfer - Azure AD 통합에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7305-140">MOVEit Transfer - Azure AD 통합에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7305-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7305-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7305-143">**[MOVEit Transfer - Azure AD 통합 테스트 사용자 만들기](#create-a-moveit-transfer---azure-ad-integration-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 MOVEit Transfer - Azure AD 통합에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7305-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7305-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f7305-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f7305-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f7305-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 MOVEit Transfer - Azure AD 통합 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="f7305-148">**MOVEit Transfer - Azure AD 통합에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7305-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="f7305-149">Azure Portal의 **MOVEit Transfer - Azure AD 통합** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="f7305-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="f7305-153">**MOVEit Transfer - Azure AD 통합 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="f7305-155">a.</span><span class="sxs-lookup"><span data-stu-id="f7305-155">a.</span></span> <span data-ttu-id="f7305-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="f7305-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="f7305-157">b.</span><span class="sxs-lookup"><span data-stu-id="f7305-157">b.</span></span> <span data-ttu-id="f7305-158">**식별자** 텍스트 상자에서 `https://contoso.com/<tenatid>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="f7305-159">c.</span><span class="sxs-lookup"><span data-stu-id="f7305-159">c.</span></span> <span data-ttu-id="f7305-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="f7305-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="f7305-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-161">These values are not real.</span></span> <span data-ttu-id="f7305-162">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f7305-163">**서비스 공급자 메타데이터 URL** 섹션에서 이러한 값을 나중에 참조하거나 해당 값을 얻기 위해 [MOVEit Transfer - Azure AD 통합 클라이언트 지원 팀](https://community.ipswitch.com/s/support)에 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="f7305-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="f7305-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-166">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f7305-168">MOVEit Transfer 테넌트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="f7305-169">왼쪽 탐색 창에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-169">On the left navigation pane, click **Settings**.</span></span>

    ![앱 쪽의 설정 섹션](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="f7305-171">**보안 정책 -> 사용자 인증** 아래의 **Single Sign On** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![앱 쪽의 보안 정책](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="f7305-173">메타데이터 URL 링크를 클릭하여 메타데이터 문서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![서비스 공급자 메타데이터 URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="f7305-175">**엔터티 ID**가 **MOVEit Transfer - Azure AD 통합 도메인 및 URL** 섹션의 **식별자**와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="f7305-176">**AssertionConsumerService** 위치 URL이 **MOVEit Transfer - Azure AD 통합 도메인 및 URL** 섹션의 **회신 URL**과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="f7305-178">**ID 공급자 추가** 단추를 클릭하여 새 페더레이션 ID 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![ID 공급자 추가](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="f7305-180">**찾아보기...**를 클릭하여 Azure Portal에서 다운로드한 메타데이터 파일을 선택한 다음 **ID 공급자 추가**를 클릭하여 다운로드한 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![SAML ID 공급자](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="f7305-182">**페더레이션 ID 공급자 설정 편집...** 페이지에서 **활성화**로 "**예**"를 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![페더레이션 ID 공급자 설정](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="f7305-184">**페더레이션 ID 공급자 사용자 설정 편집** 페이지에서 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![페더레이션 ID 공급자 설정 편집](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="f7305-186">a.</span><span class="sxs-lookup"><span data-stu-id="f7305-186">a.</span></span> <span data-ttu-id="f7305-187">**로그인 이름**으로 **SAML NameID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="f7305-188">b.</span><span class="sxs-lookup"><span data-stu-id="f7305-188">b.</span></span> <span data-ttu-id="f7305-189">**전체 이름**으로 **기타**를 선택하고 **특성 이름** 텍스트 상자에 `http://schemas.microsoft.com/identity/claims/displayname` 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="f7305-190">c.</span><span class="sxs-lookup"><span data-stu-id="f7305-190">c.</span></span> <span data-ttu-id="f7305-191">**전자 메일**로 **기타**를 선택하고 **특성 이름** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f7305-192">d.</span><span class="sxs-lookup"><span data-stu-id="f7305-192">d.</span></span> <span data-ttu-id="f7305-193">**SignOn에서 계정 자동 만들기**로 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="f7305-194">e.</span><span class="sxs-lookup"><span data-stu-id="f7305-194">e.</span></span> <span data-ttu-id="f7305-195">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="f7305-196">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7305-197">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7305-198">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f7305-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f7305-199">Create an Azure AD test user</span></span>

<span data-ttu-id="f7305-200">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="f7305-202">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="f7305-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7305-203">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f7305-205">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f7305-207">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f7305-209">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-209">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f7305-211">a.</span><span class="sxs-lookup"><span data-stu-id="f7305-211">a.</span></span> <span data-ttu-id="f7305-212">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7305-213">b.</span><span class="sxs-lookup"><span data-stu-id="f7305-213">b.</span></span> <span data-ttu-id="f7305-214">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f7305-215">c.</span><span class="sxs-lookup"><span data-stu-id="f7305-215">c.</span></span> <span data-ttu-id="f7305-216">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f7305-217">d.</span><span class="sxs-lookup"><span data-stu-id="f7305-217">d.</span></span> <span data-ttu-id="f7305-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="f7305-219">MOVEit Transfer - Azure AD 통합 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f7305-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="f7305-220">이 섹션은 MOVEit Transfer - Azure AD 통합에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="f7305-221">MOVEit Transfer - Azure AD 통합은 적시에 프로비전을 지원하며 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="f7305-222">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-222">There is no action item for you in this section.</span></span> <span data-ttu-id="f7305-223">새 사용자가 아직 존재하지 않는 경우 MOVEit Transfer - Azure AD 통합에 액세스하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f7305-224">사용자를 수동으로 만들어야 하는 경우 [MOVEit Transfer - Azure AD 통합 클라이언트 지원 팀](https://community.ipswitch.com/s/support)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f7305-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="f7305-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="f7305-226">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 MOVEit Transfer - Azure AD 통합에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="f7305-228">**Britta Simon을 MOVEit Transfer - Azure AD 통합에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="f7305-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="f7305-229">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f7305-231">응용 프로그램 목록에서 **MOVEit Transfer - Azure AD 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![응용 프로그램 목록의 MOVEit Transfer - Azure AD 통합 링크](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="f7305-233">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-233">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="f7305-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-235">Click **Add** button.</span></span> <span data-ttu-id="f7305-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="f7305-238">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7305-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7305-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f7305-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f7305-241">Test single sign-on</span></span>

<span data-ttu-id="f7305-242">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f7305-243">액세스 패널에서 MOVEit Transfer - Azure AD 통합 타일을 클릭하면 MOVEit Transfer - Azure AD 통합 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7305-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f7305-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f7305-244">Additional resources</span></span>

* [<span data-ttu-id="f7305-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="f7305-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7305-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f7305-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

