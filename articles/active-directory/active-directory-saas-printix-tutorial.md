---
title: "자습서: Printix와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Printix 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="61d67-103">자습서: Printix와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="61d67-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="61d67-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Printix를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61d67-105">Printix를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61d67-106">Printix에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="61d67-107">사용자가 해당 Azure AD 계정으로 Printix에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61d67-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61d67-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61d67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61d67-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="61d67-110">Prerequisites</span></span>

<span data-ttu-id="61d67-111">Printix와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="61d67-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="61d67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61d67-113">Printix Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="61d67-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61d67-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61d67-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61d67-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="61d67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61d67-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61d67-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="61d67-118">Scenario description</span></span>
<span data-ttu-id="61d67-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61d67-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61d67-121">갤러리에서 Printix 추가</span><span class="sxs-lookup"><span data-stu-id="61d67-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="61d67-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="61d67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="61d67-123">갤러리에서 Printix 추가</span><span class="sxs-lookup"><span data-stu-id="61d67-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="61d67-124">Printix의 Azure AD 통합을 구성하려면 갤러리의 Printix를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61d67-125">**갤러리에서 Printix를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="61d67-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61d67-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="61d67-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61d67-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="61d67-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="61d67-133">검색 상자에 **Printix**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-133">In the search box, type **Printix**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="61d67-135">결과 패널에서 **Printix**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61d67-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="61d67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61d67-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Printix에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61d67-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Printix 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="61d67-140">즉, Azure AD 사용자와 Printix의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="61d67-141">Printix에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61d67-142">Printix에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61d67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="61d67-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61d67-145">**[Printix 테스트 사용자 만들기](#creating-a-printix-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Printix에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="61d67-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61d67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61d67-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="61d67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61d67-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Printix 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="61d67-150">**Printix에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="61d67-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="61d67-151">Azure Portal의 **Printix** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="61d67-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="61d67-155">**Printix 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="61d67-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="61d67-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61d67-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-158">The value is not real.</span></span> <span data-ttu-id="61d67-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="61d67-160">값을 얻으려면 [Printix 클라이언트 지원 팀](mailto:support@printix.net)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="61d67-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="61d67-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="61d67-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61d67-165">Printix 테넌트에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="61d67-166">위쪽의 메뉴에서 오른쪽 위 모서리에 있는 아이콘을 클릭하고 "**인증**"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="61d67-168">**설정** 탭에서 **Azure/Office 365 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="61d67-170">**Azure** 탭에서 "**페더레이션 메타데이터 문서**"의 텍스트 상자에 페더레이션 메타데이터 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="61d67-171">Azure AD에서 다운로드한 메타데이터 xml 파일을 [Printix 지원 팀](mailto:support@printix.net)에 첨부하여 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="61d67-172">그러면 xml 파일을 업로드하고 페더레이션 메타데이터 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="61d67-174">"**테스트**"단추를 클릭한 후 테스트가 성공적이면 "**확인**" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="61d67-175">**테스트** 단추를 클릭하면 Azure active directory 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="61d67-176">여기서 "테스트가 성공적이었다"는 것은 Azure 테스트 계정의 자격 증명을 입력한 후 "Settings tested OK"(테스트 확인된 설정) 메시지 팝업 창이 나타남을 의미합니다. 그런 다음 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="61d67-178">"**인증**" 페이지에 있는 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="61d67-179">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61d67-180">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61d67-181">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61d67-182">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="61d67-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="61d67-183">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="61d67-185">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="61d67-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61d67-186">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61d67-188">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61d67-190">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61d67-192">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61d67-194">a.</span><span class="sxs-lookup"><span data-stu-id="61d67-194">a.</span></span> <span data-ttu-id="61d67-195">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61d67-196">b.</span><span class="sxs-lookup"><span data-stu-id="61d67-196">b.</span></span> <span data-ttu-id="61d67-197">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61d67-198">c.</span><span class="sxs-lookup"><span data-stu-id="61d67-198">c.</span></span> <span data-ttu-id="61d67-199">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61d67-200">d.</span><span class="sxs-lookup"><span data-stu-id="61d67-200">d.</span></span> <span data-ttu-id="61d67-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="61d67-202">Printix 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="61d67-202">Creating a Printix test user</span></span>

<span data-ttu-id="61d67-203">이 섹션은 Printix에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="61d67-204">Printix는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="61d67-205">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-205">There is no action item for you in this section.</span></span> <span data-ttu-id="61d67-206">새 사용자가 아직 존재하지 않는 경우 Printix에 액세스하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="61d67-207">사용자를 수동으로 생성해야 하는 경우 [Printix 지원 팀](mailto:support@printix.net)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61d67-208">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="61d67-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61d67-209">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Printix에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![사용자 할당][200] 

<span data-ttu-id="61d67-211">**Britta Simon을 Printix에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="61d67-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="61d67-212">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="61d67-214">응용 프로그램 목록에서 **Printix**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-214">In the applications list, select **Printix**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="61d67-216">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-216">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="61d67-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-218">Click **Add** button.</span></span> <span data-ttu-id="61d67-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="61d67-221">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="61d67-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61d67-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61d67-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="61d67-224">Testing single sign-on</span></span>

<span data-ttu-id="61d67-225">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61d67-226">액세스 패널에서 Printix 타일을 클릭하면 Printix 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="61d67-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61d67-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="61d67-227">Additional resources</span></span>

* [<span data-ttu-id="61d67-228">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="61d67-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61d67-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="61d67-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

