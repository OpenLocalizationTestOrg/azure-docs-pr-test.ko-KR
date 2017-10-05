---
title: "할당한 응용 프로그램이 액세스 패널에 표시되지 않음 | Microsoft Docs"
description: "응용 프로그램이 액세스 패널에 표시되지 않는 문제 해결"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="64a44-103">할당한 응용 프로그램이 액세스 패널에 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="64a44-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="64a44-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="64a44-105">이러한 응용 프로그램은 Azure AD 포털에서 사용자를 대신하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="64a44-106">응용 프로그램을 액세스 패널에 표시하려면 응용 프로그램이 올바르게 구성되어 있고, 사용자나 그 사용자가 속한 그룹에 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="64a44-107">사용자가 볼 수 있는 앱의 종류는 다음과 같은 범주로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="64a44-108">Office 365 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="64a44-108">Office 365 Applications</span></span>

-   <span data-ttu-id="64a44-109">페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="64a44-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="64a44-110">암호 기반 SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="64a44-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="64a44-111">기존 SSO 솔루션을 사용한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="64a44-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="64a44-112">먼저 확인해야 할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="64a44-112">General issues to check first</span></span>

-   <span data-ttu-id="64a44-113">사용자에게 방금 응용 프로그램이 추가되었으면 몇 분 후에 사용자의 액세스 패널에 로그인했다가 다시 로그아웃하고 응용 프로그램이 추가되었는지 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="64a44-114">라이선스가 사용자 또는 사용자가 구성원인 그룹에서 제거된 경우 변경 사항이 만들어질 그룹의 크기 및 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="64a44-115">액세스 패널에 로그인하기 전에 잠시 여유 시간을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="64a44-116">응용 프로그램 구성에 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="64a44-116">Problems related to application configuration</span></span>

<span data-ttu-id="64a44-117">응용 프로그램이 올바르게 구성되지 않아서 사용자의 액세스 패널에 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="64a44-118">다음은 응용 프로그램 구성과 관련된 문제를 해결할 수 있는 몇 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="64a44-119">Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="64a44-120">비갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="64a44-121">Azure AD 갤러리 응용 프로그램에 대해 암호 Single Sign-On 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="64a44-122">비갤러리 응용 프로그램에 대해 암호 Single Sign-On 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="64a44-123">Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="64a44-124">Azure AD 갤러리에서 Enterprise Single Sign-On 기능을 사용하도록 설정된 모든 응용 프로그램은 단계별 자습서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="64a44-125">[Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)에 액세스하면 자세한 단계별 지침을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="64a44-126">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="64a44-127">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="64a44-128">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="64a44-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="64a44-129">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="64a44-130">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="64a44-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="64a44-131">응용 프로그램에서 Azure AD 메타데이터 값 구성(로그온 URL, 발급자, 로그아웃 URL 및 인증서)</span><span class="sxs-lookup"><span data-stu-id="64a44-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="64a44-132">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="64a44-133">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-134">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="64a44-135">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-136">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-137">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-138">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="64a44-139">**갤러리에서 추가** 섹션의 **이름 입력** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="64a44-140">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="64a44-141">응용 프로그램을 추가하기 전에 **이름** 텍스트 상자에서 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="64a44-142">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="64a44-143">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="64a44-144">Azure AD 갤러리에서 응용 프로그램의 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="64a44-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="64a44-145">응용 프로그램에 대한 Single Sign-On을 구성하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-146">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-147">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-148">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-149">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-150">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="64a44-151">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-152">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="64a44-153">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-154">**모드** 드롭다운에서 **SAML 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="64a44-155">**도메인 및 URL**에 필요한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="64a44-156">이러한 값은 응용 프로그램 공급업체에서 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="64a44-157">응용 프로그램을 SP에서 시작한 SSO로 구성하려면 로그온 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="64a44-158">일부 응용 프로그램의 경우는 식별자도 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="64a44-159">응용 프로그램을 IdP에서 시작한 SSO로 구성하려면 회신 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="64a44-160">일부 응용 프로그램의 경우는 식별자도 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="64a44-161">**선택 사항:** 선택적인 값을 보려면 **고급 URL 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="64a44-162">**사용자 특성**의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="64a44-163">**선택 사항:** 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="64a44-164">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="64a44-164">To add an attribute:</span></span>

   1. <span data-ttu-id="64a44-165">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-165">click **Add attribute**.</span></span> <span data-ttu-id="64a44-166">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="64a44-167">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-167">click **Save.**</span></span> <span data-ttu-id="64a44-168">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="64a44-169">응용 프로그램의 Single Sign-On을 구성하는 방법에 관한 문서에 액세스하려면 **&lt;응용 프로그램 이름&gt; 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="64a44-170">또한 응용 프로그램에 SSO를 설정하는 데 필요한 메타데이터 URL 및 인증서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="64a44-171">구성을 저장하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="64a44-172">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="64a44-173">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="64a44-174">사용자 식별자를 선택하거나 사용자 특성을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-175">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-176">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-177">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-178">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-179">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="64a44-180">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-181">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="64a44-182">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-183">**사용자 특성** 섹션 아래의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="64a44-184">사용자를 인증하려면 선택한 옵션이 응용 프로그램의 예상 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="64a44-185">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="64a44-186">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="64a44-187">사용자 특성을 추가하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭하여 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="64a44-188">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="64a44-188">To add an attribute:</span></span>

   1. <span data-ttu-id="64a44-189">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-189">click **Add attribute**.</span></span> <span data-ttu-id="64a44-190">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="64a44-191">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-191">click **Save.**</span></span> <span data-ttu-id="64a44-192">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="64a44-193">Azure AD 메타데이터 또는 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="64a44-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="64a44-194">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-195">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-196">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-197">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-198">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-199">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="64a44-200">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-201">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="64a44-202">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-203">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="64a44-204">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="64a44-205">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="64a44-206">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="64a44-207">비갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="64a44-208">비갤러리 응용 프로그램을 구성하려면 Azure AD 프리미엄이 있어야 하며 응용 프로그램에서 SAML 2.0을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="64a44-209">Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="64a44-210">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="64a44-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="64a44-211">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="64a44-212">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="64a44-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="64a44-213">응용 프로그램에서 Azure AD 메타데이터 값 구성(로그온 URL, 발급자, 로그아웃 URL 및 인증서)</span><span class="sxs-lookup"><span data-stu-id="64a44-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="64a44-214">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="64a44-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="64a44-215">Azure AD 갤러리에 없는 응용 프로그램에 대해 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-216">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-217">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-218">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-219">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-220">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="64a44-221">**고유한 응용 프로그램 추가** 섹션에서 **비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="64a44-222">**이름** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="64a44-223">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="64a44-224">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="64a44-225">**모드** 드롭다운에서 **SAML 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="64a44-226">**도메인 및 URL**에 필요한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="64a44-227">이러한 값은 응용 프로그램 공급업체에서 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="64a44-228">응용 프로그램을 IdP에서 시작한 SSO로 구성하려면 회신 URL과 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="64a44-229">**선택 사항:** 응용 프로그램을 SP에서 시작한 SSO로 구성하려면 로그온 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="64a44-230">**사용자 특성**의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="64a44-231">**선택 사항:** 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="64a44-232">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="64a44-232">To add an attribute:</span></span>

   1. <span data-ttu-id="64a44-233">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-233">click **Add attribute**.</span></span> <span data-ttu-id="64a44-234">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="64a44-235">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-235">Click **Save.**</span></span> <span data-ttu-id="64a44-236">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="64a44-237">응용 프로그램의 Single Sign-On을 구성하는 방법에 관한 문서에 액세스하려면 **&lt;응용 프로그램 이름&gt; 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="64a44-238">또한 응용 프로그램에 필요한 Azure AD URL과 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="64a44-239">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="64a44-240">사용자 식별자를 선택하거나 사용자 특성을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-241">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-242">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-243">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-244">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-245">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="64a44-246">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-247">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="64a44-248">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-249">**사용자 특성** 섹션 아래의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="64a44-250">사용자를 인증하려면 선택한 옵션이 응용 프로그램의 예상 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="64a44-251">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="64a44-252">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="64a44-253">사용자 특성을 추가하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭하여 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="64a44-254">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="64a44-254">To add an attribute:</span></span>

   1. <span data-ttu-id="64a44-255">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-255">click **Add attribute**.</span></span> <span data-ttu-id="64a44-256">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="64a44-257">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-257">Click **Save.**</span></span> <span data-ttu-id="64a44-258">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="64a44-259">Azure AD 메타데이터 또는 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="64a44-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="64a44-260">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-261">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-262">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-263">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-264">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-265">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="64a44-266">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-267">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="64a44-268">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-269">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="64a44-270">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="64a44-271">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="64a44-272">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="64a44-273">Azure AD 갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="64a44-274">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="64a44-275">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="64a44-276">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="64a44-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="64a44-277">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="64a44-278">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-279">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="64a44-280">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-281">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-282">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-283">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="64a44-284">**갤러리에서 추가** 섹션의 **이름 입력** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="64a44-285">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="64a44-286">응용 프로그램을 추가하기 전에 **이름** 텍스트 상자에서 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="64a44-287">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="64a44-288">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="64a44-289">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="64a44-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="64a44-290">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-291">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-292">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-293">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-294">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-295">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="64a44-296">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-297">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="64a44-298">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-299">**암호 기반의 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="64a44-300">[응용 프로그램에 사용자를 할당합니다](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="64a44-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="64a44-301">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="64a44-302">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="64a44-303">비갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="64a44-304">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="64a44-305">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="64a44-306">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="64a44-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="64a44-307">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-307">Add a non-gallery application</span></span>

<span data-ttu-id="64a44-308">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-309">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="64a44-310">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-311">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-312">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-313">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="64a44-314">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="64a44-315">**이름** 텍스트 상자에 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="64a44-316">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-316">Select **Add.**</span></span>

<span data-ttu-id="64a44-317">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="64a44-318">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="64a44-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="64a44-319">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-320">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="64a44-321">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-322">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-323">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-324">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="64a44-325">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-326">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="64a44-327">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-328">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="64a44-329">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="64a44-330">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="64a44-331">URL에서 로그인 필드가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="64a44-332">[응용 프로그램에 사용자를 할당합니다](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="64a44-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="64a44-333">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="64a44-334">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="64a44-335">사용자의 응용 프로그램 할당과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="64a44-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="64a44-336">사용자에게 응용 프로그램이 할당되지 않아 액세스 패널에서 응용 프로그램이 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="64a44-337">다음은 확인할 몇 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="64a44-338">사용자가 응용 프로그램에 할당되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="64a44-339">응용 프로그램에 사용자를 직접 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="64a44-340">사용자에게 응용 프로그램과 관련된 라이선스가 할당되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="64a44-341">사용자에게 라이선스를 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="64a44-342">사용자가 응용 프로그램에 할당되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="64a44-343">사용자가 응용 프로그램에 할당되었는지 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-344">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="64a44-345">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-346">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-347">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-348">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="64a44-349">문제의 응용 프로그램 이름을 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="64a44-350">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="64a44-351">사용자가 응용 프로그램에 할당되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="64a44-352">할당되지 않았으면 “응용 프로그램에 사용자를 직접 할당하는 방법”에 있는 단계를 수행하여 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="64a44-353">응용 프로그램에 사용자를 직접 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="64a44-354">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-355">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="64a44-356">왼쪽 주 탐색 메뉴의 맨 아래에서 **더 많은 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-357">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-358">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-359">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="64a44-360">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-361">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="64a44-362">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-363">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="64a44-364">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="64a44-365">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="64a44-366">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="64a44-367">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="64a44-368">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="64a44-369">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="64a44-370">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="64a44-371">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="64a44-372">짧은 시간 후에 선택한 사용자는 액세스 패널에서 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="64a44-373">사용자에게 응용 프로그램과 관련된 라이센스가 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="64a44-374">사용자의 할당된 라이선스를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-375">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="64a44-376">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-377">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-378">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="64a44-379">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-379">click **All users**.</span></span>

6.  <span data-ttu-id="64a44-380">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="64a44-381">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="64a44-382">사용자가 Office 라이선스에 할당된 경우 사용자의 액세스 패널에 나타나도록 자사 Office 응용 프로그램을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="64a44-383">사용자에게 라이선스를 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-383">How to assign a user a license</span></span> 

<span data-ttu-id="64a44-384">사용자에게 라이선스를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-385">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="64a44-386">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-387">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-388">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="64a44-389">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-389">click **All users**.</span></span>

6.  <span data-ttu-id="64a44-390">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="64a44-391">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="64a44-392">**할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="64a44-393">사용 가능한 제품 목록에서 **하나 이상의 제품**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="64a44-394">**선택 사항** 제품을 상세하게 할당하려면 **할당 옵션** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="64a44-395">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="64a44-396">**할당** 단추를 클릭하여 이러한 라이선스를 이 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="64a44-397">그룹의 응용 프로그램 할당과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="64a44-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="64a44-398">사용자는 응용 프로그램이 할당된 그룹에 속해 있으므로 액세스 패널에 응용 프로그램이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="64a44-399">다음은 확인할 몇 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="64a44-400">사용자의 그룹 멤버 자격 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="64a44-401">그룹에 응용 프로그램을 직접 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="64a44-402">사용자가 라이선스에 할당된 그룹에 속해 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="64a44-403">그룹에 라이선스를 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="64a44-404">사용자의 그룹 멤버 자격 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-404">Check a user’s group memberships</span></span>

<span data-ttu-id="64a44-405">그룹의 멤버 자격을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-406">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="64a44-407">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-408">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-409">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="64a44-410">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-410">click **All users**.</span></span>

6.  <span data-ttu-id="64a44-411">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="64a44-412">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-412">click **Groups**.</span></span>

8.  <span data-ttu-id="64a44-413">사용자가 응용 프로그램에 할당된 그룹에 속하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="64a44-414">그룹에서 사용자를 제거하려는 경우 그룹의 **행을 클릭**하고 삭제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="64a44-415">그룹에 응용 프로그램을 직접 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="64a44-416">응용 프로그램에 하나 이상의 그룹을 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-417">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="64a44-418">왼쪽 주 탐색 메뉴의 맨 아래에서 **더 많은 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-419">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-420">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="64a44-421">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="64a44-422">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="64a44-423">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="64a44-424">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="64a44-425">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="64a44-426">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="64a44-427">**이름 또는 메일 주소로 검색** 검색 상자에 할당하려는 그룹의 **전체 그룹 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="64a44-428">목록의 **그룹** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="64a44-429">그룹의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="64a44-430">**선택 사항:** **둘 이상의 그룹을 추가**하려는 경우 **이름 또는 메일 주소로 검색** 검색 상자에 다른 **전체 그룹 이름**을 입력하고 확인란을 클릭하여 이 그룹을 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="64a44-431">그룹 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="64a44-432">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 그룹에 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="64a44-433">**할당** 단추를 클릭하여 선택한 그룹에 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="64a44-434">짧은 시간 후에 선택한 사용자는 액세스 패널에서 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="64a44-435">사용자가 라이선스에 할당된 그룹에 속해 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="64a44-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="64a44-436">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="64a44-437">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-438">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-439">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="64a44-440">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-440">click **All users**.</span></span>

6.  <span data-ttu-id="64a44-441">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="64a44-442">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-442">click **Groups**.</span></span>

8.  <span data-ttu-id="64a44-443">특정 그룹의 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="64a44-444">**라이선스**를 클릭하여 그룹이 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="64a44-445">그룹이 Office 라이선스에 할당된 경우 사용자의 액세스 패널에 나타나도록 특정 자사 Office 응용 프로그램을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="64a44-446">그룹에 라이선스를 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="64a44-446">How to assign a license to a group</span></span>

<span data-ttu-id="64a44-447">그룹에 라이선스를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="64a44-448">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="64a44-449">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="64a44-450">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="64a44-451">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="64a44-452">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-452">click **All groups**.</span></span>

6.  <span data-ttu-id="64a44-453">관심이 있는 그룹을 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="64a44-454">**라이선스**를 클릭하여 그룹이 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="64a44-455">**할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="64a44-456">사용 가능한 제품 목록에서 **하나 이상의 제품**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="64a44-457">**선택 사항** 제품을 상세하게 할당하려면 **할당 옵션** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="64a44-458">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="64a44-459">**할당** 단추를 클릭하여 이러한 라이선스를 이 그룹에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="64a44-460">그룹의 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="64a44-461">시간을 단축하려면 일시적으로 라이선스를 사용자에게 직접 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64a44-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="64a44-462">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64a44-462">Next steps</span></span>
[<span data-ttu-id="64a44-463">Azure Active Directory에 새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="64a44-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

