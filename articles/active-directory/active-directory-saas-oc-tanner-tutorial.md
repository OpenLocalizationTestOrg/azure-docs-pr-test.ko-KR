---
title: "자습서: O.C. Tanner - AppreciateHub와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 O.C. Tanner - AppreciateHub 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="a00a2-105">자습서: O.C. Tanner - AppreciateHub와</span><span class="sxs-lookup"><span data-stu-id="a00a2-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="a00a2-106">Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a00a2-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="a00a2-107">이 자습서에서는 O.C. Tanner - AppreciateHub와 Azure AD(Azure Active Directory)를</span><span class="sxs-lookup"><span data-stu-id="a00a2-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="a00a2-108">통합하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a00a2-109">O.C. 통합</span><span class="sxs-lookup"><span data-stu-id="a00a2-109">Integrating O.C.</span></span> <span data-ttu-id="a00a2-110">Tanner - Azure AD가 포함된 AppreciateHub는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a00a2-111">O.C.에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="a00a2-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a00a2-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="a00a2-113">사용자가 자동으로 O.C.에 로그온하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="a00a2-114">Tanner - Azure AD 계정이 포함된 AppreciateHub(Single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="a00a2-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a00a2-115">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a00a2-116">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a00a2-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a00a2-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a00a2-117">Prerequisites</span></span>

<span data-ttu-id="a00a2-118">O.C.와 Azure AD 통합을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="a00a2-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="a00a2-119">Tanner - AppreciateHub, 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="a00a2-120">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a00a2-120">An Azure AD subscription</span></span>
- <span data-ttu-id="a00a2-121">O.C.</span><span class="sxs-lookup"><span data-stu-id="a00a2-121">A O.C.</span></span> <span data-ttu-id="a00a2-122">Tanner - AppreciateHub Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a00a2-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a00a2-123">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a00a2-124">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a00a2-125">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a00a2-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a00a2-126">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a00a2-127">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a00a2-127">Scenario description</span></span>
<span data-ttu-id="a00a2-128">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a00a2-129">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a00a2-130">O.C. 추가</span><span class="sxs-lookup"><span data-stu-id="a00a2-130">Adding O.C.</span></span> <span data-ttu-id="a00a2-131">Tanner - 갤러리에서 AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a00a2-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="a00a2-132">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a00a2-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="a00a2-133">O.C. 추가</span><span class="sxs-lookup"><span data-stu-id="a00a2-133">Adding O.C.</span></span> <span data-ttu-id="a00a2-134">Tanner - 갤러리에서 AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a00a2-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="a00a2-135">O.C.의 통합을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="a00a2-135">To configure the integration of O.C.</span></span> <span data-ttu-id="a00a2-136">Tanner - Azure AD에서 AppreciateHub, O.C.를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="a00a2-137">Tanner - 갤러리에서 관리된 SaaS 앱 목록에 AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a00a2-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a00a2-138">**O.C.를 추가하려면 Tanner - 갤러리에서 AppreciateHub, 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a00a2-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a00a2-139">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a00a2-141">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a00a2-142">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-142">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a00a2-144">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a00a2-146">검색 상자에 **O.C.를 입력합니다. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="a00a2-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="a00a2-148">결과 패널에서 **O.C. Tanner - AppreciateHub**를 선택한 다음 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a00a2-150">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a00a2-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a00a2-151">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 한 O.C.</span><span class="sxs-lookup"><span data-stu-id="a00a2-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="a00a2-152">Tanner - AppreciateHub를 사용하여 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a00a2-153">Single Sign-On이 작동하려면 Azure AD는 O.C. Tanner - AppreciateHub에서 해당 사용자가</span><span class="sxs-lookup"><span data-stu-id="a00a2-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="a00a2-154">Azure AD에서의 사용자라는 것을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="a00a2-155">즉, Azure AD 사용자와 O.C.의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="a00a2-156">Tanner - AppreciateHub를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="a00a2-157">O.C.</span><span class="sxs-lookup"><span data-stu-id="a00a2-157">In O.C.</span></span> <span data-ttu-id="a00a2-158">Tanner - AppreciateHub에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a00a2-159">O.C.를 사용하여 Azure AD Single Sign-On을 구성하고 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="a00a2-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="a00a2-160">Tanner - AppreciateHub, 다음과 같은 구성 블록을 완료하는데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a00a2-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a00a2-162">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-on 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a00a2-163">**[O.C. 만들기 Tanner - O.C.에서 Britta Simon에 해당하는 사용자가 있는 AppreciateHub 테스트 사용자](#creating-a-oc-tanner---appreciatehub-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="a00a2-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="a00a2-164">해당 사용자의 Azure AD 표현에 연결된 Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a00a2-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a00a2-165">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a00a2-166">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a00a2-167">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a00a2-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a00a2-168">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 O.C. Tanner - AppreciateHub 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="a00a2-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="a00a2-169">Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="a00a2-170">**O.C.를 사용하여 Azure AD Single Sign-On을 구성하려면 Tanner - AppreciateHub, 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a00a2-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="a00a2-171">Azure Portal의 **O.C. Tanner - AppreciateHub** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a00a2-173">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="a00a2-175">**O.C. Tanner - AppreciateHub 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="a00a2-177">a.</span><span class="sxs-lookup"><span data-stu-id="a00a2-177">a.</span></span> <span data-ttu-id="a00a2-178">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="a00a2-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a00a2-179">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-179">This value is not real.</span></span> <span data-ttu-id="a00a2-180">실제 회신 URL로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="a00a2-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="a00a2-181">이 값을 얻으려면 [O.C. Tanner - AppreciateHub 지원 팀](mailto:sso@octanner.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a00a2-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="a00a2-182">b.</span><span class="sxs-lookup"><span data-stu-id="a00a2-182">b.</span></span> <span data-ttu-id="a00a2-183">[https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata) 링크를 사용하여 메타데이터 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="a00a2-184">c.</span><span class="sxs-lookup"><span data-stu-id="a00a2-184">c.</span></span> <span data-ttu-id="a00a2-185">**md:AssertionConsumerService** 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="a00a2-186">d.</span><span class="sxs-lookup"><span data-stu-id="a00a2-186">d.</span></span> <span data-ttu-id="a00a2-187">**위치** 특성의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![앱 설정 구성][12]
   
    <span data-ttu-id="a00a2-189">e.</span><span class="sxs-lookup"><span data-stu-id="a00a2-189">e.</span></span> <span data-ttu-id="a00a2-190">**Sign-on URL** 텍스트 상자에서 이전 단계에 얻은 값보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="a00a2-191">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="a00a2-193">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-193">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a00a2-195">**O.C. Tanner - AppreciateHub** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [O.C. Tanner - AppreciateHub 지원 팀](mailto:sso@octanner.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="a00a2-196">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a00a2-197">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a00a2-198">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a00a2-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a00a2-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="a00a2-200">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a00a2-202">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a00a2-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a00a2-203">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a00a2-205">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a00a2-207">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a00a2-209">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a00a2-211">a.</span><span class="sxs-lookup"><span data-stu-id="a00a2-211">a.</span></span> <span data-ttu-id="a00a2-212">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a00a2-213">b.</span><span class="sxs-lookup"><span data-stu-id="a00a2-213">b.</span></span> <span data-ttu-id="a00a2-214">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a00a2-215">c.</span><span class="sxs-lookup"><span data-stu-id="a00a2-215">c.</span></span> <span data-ttu-id="a00a2-216">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a00a2-217">d.</span><span class="sxs-lookup"><span data-stu-id="a00a2-217">d.</span></span> <span data-ttu-id="a00a2-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="a00a2-219">O.C. 만들기</span><span class="sxs-lookup"><span data-stu-id="a00a2-219">Creating a O.C.</span></span> <span data-ttu-id="a00a2-220">Tanner - AppreciateHub 테스트 사용자.</span><span class="sxs-lookup"><span data-stu-id="a00a2-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="a00a2-221">이 섹션은 O.C.에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="a00a2-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a00a2-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="a00a2-223">**O.C.에서 Britta Simon이라는 사용자를 만들려면 Tanner - AppreciateHub, 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a00a2-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="a00a2-224">[O.C. Tanner - AppreciateHub 지원 팀](mailto:sso@octanner.com)에 요청하여 Azure AD에서 Britta Simon이라는 사용자 이름이 동일한 값인 nameID 특성을 가진 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a00a2-225">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a00a2-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a00a2-226">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 O.C. Tanner - AppreciateHub에 대한</span><span class="sxs-lookup"><span data-stu-id="a00a2-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="a00a2-227">액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-227">Tanner - AppreciateHub.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a00a2-229">**Britta Simon를 O.C.에 할당하려면 Tanner - AppreciateHub, 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a00a2-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="a00a2-230">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a00a2-232">응용 프로그램 목록에서 **O.C.를 선택합니다. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="a00a2-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="a00a2-234">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-234">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a00a2-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-236">Click **Add** button.</span></span> <span data-ttu-id="a00a2-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a00a2-239">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a00a2-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a00a2-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a00a2-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a00a2-242">Testing single sign-on</span></span>

<span data-ttu-id="a00a2-243">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="a00a2-244">O.C.를 클릭할 때</span><span class="sxs-lookup"><span data-stu-id="a00a2-244">When you click the O.C.</span></span> <span data-ttu-id="a00a2-245">Tanner - 액세스 패널에서 AppreciateHub 타일, O.C.에 자동으로 로그온되야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a2-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="a00a2-246">Tanner - AppreciateHub 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="a00a2-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a00a2-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a00a2-247">Additional resources</span></span>

* [<span data-ttu-id="a00a2-248">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a00a2-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a00a2-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a00a2-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

