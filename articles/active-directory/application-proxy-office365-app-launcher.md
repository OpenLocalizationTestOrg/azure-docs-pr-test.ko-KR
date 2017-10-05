---
title: "Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 사용자 지정 홈 페이지 설정 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대한 기본 사항 제공"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="14e18-103">Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 사용자 지정 홈 페이지 설정</span><span class="sxs-lookup"><span data-stu-id="14e18-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="14e18-104">이 문서에서는 사용자를 사용자 지정 홈 페이지에 연결하도록 앱을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="14e18-105">응용 프로그램 프록시를 사용하여 응용 프로그램을 게시할 때 내부 URL을 설정하지만 사용자가 처음 보게 되는 페이지는 설정하지 않는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="14e18-106">Azure Active Directory 액세스 패널 또는 Office 365 앱 시작 관리자에서 사용자가 앱에 액세스할 때 오른쪽 페이지로 이동하도록 사용자 지정 홈 페이지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="14e18-107">사용자가 앱을 시작하면 기본적으로 게시된 앱의 루트 도메인 URL로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="14e18-108">방문 페이지는 일반적으로 홈페이지 URL로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="14e18-109">앱 사용자가 앱 내의 특정 페이지를 방문하게 하려는 경우 Azure AD PowerShell 모듈을 사용하여 사용자 지정 홈 페이지 URL을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="14e18-110">예:</span><span class="sxs-lookup"><span data-stu-id="14e18-110">For example:</span></span>
- <span data-ttu-id="14e18-111">회사 네트워크 내부에서 사용자는 *https://ExpenseApp/login/login.aspx*로 이동하여 로그인하고 앱에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="14e18-112">응용 프로그램 프록시가 폴더 구조의 최상위 수준에서 액세스해야 하는 이미지와 같은 기타 자산이 있으므로 앱을 *https://ExpenseApp*을 사용해서 내부 URL로 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="14e18-113">기본 외부 URL은 *https://ExpenseApp-contoso.msappproxy.net*입니다. 이 URL은 사용자를 로그인 페이지로 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="14e18-114">*https://ExpenseApp-contoso.msappproxy.net/login/login.aspx*를 홈페이지 URL로 설정하면 사용자에게 원활한 환경을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="14e18-115">사용자에게 게시된 응용 프로그램에 대한 액세스 권한을 제공하면 [Azure AD 액세스 패널](active-directory-saas-access-panel-introduction.md) 및 [Office 365 앱 시작 관리자](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher)에 앱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="14e18-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="14e18-116">Before you start</span></span>

<span data-ttu-id="14e18-117">홈페이지 URL을 설정하기 전에 다음 요구 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="14e18-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="14e18-118">사용자가 지정한 경로가 루트 도메인 URL의 하위 도메인 경로인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="14e18-119">예를 들어, 루트 도메인 URL이 https://apps.contoso.com/app1/이면 구성한 홈페이지 URL은 https://apps.contoso.com/app1/로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="14e18-120">게시된 앱을 변경하는 경우 이로 인해 홈페이지 URL 값을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="14e18-121">나중에 앱을 업데이트할 경우 홈페이지 URL을 다시 확인하고 필요한 경우 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="14e18-122">Azure Portal에서 홈페이지 변경</span><span class="sxs-lookup"><span data-stu-id="14e18-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="14e18-123">관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="14e18-124">**Azure Active Directory** > **앱 등록**으로 이동한 후 목록에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="14e18-125">설정에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="14e18-126">**홈페이지 URL** 필드를 새 경로로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-126">Update the **Home page URL** field with your new path.</span></span> 

   ![새 홈페이지 URL 제공](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="14e18-128">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="14e18-129">PowerShell을 사용하여 홈페이지 변경</span><span class="sxs-lookup"><span data-stu-id="14e18-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="14e18-130">Azure AD PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="14e18-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="14e18-131">PowerShell을 사용하여 사용자 지정 홈페이지 URL을 정의하기 전에 Azure AD PowerShell 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="14e18-132">Graph API 끝점을 사용하는 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131)에서 패키지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="14e18-133">패키지를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="14e18-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="14e18-134">표준 PowerShell 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="14e18-135">관리자가 아닌 사용자로 명령을 실행하는 경우 `-scope currentuser` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="14e18-136">설치 도중 Nuget.org에서 두 개의 패키지를 설치하려면 **Y**를 선택합니다. 두 개의 패키지가 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="14e18-137">앱의 ObjectID 찾기</span><span class="sxs-lookup"><span data-stu-id="14e18-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="14e18-138">앱의 ObjectID를 받은 다음 해당 홈 페이지에서 앱을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="14e18-139">PowerShell을 열고 Azure AD 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="14e18-140">테넌트 관리자로 Azure AD 모듈에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="14e18-141">홈페이지 URL을 기준으로 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="14e18-142">**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**으로 이동하여 포털에서 URL을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="14e18-143">이 예제에서는 *sharepoint-iddemo*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="14e18-144">여기에 표시된 것과 비슷한 결과가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="14e18-145">다음 섹션에서 사용할 ObjectID GUID를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="14e18-146">홈페이지 URL 업데이트</span><span class="sxs-lookup"><span data-stu-id="14e18-146">Update the home page URL</span></span>

<span data-ttu-id="14e18-147">1단계에서 사용한 것과 동일한 PowerShell 모듈에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="14e18-148">맞는 앱이 있는지 확인하고 *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4*를 앞의 단계에서 복사한 ObjectID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="14e18-149">이제 앱을 확인했으므로 다음과 같이 홈 페이지를 업데이트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="14e18-150">변경 내용을 저장하기 위해 비어 있는 응용 프로그램 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="14e18-151">이 변수는 업데이트하려는 값을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="14e18-152">이 단계에서는 아무 것도 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="14e18-153">홈페이지 URL을 원하는 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="14e18-154">값은 게시된 앱의 하위 도메인 경로여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="14e18-155">예를 들어, 홈페이지 URL을 *https://sharepoint-iddemo.msappproxy.net/*에서 *https://sharepoint-iddemo.msappproxy.net/hybrid/*로 변경하는 경우 앱 사용자는 사용자 지정 홈페이지로 직접 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="14e18-156">"1단계: 앱의 ObjectID 찾기"에서 복사한 GUID(ObjectID)를 사용하여 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="14e18-157">변경 내용이 성공했는지를 확인하려면 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="14e18-158">앱에 대한 변경 내용으로 인해 홈페이지 URL을 다시 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="14e18-159">홈페이지 URL이 다시 설정되면 2단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="14e18-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14e18-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14e18-160">Next steps</span></span>

- [<span data-ttu-id="14e18-161">Azure AD 응용 프로그램 프록시를 사용하여 SharePoint에 원격 액세스 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="14e18-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="14e18-162">Azure Portal에서 응용 프로그램 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="14e18-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
