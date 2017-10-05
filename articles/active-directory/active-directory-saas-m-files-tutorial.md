---
title: "자습서: M-Files와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 M-Files 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="17e65-103">자습서: Azure Active Directory와 M-Files 통합</span><span class="sxs-lookup"><span data-stu-id="17e65-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="17e65-104">이 자습서에서는 Azure AD(Azure Active Directory)와 M-Files를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17e65-105">M-Files를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17e65-106">M-Files에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="17e65-107">사용자가 해당 Azure AD 계정으로 M-Files에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17e65-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17e65-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17e65-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17e65-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="17e65-110">Prerequisites</span></span>

<span data-ttu-id="17e65-111">M-Files와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="17e65-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="17e65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17e65-113">M-Files Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="17e65-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17e65-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17e65-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17e65-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="17e65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17e65-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17e65-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="17e65-118">Scenario description</span></span>
<span data-ttu-id="17e65-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17e65-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17e65-121">갤러리에서 M-Files 추가</span><span class="sxs-lookup"><span data-stu-id="17e65-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="17e65-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="17e65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="17e65-123">갤러리에서 M-Files 추가</span><span class="sxs-lookup"><span data-stu-id="17e65-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="17e65-124">M-Files의 Azure AD 통합을 구성하려면 갤러리의 M-Files를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17e65-125">**갤러리에서 M-Files를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="17e65-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17e65-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17e65-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17e65-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="17e65-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="17e65-133">검색 상자에 **M-Files**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-133">In the search box, type **M-Files**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="17e65-135">결과 패널에서 **M-Files**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17e65-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="17e65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17e65-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 M-Files에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17e65-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 M-Files 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="17e65-140">즉, Azure AD 사용자와 M-Files의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="17e65-141">M-Files에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17e65-142">M-Files에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17e65-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17e65-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17e65-145">**[M-Files 테스트 사용자 만들기](#creating-a-m-files-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 M-Files에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17e65-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17e65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17e65-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="17e65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17e65-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 M-Files 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="17e65-150">**M-Files에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="17e65-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="17e65-151">Azure Portal의 **M-Files** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="17e65-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="17e65-155">**M-Files 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="17e65-157">a.</span><span class="sxs-lookup"><span data-stu-id="17e65-157">a.</span></span> <span data-ttu-id="17e65-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="17e65-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="17e65-159">b.</span><span class="sxs-lookup"><span data-stu-id="17e65-159">b.</span></span> <span data-ttu-id="17e65-160">**식별자** 텍스트 상자에서 `https://<tenantname>.cloudvault.m-files.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17e65-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-161">These values are not real.</span></span> <span data-ttu-id="17e65-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="17e65-163">이러한 값을 얻으려면 [M-Files 클라이언트 지원 팀](mailto:support@m-files.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="17e65-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="17e65-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="17e65-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17e65-168">응용 프로그램에 대해 SSO를 구성하려면 [M-Files 지원 팀](mailto:support@m-files.com)에 문의하고 다운로드한 메타데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="17e65-169">M-Files 데스크톱 응용 프로그램에 대한 SSO를 구성하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="17e65-170">M-Files 웹 버전에 대해서만 SSO를 구성하려는 경우 추가 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="17e65-171">다음 단계에 따라 Azure AD에서 SSO를 사용하도록 M-Files 데스크톱 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="17e65-172">M-Files를 다운로드하려면 [M-Files 다운로드](https://www.m-files.com/en/download-latest-version) 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="17e65-173">**M-Files 데스크톱 설정** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="17e65-174">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-174">Then, click **Add**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="17e65-176">**문서 자격 증명 모음 연결 속성** 창에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="17e65-178">서버 섹션 아래에서 다음과 같이 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="17e65-179">a.</span><span class="sxs-lookup"><span data-stu-id="17e65-179">a.</span></span> <span data-ttu-id="17e65-180">**이름**에 `<tenant-name>.cloudvault.m-files.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="17e65-181">b.</span><span class="sxs-lookup"><span data-stu-id="17e65-181">b.</span></span> <span data-ttu-id="17e65-182">**포트 번호**에 **4466**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="17e65-183">c.</span><span class="sxs-lookup"><span data-stu-id="17e65-183">c.</span></span> <span data-ttu-id="17e65-184">**프로토콜**에서 **HTTPS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="17e65-185">d.</span><span class="sxs-lookup"><span data-stu-id="17e65-185">d.</span></span> <span data-ttu-id="17e65-186">**인증** 필드에서 **특정 Windows 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="17e65-187">그러면 서명 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="17e65-188">Azure AD 자격 증명을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="17e65-189">e.</span><span class="sxs-lookup"><span data-stu-id="17e65-189">e.</span></span> <span data-ttu-id="17e65-190">**서버의 자격 증명 모음**에서 서버에 있는 해당 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="17e65-191">f.</span><span class="sxs-lookup"><span data-stu-id="17e65-191">f.</span></span> <span data-ttu-id="17e65-192">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="17e65-193">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17e65-194">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17e65-195">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17e65-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="17e65-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="17e65-197">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="17e65-199">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="17e65-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17e65-200">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17e65-202">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17e65-204">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17e65-206">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17e65-208">a.</span><span class="sxs-lookup"><span data-stu-id="17e65-208">a.</span></span> <span data-ttu-id="17e65-209">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17e65-210">b.</span><span class="sxs-lookup"><span data-stu-id="17e65-210">b.</span></span> <span data-ttu-id="17e65-211">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17e65-212">c.</span><span class="sxs-lookup"><span data-stu-id="17e65-212">c.</span></span> <span data-ttu-id="17e65-213">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17e65-214">d.</span><span class="sxs-lookup"><span data-stu-id="17e65-214">d.</span></span> <span data-ttu-id="17e65-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="17e65-216">M-Files 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="17e65-216">Creating a M-Files test user</span></span>

<span data-ttu-id="17e65-217">이 섹션의 목표는 M-Files에서 Britta Simon이라는 사용자를 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="17e65-218">M-Files에 사용자를 추가하려면 [M-Files 지원 팀](mailto:support@m-files.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="17e65-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17e65-219">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="17e65-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17e65-220">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 M-Files에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![사용자 할당][200] 

<span data-ttu-id="17e65-222">**Britta Simon을 M-Files에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="17e65-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="17e65-223">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="17e65-225">응용 프로그램 목록에서 **M-Files**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-225">In the applications list, select **M-Files**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="17e65-227">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-227">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="17e65-229">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-229">Click **Add** button.</span></span> <span data-ttu-id="17e65-230">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="17e65-232">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17e65-233">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17e65-234">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17e65-235">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="17e65-235">Testing single sign-on</span></span>

<span data-ttu-id="17e65-236">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="17e65-237">액세스 패널에서 M-Files 타일을 클릭하면 M-Files 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="17e65-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17e65-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="17e65-238">Additional resources</span></span>

* [<span data-ttu-id="17e65-239">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="17e65-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17e65-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="17e65-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

