---
title: "자습서: BenSelect와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 BenSelect 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="7c65a-103">자습서: BenSelect와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7c65a-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="7c65a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 BenSelect를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c65a-105">BenSelect를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c65a-106">BenSelect에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="7c65a-107">사용자가 해당 Azure AD 계정으로 BenSelect에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c65a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c65a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c65a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c65a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c65a-110">Prerequisites</span></span>

<span data-ttu-id="7c65a-111">BenSelect와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="7c65a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7c65a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c65a-113">BenSelect Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7c65a-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c65a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c65a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c65a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7c65a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c65a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c65a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7c65a-118">Scenario description</span></span>
<span data-ttu-id="7c65a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c65a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c65a-121">갤러리에서 BenSelect 추가</span><span class="sxs-lookup"><span data-stu-id="7c65a-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="7c65a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7c65a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="7c65a-123">갤러리에서 BenSelect 추가</span><span class="sxs-lookup"><span data-stu-id="7c65a-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="7c65a-124">BenSelect의 Azure AD 통합을 구성하려면 갤러리의 BenSelect를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c65a-125">**갤러리에서 BenSelect를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7c65a-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c65a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c65a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c65a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7c65a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7c65a-133">검색 상자에 **BenSelect**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-133">In the search box, type **BenSelect**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="7c65a-135">결과 패널에서 **BenSelect**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c65a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7c65a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c65a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BenSelect에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7c65a-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 BenSelect 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="7c65a-140">즉, Azure AD 사용자와 BenSelect의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="7c65a-141">BenSelect에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7c65a-142">BenSelect에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c65a-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c65a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c65a-145">**[BenSelect 테스트 사용자 만들기](#creating-a-benselect-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 BenSelect에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c65a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c65a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c65a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7c65a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c65a-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 BenSelect 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="7c65a-150">**BenSelect에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7c65a-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="7c65a-151">Azure Portal의 **BenSelect** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7c65a-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="7c65a-155">**BenSelect 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="7c65a-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="7c65a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c65a-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-158">This value is not real.</span></span> <span data-ttu-id="7c65a-159">실제 회신 URL로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="7c65a-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="7c65a-160">이 값을 가져오려면 [BenSelect 지원팀](mailto:support@selerix.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7c65a-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="7c65a-161">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="7c65a-163">BenSelect 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7c65a-164">이 응용 프로그램에 대해 다음 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-164">Configure the following claims for this application.</span></span> <span data-ttu-id="7c65a-165">응용 프로그램 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="7c65a-166">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-166">The following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="7c65a-168">**Single Sign-On** 대화 상자의 **사용자 특성** 섹션에서</span><span class="sxs-lookup"><span data-stu-id="7c65a-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="7c65a-169">a.</span><span class="sxs-lookup"><span data-stu-id="7c65a-169">a.</span></span> <span data-ttu-id="7c65a-170">**사용자 ID** 드롭다운 목록에서 **ExtractMailPrefix**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="7c65a-171">b.</span><span class="sxs-lookup"><span data-stu-id="7c65a-171">b.</span></span> <span data-ttu-id="7c65a-172">**전자 메일** 드롭다운 목록에서 **user.userprincipalname**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="7c65a-173">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-173">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7c65a-175">**BenSelect 구성** 섹션에서 **BenSelect 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7c65a-176">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="7c65a-178">**BenSelect** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서(원시)**, **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 [BenSelect 지원팀](mailto:support@selerix.com)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="7c65a-179">app2101 등과 같은 해당 서버에서 SSO를 설정할 수 있도록 이 통합에 SHA256 알고리즘(SHA1은 지원되지 않음)이 필요하다는 내용을 언급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="7c65a-180">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7c65a-181">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7c65a-182">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c65a-183">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7c65a-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c65a-184">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7c65a-186">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7c65a-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c65a-187">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c65a-189">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c65a-191">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c65a-193">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c65a-195">a.</span><span class="sxs-lookup"><span data-stu-id="7c65a-195">a.</span></span> <span data-ttu-id="7c65a-196">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c65a-197">b.</span><span class="sxs-lookup"><span data-stu-id="7c65a-197">b.</span></span> <span data-ttu-id="7c65a-198">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c65a-199">c.</span><span class="sxs-lookup"><span data-stu-id="7c65a-199">c.</span></span> <span data-ttu-id="7c65a-200">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c65a-201">d.</span><span class="sxs-lookup"><span data-stu-id="7c65a-201">d.</span></span> <span data-ttu-id="7c65a-202">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="7c65a-203">BenSelect 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7c65a-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="7c65a-204">이 섹션은 BenSelect에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="7c65a-205">BenSelect 계정에 사용자를 추가하려면 [BenSelect 지원팀](mailto:support@selerix.com)과 함께 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="7c65a-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c65a-206">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7c65a-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c65a-207">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 BenSelect에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7c65a-209">**Britta Simon을 BenSelect에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7c65a-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="7c65a-210">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7c65a-212">응용 프로그램 목록에서 **BenSelect**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-212">In the applications list, select **BenSelect**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="7c65a-214">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-214">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7c65a-216">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-216">Click **Add** button.</span></span> <span data-ttu-id="7c65a-217">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7c65a-219">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c65a-220">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c65a-221">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c65a-222">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7c65a-222">Testing single sign-on</span></span>

<span data-ttu-id="7c65a-223">이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7c65a-224">액세스 패널에서 BenSelect 타일을 클릭하면 BenSelect 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c65a-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c65a-225">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7c65a-225">Additional resources</span></span>

* [<span data-ttu-id="7c65a-226">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7c65a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c65a-227">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7c65a-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

