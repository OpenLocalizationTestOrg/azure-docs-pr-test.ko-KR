---
title: "자습서: Azure에서 Google Apps와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Google Apps 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="04c96-103">자습서: Google Apps와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="04c96-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="04c96-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Google Apps를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04c96-105">Google Apps를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="04c96-106">Google Apps에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="04c96-107">사용자가 Azure AD 계정으로 Google Apps에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04c96-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="04c96-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04c96-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04c96-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="04c96-110">Prerequisites</span></span>

<span data-ttu-id="04c96-111">Google Apps와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="04c96-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="04c96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04c96-113">Google Apps Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="04c96-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04c96-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04c96-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04c96-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="04c96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04c96-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="04c96-118">비디오 자습서</span><span class="sxs-lookup"><span data-stu-id="04c96-118">Video tutorial</span></span>
<span data-ttu-id="04c96-119">2분 안에 Google Apps에 Single Sign-On을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="04c96-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="04c96-120">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="04c96-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="04c96-121">**Q: Chromebooks 및 기타 크롬 장치는 Azure AD Single Sign-On과 호환되나요?**</span><span class="sxs-lookup"><span data-stu-id="04c96-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="04c96-122">A: 예, 사용자는 Azure AD 자격 증명을 사용하여 Chromebook 장치에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="04c96-123">사용자가 자격 증명을 두 번 입력해야 하는 이유는 이 [Google Apps 지원 문서](https://support.google.com/chrome/a/answer/6060880) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04c96-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="04c96-124">**Q: Single Sign-On을 사용하도록 설정한 경우 사용자가 자신의 Azure AD 자격 증명을 사용하여 Google 클래스룸, GMail, Google 드라이브, YouTube 등과 같은 Google 제품에 로그인할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="04c96-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="04c96-125">A: 예, [Google 앱](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) 에 따라 조직에 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="04c96-126">**Q: 내 Google 앱 사용자의 하위 집합에만 Single Sign-On을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="04c96-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="04c96-127">A: 아니요, Single Sign-On을 켜는 즉시 모든 Google Apps 사용자가 Azure AD 자격 증명으로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="04c96-128">Google 앱은 여러 ID 공급자를 지원하지 않으므로 Google 앱 환경의 ID 공급자는 Azure AD 또는 Google 중 하나가 될 수 있지만 동시에 둘 다가 될 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="04c96-129">**Q: 사용자가 Windows를 통해 로그인한 경우 암호 입력을 요청하는 메시지가 표시되지 않고 Google Apps에 자동으로 인증되나요?**</span><span class="sxs-lookup"><span data-stu-id="04c96-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="04c96-130">A: 이 시나리오에는 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="04c96-131">첫째, [Azure Active Directory 조인](active-directory-azureadjoin-overview.md)을 통해 Windows 10 장치에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="04c96-132">또는 [AD FS(Active Directory Federation Services)](active-directory-aadconnect-user-signin.md) 배포를 통해 Azure AD에 Single Sign-On을 사용할 수 있도록 설정한 온-프레미스 Active Directory에 도메인 가입한 Windows 장치에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="04c96-133">두 가지 옵션 모두 Azure AD와 Google Apps간에 Single Sign-On을 사용하도록 설정하려면 다음 자습서의 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04c96-134">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="04c96-134">Scenario description</span></span>
<span data-ttu-id="04c96-135">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04c96-136">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04c96-137">갤러리에서 Google Apps 추가</span><span class="sxs-lookup"><span data-stu-id="04c96-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="04c96-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="04c96-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="04c96-139">갤러리에서 Google Apps 추가</span><span class="sxs-lookup"><span data-stu-id="04c96-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="04c96-140">Google Apps가 Azure AD에 통합되도록 구성하려면 갤러리에서 Google Apps를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="04c96-141">**갤러리에서 Google Apps를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="04c96-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="04c96-142">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04c96-144">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="04c96-145">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-145">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="04c96-147">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="04c96-149">검색 상자에 **Google Apps**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-149">In the search box, type **Google Apps**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="04c96-151">결과 창에서 **Google Apps**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04c96-153">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="04c96-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="04c96-154">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Google Apps에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="04c96-155">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Google Apps 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="04c96-156">즉, Azure AD 사용자와 Google Apps의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="04c96-157">이 링크 관계는 Azure AD의 **사용자 이름** 값을 Google Apps의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="04c96-158">Google Apps에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="04c96-159">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="04c96-160">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04c96-161">**[Google Apps 테스트 사용자 만들기](#creating-a-google-apps-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Google Apps에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="04c96-162">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04c96-163">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04c96-164">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="04c96-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04c96-165">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Google Apps 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="04c96-166">**Google Apps에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="04c96-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="04c96-167">Azure Portal의 **Google Apps** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="04c96-169">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="04c96-171">**Google Apps 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="04c96-173">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="04c96-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="04c96-174">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-174">This value is not real.</span></span> <span data-ttu-id="04c96-175">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="04c96-176">[Google 지원 팀](https://www.google.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="04c96-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="04c96-177">**SAML 서명 인증서** 섹션에서 **인증서**를 클릭한 후 컴퓨터에 인증서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="04c96-179">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-179">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="04c96-181">**Google Apps 구성** 섹션에서 **Google Apps 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="04c96-182">**빠른 참조 섹션**에서 **로그아웃 URL, SAML Single Sign-On 서비스 URL 및 암호 변경 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="04c96-184">브라우저에서 새 탭을 열고 관리자 계정을 사용하여 [관리 콘솔](http://admin.google.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="04c96-185">**보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-185">Click **Security**.</span></span> <span data-ttu-id="04c96-186">링크가 보이지 않으면 화면 아래쪽에 있는 **기타 컨트롤** 메뉴에 숨겨져 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![보안을 클릭합니다.][10]

9. <span data-ttu-id="04c96-188">**보안** 페이지에서 **SSO(Single Sign-On) 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![SSO를 클릭합니다.][11]

10. <span data-ttu-id="04c96-190">다음 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-190">Perform the following configuration changes:</span></span>
   
    ![SSL 구성][12]
   
    <span data-ttu-id="04c96-192">a.</span><span class="sxs-lookup"><span data-stu-id="04c96-192">a.</span></span> <span data-ttu-id="04c96-193">**Setup SSO with third party identity provider**(타사 ID 공급자로 SSO 설정)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="04c96-194">b.</span><span class="sxs-lookup"><span data-stu-id="04c96-194">b.</span></span> <span data-ttu-id="04c96-195">Google Apps의 **로그인 페이지 URL** 필드에 Azure Portal에서 복사한 **Single Sign-On 서비스 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="04c96-196">c.</span><span class="sxs-lookup"><span data-stu-id="04c96-196">c.</span></span> <span data-ttu-id="04c96-197">Google Apps의 **로그아웃 페이지 URL** 필드에 Azure Portal에서 복사한 **로그아웃 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="04c96-198">d.</span><span class="sxs-lookup"><span data-stu-id="04c96-198">d.</span></span> <span data-ttu-id="04c96-199">Google Apps의 **암호 변경 URL** 필드에 Azure Portal에서 복사한 **암호 변경 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="04c96-200">e.</span><span class="sxs-lookup"><span data-stu-id="04c96-200">e.</span></span> <span data-ttu-id="04c96-201">Google Apps에서 **확인 인증서**에 대해 Azure Portal에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="04c96-202">f.</span><span class="sxs-lookup"><span data-stu-id="04c96-202">f.</span></span> <span data-ttu-id="04c96-203">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="04c96-204">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="04c96-205">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="04c96-206">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04c96-207">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="04c96-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="04c96-208">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="04c96-210">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="04c96-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="04c96-211">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04c96-213">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04c96-215">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04c96-217">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04c96-219">a.</span><span class="sxs-lookup"><span data-stu-id="04c96-219">a.</span></span> <span data-ttu-id="04c96-220">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04c96-221">b.</span><span class="sxs-lookup"><span data-stu-id="04c96-221">b.</span></span> <span data-ttu-id="04c96-222">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04c96-223">c.</span><span class="sxs-lookup"><span data-stu-id="04c96-223">c.</span></span> <span data-ttu-id="04c96-224">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="04c96-225">d.</span><span class="sxs-lookup"><span data-stu-id="04c96-225">d.</span></span> <span data-ttu-id="04c96-226">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="04c96-227">Google Apps 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="04c96-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="04c96-228">이 섹션의 목적은 Google Apps 소프트웨어에서 Britta Simon이라는 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="04c96-229">Google Apps는 자동 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="04c96-230">이 섹션에는 사용자의 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-230">There is no action for you in this section.</span></span> <span data-ttu-id="04c96-231">Google Apps 소프트웨어에 사용자가 없는 경우 Google Apps 소프트웨어에 액세스하려고 하면 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="04c96-232">사용자를 수동으로 만들어야 하는 경우 [Google 지원 팀](https://www.google.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="04c96-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="04c96-233">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="04c96-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="04c96-234">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Google Apps에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![사용자 할당][200] 

<span data-ttu-id="04c96-236">**Britta Simon을 Google Apps에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="04c96-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="04c96-237">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="04c96-239">응용 프로그램 목록에서 **Google Apps**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-239">In the applications list, select **Google Apps**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="04c96-241">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-241">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="04c96-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-243">Click **Add** button.</span></span> <span data-ttu-id="04c96-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="04c96-246">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="04c96-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04c96-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04c96-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="04c96-249">Testing single sign-on</span></span>

<span data-ttu-id="04c96-250">이 섹션에서 Single Sign-On 설정을 테스트하려면 [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)에서 액세스 패널을 연 다음 테스트 계정에 로그인하고 액세스 패널에서 **Google Apps**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04c96-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04c96-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="04c96-251">Additional resources</span></span>

* [<span data-ttu-id="04c96-252">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="04c96-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04c96-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="04c96-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="04c96-254">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="04c96-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png