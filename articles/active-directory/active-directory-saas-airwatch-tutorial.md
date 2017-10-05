---
title: "자습서: AirWatch와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 AirWatch 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="1be5e-103">자습서: AirWatch와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1be5e-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="1be5e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 AirWatch를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1be5e-105">AirWatch와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1be5e-106">AirWatch에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="1be5e-107">사용자가 해당 Azure AD 계정으로 AirWatch에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1be5e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1be5e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1be5e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1be5e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1be5e-110">Prerequisites</span></span>

<span data-ttu-id="1be5e-111">AirWatch와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="1be5e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1be5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1be5e-113">AirWatch Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1be5e-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1be5e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1be5e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1be5e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1be5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1be5e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1be5e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1be5e-118">Scenario description</span></span>
<span data-ttu-id="1be5e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1be5e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1be5e-121">갤러리에서 AirWatch 추가</span><span class="sxs-lookup"><span data-stu-id="1be5e-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="1be5e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1be5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="1be5e-123">갤러리에서 AirWatch 추가</span><span class="sxs-lookup"><span data-stu-id="1be5e-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="1be5e-124">AirWatch의 Azure AD 통합을 구성하려면 갤러리의 AirWatch를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1be5e-125">**갤러리에서 AirWatch를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1be5e-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1be5e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1be5e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1be5e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1be5e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1be5e-133">검색 상자에 **AirWatch**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-133">In the search box, type **AirWatch**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="1be5e-135">결과 패널에서 **AirWatch**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1be5e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1be5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1be5e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AirWatch에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1be5e-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 AirWatch 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="1be5e-140">즉, Azure AD 사용자와 AirWatch의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="1be5e-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 AirWatch의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="1be5e-142">AirWatch에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1be5e-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1be5e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1be5e-145">**[AirWatch 테스트 사용자 만들기](#creating-a-airwatch-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 AirWatch에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1be5e-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1be5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1be5e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1be5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1be5e-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 AirWatch 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="1be5e-150">**AirWatch에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1be5e-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="1be5e-151">Azure Portal의 **AirWatch** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1be5e-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="1be5e-155">**AirWatch 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="1be5e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1be5e-157">a.</span></span> <span data-ttu-id="1be5e-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="1be5e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="1be5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1be5e-159">b.</span></span> <span data-ttu-id="1be5e-160">**식별자** 텍스트 상자에 해당 값으로 `AirWatch`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1be5e-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-161">This value is not the real.</span></span> <span data-ttu-id="1be5e-162">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="1be5e-163">이 값을 얻으려면 [AirWatch Client 지원 팀](http://www.air-watch.com/company/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1be5e-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="1be5e-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="1be5e-166">**AirWatch 구성** 섹션에서 **AirWatch 구성**을 클릭하여 **로그인 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1be5e-167">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="1be5e-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-169">Click **Save** button.</span></span>

    <span data-ttu-id="1be5e-170">![Single Sign-On 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="1be5e-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="1be5e-171">다른 웹 브라우저 창에서 AirWatch 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="1be5e-172">왼쪽 탐색 창에서 **계정**과 **관리자**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="1be5e-173">![관리자](./media/active-directory-saas-airwatch-tutorial/ic791920.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="1be5e-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="1be5e-174">**설정** 메뉴를 확장한 다음 **디렉터리 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="1be5e-175">![설정](./media/active-directory-saas-airwatch-tutorial/ic791921.png "설정")</span><span class="sxs-lookup"><span data-stu-id="1be5e-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="1be5e-176">**사용자** 탭을 클릭하고 **Base DN** 텍스트 상자에 도메인 이름을 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="1be5e-177">![사용자](./media/active-directory-saas-airwatch-tutorial/ic791922.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1be5e-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="1be5e-178">**서버** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="1be5e-179">![서버](./media/active-directory-saas-airwatch-tutorial/ic791923.png "서버")</span><span class="sxs-lookup"><span data-stu-id="1be5e-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="1be5e-180">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="1be5e-181">![업로드](./media/active-directory-saas-airwatch-tutorial/ic791924.png "업로드")</span><span class="sxs-lookup"><span data-stu-id="1be5e-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="1be5e-182">a.</span><span class="sxs-lookup"><span data-stu-id="1be5e-182">a.</span></span> <span data-ttu-id="1be5e-183">**디렉터리 유형**으로 **없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="1be5e-184">b.</span><span class="sxs-lookup"><span data-stu-id="1be5e-184">b.</span></span> <span data-ttu-id="1be5e-185">**인증에 SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="1be5e-186">c.</span><span class="sxs-lookup"><span data-stu-id="1be5e-186">c.</span></span> <span data-ttu-id="1be5e-187">다운로드한 인증서를 업로드하려면 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="1be5e-188">**요청** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="1be5e-189">![요청](./media/active-directory-saas-airwatch-tutorial/ic791925.png "요청")</span><span class="sxs-lookup"><span data-stu-id="1be5e-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="1be5e-190">a.</span><span class="sxs-lookup"><span data-stu-id="1be5e-190">a.</span></span> <span data-ttu-id="1be5e-191">**요청 바인딩 형식**으로 **POST**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="1be5e-192">b.</span><span class="sxs-lookup"><span data-stu-id="1be5e-192">b.</span></span> <span data-ttu-id="1be5e-193">Azure Portal의 **Airwatch에서 Single Sign-on 구성** 대화 상자 페이지에서 **SAML Single Sign-On 서비스 URL** 값을 복사한 다음 **ID 공급자 Single Sign-On URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="1be5e-194">c.</span><span class="sxs-lookup"><span data-stu-id="1be5e-194">c.</span></span> <span data-ttu-id="1be5e-195">**NameID 형식**으로 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="1be5e-196">d.</span><span class="sxs-lookup"><span data-stu-id="1be5e-196">d.</span></span> <span data-ttu-id="1be5e-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-197">Click **Save**.</span></span>

14. <span data-ttu-id="1be5e-198">**사용자** 탭을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="1be5e-199">![사용자](./media/active-directory-saas-airwatch-tutorial/ic791926.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1be5e-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="1be5e-200">**특성** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="1be5e-201">![특성](./media/active-directory-saas-airwatch-tutorial/ic791927.png "특성")</span><span class="sxs-lookup"><span data-stu-id="1be5e-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="1be5e-202">a.</span><span class="sxs-lookup"><span data-stu-id="1be5e-202">a.</span></span> <span data-ttu-id="1be5e-203">**개체 식별자** 텍스트 상자에 **http://schemas.microsoft.com/identity/claims/objectidentifier**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="1be5e-204">b.</span><span class="sxs-lookup"><span data-stu-id="1be5e-204">b.</span></span> <span data-ttu-id="1be5e-205">**사용자 이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="1be5e-206">c.</span><span class="sxs-lookup"><span data-stu-id="1be5e-206">c.</span></span> <span data-ttu-id="1be5e-207">**표시 이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="1be5e-208">d.</span><span class="sxs-lookup"><span data-stu-id="1be5e-208">d.</span></span> <span data-ttu-id="1be5e-209">**이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="1be5e-210">e.</span><span class="sxs-lookup"><span data-stu-id="1be5e-210">e.</span></span> <span data-ttu-id="1be5e-211">**성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="1be5e-212">f.</span><span class="sxs-lookup"><span data-stu-id="1be5e-212">f.</span></span> <span data-ttu-id="1be5e-213">**전자 메일** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="1be5e-214">g.</span><span class="sxs-lookup"><span data-stu-id="1be5e-214">g.</span></span> <span data-ttu-id="1be5e-215">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1be5e-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1be5e-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="1be5e-217">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1be5e-219">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1be5e-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1be5e-220">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1be5e-222">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1be5e-224">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1be5e-226">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1be5e-228">a.</span><span class="sxs-lookup"><span data-stu-id="1be5e-228">a.</span></span> <span data-ttu-id="1be5e-229">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1be5e-230">b.</span><span class="sxs-lookup"><span data-stu-id="1be5e-230">b.</span></span> <span data-ttu-id="1be5e-231">**사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1be5e-232">c.</span><span class="sxs-lookup"><span data-stu-id="1be5e-232">c.</span></span> <span data-ttu-id="1be5e-233">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1be5e-234">d.</span><span class="sxs-lookup"><span data-stu-id="1be5e-234">d.</span></span> <span data-ttu-id="1be5e-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="1be5e-236">AirWatch 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1be5e-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="1be5e-237">Azure AD 사용자가 AirWatch에 로그인할 수 있도록 하려면 AirWatch로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="1be5e-238">AirWatch의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="1be5e-239">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1be5e-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1be5e-240">**AirWatch** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="1be5e-241">왼쪽의 탐색 창에서 **계정**과 **사용자**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="1be5e-242">![사용자](./media/active-directory-saas-airwatch-tutorial/ic791929.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1be5e-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="1be5e-243">**사용자** 메뉴에서 **목록 보기**와 **추가 \> 사용자 추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="1be5e-244">![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791930.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="1be5e-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="1be5e-245">**사용자 추가/편집** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="1be5e-246">![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791931.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="1be5e-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="1be5e-247">관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 계정의 **사용자 이름**, **암호**, **암호 확인**, **이름**, **성**, **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="1be5e-248">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1be5e-249">다른 AirWatch 사용자 계정 생성 도구 또는 AirWatch가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1be5e-250">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1be5e-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1be5e-251">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 AirWatch에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1be5e-253">**Britta Simon을 AirWatch에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1be5e-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="1be5e-254">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1be5e-256">응용 프로그램 목록에서 **AirWatch**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-256">In the applications list, select **AirWatch**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="1be5e-258">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-258">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1be5e-260">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-260">Click **Add** button.</span></span> <span data-ttu-id="1be5e-261">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1be5e-263">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1be5e-264">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1be5e-265">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1be5e-266">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1be5e-266">Testing single sign-on</span></span>

<span data-ttu-id="1be5e-267">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1be5e-268">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1be5e-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1be5e-269">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1be5e-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1be5e-270">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1be5e-270">Additional resources</span></span>

* [<span data-ttu-id="1be5e-271">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1be5e-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1be5e-272">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1be5e-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

