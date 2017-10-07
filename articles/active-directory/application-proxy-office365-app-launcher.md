---
title: "Azure AD 응용 프로그램 프록시를 사용 하 여 게시 된 앱에 대 한 사용자 지정 홈 페이지 aaaSet | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항 설명"
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
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="16843-103">Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 사용자 지정 홈 페이지 설정</span><span class="sxs-lookup"><span data-stu-id="16843-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="16843-104">이 문서에서는 어떻게 tooconfigure 앱 toodirect 사용자 tooa 사용자 지정 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="16843-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="16843-105">응용 프로그램 프록시 응용 프로그램을 게시할 때 내부 URL을 설정 하면 사용할 수 있지만 때로는 hello 페이지를 사용자가 먼저 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16843-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="16843-106">사용자가 Azure Active Directory 액세스 패널 hello 또는 hello Office 365 앱 시작 관리자에서 hello 앱에 액세스할 때 toohello 오른쪽 페이지 이동 되도록 사용자 지정 홈 페이지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="16843-107">Hello 앱을 시작 하는 사용자가 hello 게시 된 앱에 대 한 기본 toohello 루트 도메인 URL로 이동 하는.</span><span class="sxs-lookup"><span data-stu-id="16843-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="16843-108">hello 방문 페이지는 일반적으로 hello 홈 페이지 URL로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16843-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="16843-109">Hello Azure AD PowerShell 모듈 toodefine 사용자 지정 홈 페이지 Url을 사용 하 여 hello 앱 내에서 특정 페이지에 응용 프로그램 사용자 tooland 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="16843-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="16843-110">예:</span><span class="sxs-lookup"><span data-stu-id="16843-110">For example:</span></span>
- <span data-ttu-id="16843-111">회사 네트워크 내 사용자가 이동 너무*https://ExpenseApp/login/login.aspx* toosign에 응용 프로그램에 액세스 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16843-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="16843-112">Hello 앱을 게시 하는 응용 프로그램 프록시 tooaccess hello 폴더 구조의 최상위 hello에 필요한 이미지와 같은 다른 자산을 가지기 때문에 *https://ExpenseApp* 내부 URL hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="16843-113">기본 외부 URL은 hello *https://ExpenseApp-contoso.msappproxy.net*, 페이지에서 사용자가 toohello 기호를 사용 하지 않습니다입니다.</span><span class="sxs-lookup"><span data-stu-id="16843-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="16843-114">설정 *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* 사용자가 홈 페이지 URL toogive hello으로 원활 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="16843-115">Hello 앱 hello에 표시 됩니다 toopublished 앱 사용자가 액세스를 부여 하면 [Azure AD 액세스 패널](active-directory-saas-access-panel-introduction.md) 및 hello [Office 365 앱 시작 관리자](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher)합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="16843-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="16843-116">Before you start</span></span>

<span data-ttu-id="16843-117">Hello 홈 페이지 URL을 설정 하기 전에 염두 hello 요구 사항에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="16843-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="16843-118">사용자가 지정한 해당 hello 경로 hello 루트 도메인 URL의 하위 도메인 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="16843-119">Hello 루트 도메인 URL이 인 경우 예를 들어 https://apps.contoso.com/app1/, 구성 하는 hello 홈 페이지 URL 이니셜라이저에서 https://apps.contoso.com/app1/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="16843-120">변경 하는 경우 toohello 앱 게시, hello 변경 hello 홈 페이지 URL의 hello 값을 다시 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16843-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="16843-121">향후 hello에서 hello 응용 프로그램을 업데이트할 때 다시 검사를, 필요한 경우 hello 홈 페이지 URL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="16843-122">Hello Azure 포털에서에서 변경 hello 홈 페이지</span><span class="sxs-lookup"><span data-stu-id="16843-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="16843-123">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="16843-124">너무 이동**Azure Active Directory** > **앱 등록** hello 목록에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="16843-125">선택 **속성** hello 설정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="16843-126">업데이트 hello **홈 페이지 URL** 새 경로 있는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="16843-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![새 홈페이지 URL 제공](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="16843-128">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="16843-129">PowerShell과 함께 변경 hello 홈 페이지</span><span class="sxs-lookup"><span data-stu-id="16843-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="16843-130">Hello Azure AD PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="16843-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="16843-131">PowerShell을 사용 하 여 사용자 지정 홈 페이지 URL을 정의 하기 전에 hello Azure AD PowerShell 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="16843-132">Hello에서 hello 패키지를 다운로드할 수 있습니다 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131)는, 사용 하 여 hello Graph API 끝점.</span><span class="sxs-lookup"><span data-stu-id="16843-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="16843-133">tooinstall hello 패키지에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="16843-134">표준 PowerShell 창을 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="16843-135">Hello를 사용 하 여 hello 명령 비관리자를 실행 하는 경우 `-scope currentuser` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="16843-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="16843-136">Hello 설치 하는 동안 선택 **Y** tooinstall 두 Nuget.org를 패키지 합니다. 두 개의 패키지가 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="16843-137">Hello hello 응용 프로그램의 개체 Id</span><span class="sxs-lookup"><span data-stu-id="16843-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="16843-138">Hello hello 응용 프로그램의 개체 Id를 받으며 hello 앱에 대 한 홈 페이지에서 다음 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="16843-139">PowerShell을 열고 hello Azure AD 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="16843-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="16843-140">테 넌 트 관리자에 게로 Azure AD 모듈 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="16843-141">홈 페이지 URL에 따라 hello 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="16843-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="16843-142">너무 이동 하 여 hello URL hello 포털에서 찾을 수 있습니다**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="16843-143">이 예제에서는 *sharepoint-iddemo*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="16843-144">여기에 표시 된 하나 비슷한 toohello 않는 결과 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="16843-145">Hello ObjectID GUID toouse hello 다음 섹션에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="16843-146">업데이트 hello 홈 페이지 URL</span><span class="sxs-lookup"><span data-stu-id="16843-146">Update hello home page URL</span></span>

<span data-ttu-id="16843-147">Hello에서 1 단계에 사용한 동일한 PowerShell 모듈 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="16843-148">응용 프로그램, 수정 및 바꾸기 hello 있는지 확인 *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* hello hello 앞 단계에서에서 복사한 ObjectID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="16843-149">Hello 앱을 확인 한 했으므로 준비 tooupdate hello 홈 페이지에서 다음과 같이 것입니다.</span><span class="sxs-lookup"><span data-stu-id="16843-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="16843-150">새 응용 프로그램 개체 toohold toomake hello 변경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16843-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="16843-151">이 변수는 tooupdate hello 값을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="16843-152">이 단계에서는 아무 것도 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16843-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="16843-153">Hello 홈 페이지 URL toohello 원하는 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="16843-154">hello 값 hello 게시 된 앱의 하위 경로 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="16843-155">예를 들어 변경 하는 경우 홈 페이지 URL에서 hello *https://sharepoint-iddemo.msappproxy.net/* 너무*https://sharepoint-iddemo.msappproxy.net/hybrid/*, 앱 사용자가 직접 전환 toohello 사용자 지정 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="16843-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="16843-156">복사한 GUID (ObjectID) hello를 사용 하 여 업데이트를 hello 확인 "1 단계: 찾기 hello hello 응용 프로그램의 개체 Id입니다."</span><span class="sxs-lookup"><span data-stu-id="16843-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="16843-157">hello 변경 성공적으로 수행 되었는지 tooconfirm hello 앱을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="16843-158">Toohello 앱 수행한 변경 내용 hello 홈 페이지 URL을 재설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16843-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="16843-159">홈페이지 URL이 다시 설정되면 2단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="16843-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16843-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16843-160">Next steps</span></span>

- [<span data-ttu-id="16843-161">원격 액세스 tooSharePoint Azure AD 응용 프로그램 프록시를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="16843-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="16843-162">Hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="16843-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
