---
title: "자습서: Absorb LMS와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory 및 Absorb LMS 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="c25d5-103">자습서: Absorb LMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c25d5-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="c25d5-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Absorb LMS를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c25d5-105">Absorb LMS를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c25d5-106">Azure AD에서는 Absorb LMS에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="c25d5-107">사용자가 해당 Azure AD 계정으로 Absorb LMS에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c25d5-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c25d5-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="c25d5-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="c25d5-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c25d5-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c25d5-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c25d5-111">Prerequisites</span></span>

<span data-ttu-id="c25d5-112">Absorb LMS와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="c25d5-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c25d5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c25d5-114">Absorb LMS Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c25d5-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c25d5-115">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c25d5-116">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c25d5-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c25d5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c25d5-118">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c25d5-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c25d5-119">Scenario description</span></span>
<span data-ttu-id="c25d5-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c25d5-121">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c25d5-122">갤러리에서 Absorb LMS 추가</span><span class="sxs-lookup"><span data-stu-id="c25d5-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="c25d5-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c25d5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="c25d5-124">갤러리에서 Absorb LMS 추가</span><span class="sxs-lookup"><span data-stu-id="c25d5-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="c25d5-125">Absorb LMS의 Azure AD 통합을 구성하려면 갤러리의 Absorb LMS를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c25d5-126">**갤러리에서 Absorb LMS를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c25d5-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c25d5-127">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="c25d5-129">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c25d5-130">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-130">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="c25d5-132">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="c25d5-134">검색 상자에 **Absorb LMS**를 입력하고 결과 패널에서 **Absorb LMS**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c25d5-136">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c25d5-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c25d5-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Absorb LMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c25d5-138">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Absorb LMS 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="c25d5-139">즉, Azure AD 사용자와 Absorb LMS의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="c25d5-140">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Absorb LMS의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="c25d5-141">Absorb LMS에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c25d5-142">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c25d5-143">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c25d5-144">**[Absorb LMS 테스트 사용자 만들기](#create-an-absorb-lms-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Absorb LMS에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c25d5-145">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c25d5-146">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c25d5-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c25d5-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c25d5-148">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Absorb LMS 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="c25d5-149">**Absorb LMS에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c25d5-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c25d5-150">Azure Portal의 **Absorb LMS** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="c25d5-152">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="c25d5-154">**Absorb LMS 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Absorb LMS 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="c25d5-156">a.</span><span class="sxs-lookup"><span data-stu-id="c25d5-156">a.</span></span> <span data-ttu-id="c25d5-157">**식별자** 텍스트 상자에서 `https://<subdomain>.myabsorb.com/Account/SAML` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="c25d5-158">b.</span><span class="sxs-lookup"><span data-stu-id="c25d5-158">b.</span></span> <span data-ttu-id="c25d5-159">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="c25d5-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c25d5-160">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-160">These values are not the real.</span></span> <span data-ttu-id="c25d5-161">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c25d5-162">이러한 값을 얻으려면 [Absorb LMS 클라이언트 지원 팀](https://www.absorblms.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c25d5-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="c25d5-163">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="c25d5-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-165">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c25d5-167">**Absorb LMS 구성** 섹션에서 **Absorb LMS 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c25d5-168">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Absorb LMS 구성](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="c25d5-170">다른 웹 브라우저 창에서 Absorb LMS 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="c25d5-171">관리자 인터페이스에서 **계정 아이콘**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Single Sign-On 구성](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="c25d5-173">**포털 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-173">Click **Portal Settings**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="c25d5-175">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-175">Click the **Users** tab.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="c25d5-177">Single Sign-On 구성 필드에 액세스하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="c25d5-179">a.</span><span class="sxs-lookup"><span data-stu-id="c25d5-179">a.</span></span> <span data-ttu-id="c25d5-180">적절한 **모드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="c25d5-181">b.</span><span class="sxs-lookup"><span data-stu-id="c25d5-181">b.</span></span> <span data-ttu-id="c25d5-182">Azure Portal에서 다운로드한 인증서를 메모장에서 열고 **---BEGIN CERTIFICATE---** 및 **---END CERTIFICATE---** 태그를 제거하고 나머지 내용을 **Key** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="c25d5-183">c.</span><span class="sxs-lookup"><span data-stu-id="c25d5-183">c.</span></span> <span data-ttu-id="c25d5-184">**ID 속성**에서, Azure AD에서 사용자 식별자로 구성한 해당 특성을 선택합니다. 예를 들어 Azure AD에서 userprinciplename을 선택한 경우 여기서도 Username을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="c25d5-185">d.</span><span class="sxs-lookup"><span data-stu-id="c25d5-185">d.</span></span> <span data-ttu-id="c25d5-186">**로그인 URL**에서, Azure Portal의 **로그온 구성** 창에서 복사한 **“SAML Single Sign-On 서비스 URL”** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="c25d5-187">e.</span><span class="sxs-lookup"><span data-stu-id="c25d5-187">e.</span></span> <span data-ttu-id="c25d5-188">**로그아웃 URL**에서, Azure Portal의 **로그온 구성** 창에서 복사한 **“로그아웃 URL”** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="c25d5-189">**‘Only Allow SSO Login’**(SSO 로그인만 허용)을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="c25d5-191">**"저장"**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="c25d5-192">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c25d5-193">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c25d5-194">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c25d5-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c25d5-195">Create an Azure AD test user</span></span>

<span data-ttu-id="c25d5-196">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="c25d5-198">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c25d5-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c25d5-199">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c25d5-201">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c25d5-203">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c25d5-205">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c25d5-207">a.</span><span class="sxs-lookup"><span data-stu-id="c25d5-207">a.</span></span> <span data-ttu-id="c25d5-208">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c25d5-209">b.</span><span class="sxs-lookup"><span data-stu-id="c25d5-209">b.</span></span> <span data-ttu-id="c25d5-210">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c25d5-211">c.</span><span class="sxs-lookup"><span data-stu-id="c25d5-211">c.</span></span> <span data-ttu-id="c25d5-212">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c25d5-213">d.</span><span class="sxs-lookup"><span data-stu-id="c25d5-213">d.</span></span> <span data-ttu-id="c25d5-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="c25d5-215">Absorb LMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c25d5-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="c25d5-216">Azure AD 사용자가 Absorb LMS에 로그인할 수 있도록 하려면 Absorb LMS로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="c25d5-217">Absorb LMS의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="c25d5-218">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c25d5-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c25d5-219">Absorb LMS 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="c25d5-220">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-220">Click **Users** tab.</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="c25d5-222">**사용자** 탭에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-222">Click **Users** under the **Users** tab.</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="c25d5-224">**새로 추가** 드롭다운에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-224">Select **User** from **Add New** drop-down.</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="c25d5-226">**사용자 추가** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-226">On the **Add User** page, perform the following steps:</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="c25d5-228">a.</span><span class="sxs-lookup"><span data-stu-id="c25d5-228">a.</span></span> <span data-ttu-id="c25d5-229">**이름** 텍스트 상자에 이름(예: Britta)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="c25d5-230">b.</span><span class="sxs-lookup"><span data-stu-id="c25d5-230">b.</span></span> <span data-ttu-id="c25d5-231">**성** 텍스트 상자에 성(예: Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="c25d5-232">c.</span><span class="sxs-lookup"><span data-stu-id="c25d5-232">c.</span></span> <span data-ttu-id="c25d5-233">**사용자 이름** 텍스트 상자에 사용자 이름(예: Britta Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="c25d5-234">d.</span><span class="sxs-lookup"><span data-stu-id="c25d5-234">d.</span></span> <span data-ttu-id="c25d5-235">**암호** 텍스트 상자에 Britta Simon의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="c25d5-236">e.</span><span class="sxs-lookup"><span data-stu-id="c25d5-236">e.</span></span> <span data-ttu-id="c25d5-237">**암호 확인** 텍스트 상자에 동일한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="c25d5-238">f.</span><span class="sxs-lookup"><span data-stu-id="c25d5-238">f.</span></span> <span data-ttu-id="c25d5-239">**활성**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="c25d5-240">**"저장"**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c25d5-241">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c25d5-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="c25d5-242">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Absorb LMS에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![사용자 역할 할당][200]

<span data-ttu-id="c25d5-244">**Britta Simon을 Absorb LMS에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c25d5-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="c25d5-245">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c25d5-247">응용 프로그램 목록에서 **Absorb LMS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-247">In the applications list, select **Absorb LMS**.</span></span>

    ![응용 프로그램 목록의 Absorb LMS 링크](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="c25d5-249">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-249">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="c25d5-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-251">Click **Add** button.</span></span> <span data-ttu-id="c25d5-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="c25d5-254">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c25d5-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c25d5-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c25d5-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c25d5-257">Test single sign-on</span></span>

<span data-ttu-id="c25d5-258">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c25d5-259">액세스 패널에서 Absorb LMS 타일을 클릭하면 Absorb LMS 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="c25d5-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="c25d5-260">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c25d5-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c25d5-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c25d5-261">Additional resources</span></span>

* [<span data-ttu-id="c25d5-262">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c25d5-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c25d5-263">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c25d5-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

