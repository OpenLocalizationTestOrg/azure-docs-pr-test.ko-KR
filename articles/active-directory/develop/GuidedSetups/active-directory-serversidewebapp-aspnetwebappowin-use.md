---
title: "AD aaaAzure v2 ASP.NET 웹 서버 시작-사용 | Microsoft Docs"
description: "OpenID Connect 표준을 사용하여 기존 웹 브라우저 기반 응용 프로그램을 사용하는 ASP.NET 솔루션에서 Microsoft 로그인 구현"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a><span data-ttu-id="6efde-103">컨트롤러 toohandle 로그인 및 로그 아웃 요청 추가</span><span class="sxs-lookup"><span data-stu-id="6efde-103">Add a controller toohandle sign-in and sign-out requests</span></span>

<span data-ttu-id="6efde-104">이 단계 표시 방법을 toocreate 새 컨트롤러 tooexpose 로그인 및 로그 아웃 메서드.</span><span class="sxs-lookup"><span data-stu-id="6efde-104">This step shows how toocreate a new controller tooexpose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="6efde-105">마우스 오른쪽 단추로 클릭 하 여 hello `Controllers` 폴더 및 선택`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="6efde-105">Right click hello `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="6efde-106">`MVC (.NET version) Controller – Empty`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="6efde-107">*추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-107">Click *Add*</span></span>
4.  <span data-ttu-id="6efde-108">이름을 `HomeController`로 지정하고 *추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="6efde-109">추가 *OWIN* toohello 클래스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-109">Add *OWIN* references toohello class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="6efde-110">코드를 통해 인증 챌린지를 시작 하 여 toohandle 로그인 및 로그 아웃 tooyour 컨트롤러 아래 hello 두 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-110">Add hello two methods below toohandle sign-in and sign-out tooyour controller by initiating an authentication challenge via code:</span></span>
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a><span data-ttu-id="6efde-111">사용자가 로그인 단추를 통해 hello 응용 프로그램의 홈 페이지 toosign 만들기</span><span class="sxs-lookup"><span data-stu-id="6efde-111">Create hello app's home page toosign in users via a sign-in button</span></span>

<span data-ttu-id="6efde-112">Visual Studio에서 새 보기 tooadd hello 로그인 단추를 만들고 인증 후 사용자 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-112">In Visual Studio, create a new view tooadd hello sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="6efde-113">마우스 오른쪽 단추로 클릭 하 여 hello `Views\Home` 폴더 및 선택`Add View`</span><span class="sxs-lookup"><span data-stu-id="6efde-113">Right click hello `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="6efde-114">이름을 `Index`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="6efde-115">다음 로그인 단추 hello를 toohello 파일을 포함 하는 HTML hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-115">Add hello following HTML, which includes hello sign-in button, toohello file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="6efde-116">추가 정보</span><span class="sxs-lookup"><span data-stu-id="6efde-116">More Information</span></span>
> <span data-ttu-id="6efde-117">이 페이지는 SVG 형식으로 검은색 배경의 로그인 단추를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="6efde-118">![Microsoft로 로그인](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="6efde-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="6efde-119">더 많은 로그인 단추를 toohello를 방문 하십시오 [이 페이지](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "브랜딩 지침")합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-119">For more sign-in buttons, please go toohello [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a><span data-ttu-id="6efde-120">컨트롤러 toodisplay 사용자 클레임 추가</span><span class="sxs-lookup"><span data-stu-id="6efde-120">Add a controller toodisplay user's claims</span></span>
<span data-ttu-id="6efde-121">이 컨트롤러의 hello hello를 사용 하는 방법을 보여 줍니다 `[Authorize]` tooprotect는 컨트롤러 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-121">This controller demonstrates hello uses of hello `[Authorize]` attribute tooprotect a controller.</span></span> <span data-ttu-id="6efde-122">이 특성은 인증 된 사용자만 허용 하 여 액세스 toohello 컨트롤러를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-122">This attribute restricts access toohello controller by only allowing authenticated users.</span></span> <span data-ttu-id="6efde-123">아래 코드 hello hello에 대 한 로그인의 일부로 검색 된 hello 특성 toodisplay 사용자 클레임 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-123">hello code below makes use of hello attribute toodisplay user claims that were retrieved as part of hello sign-in.</span></span>

1.  <span data-ttu-id="6efde-124">마우스 오른쪽 단추로 클릭 하 여 hello `Controllers` 폴더:`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="6efde-124">Right click hello `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="6efde-125">`MVC {version} Controller – Empty`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="6efde-126">*추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-126">Click *Add*</span></span>
4.  <span data-ttu-id="6efde-127">이름을 `ClaimsController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="6efde-128">Hello 코드 대체 hello 아래-hello 코드로 컨트롤러 클래스의 추가 `[Authorize]` 특성 toohello 클래스:</span><span class="sxs-lookup"><span data-stu-id="6efde-128">Replace hello code of your controller class with hello code below - this adds hello `[Authorize]` attribute toohello class:</span></span>

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="6efde-129">추가 정보</span><span class="sxs-lookup"><span data-stu-id="6efde-129">More Information</span></span>
> <span data-ttu-id="6efde-130">Hello hello 사용량이 `[Authorize]` hello 사용자가 인증 하는 경우에 특성을이 컨트롤러의 모든 메서드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-130">Because of hello use of hello `[Authorize]` attribute, all methods of this controller can only be executed if hello user is authenticated.</span></span> <span data-ttu-id="6efde-131">Hello 사용자가 인증 되지 않은 tooaccess hello 컨트롤러 시도 하는 경우 OWIN 인증 챌린지 시작 되 고 hello 사용자 tooauthenticate 강제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-131">If hello user is not authenticated and tries tooaccess hello controller, OWIN will initiate an authentication challenge and force hello user tooauthenticate.</span></span> <span data-ttu-id="6efde-132">클레임의 hello 컬렉션을 보고가 hello 위의 hello 코드 `ClaimsPrincipal.Current` hello 사용자의 토큰에 포함 된 특정 사용자 특성에 대 한 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="6efde-132">hello code above looks at hello claims collection of hello `ClaimsPrincipal.Current` instance for specific user attributes included in hello user’s token.</span></span> <span data-ttu-id="6efde-133">이러한 특성에는 hello 글로벌 사용자 식별자 주체 뿐만 아니라 hello 사용자의 전체 이름 및 사용자 이름, 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-133">These attributes include hello user’s full name and username, as well as hello global user identifier subject.</span></span> <span data-ttu-id="6efde-134">Hello 포함 되어 *테 넌 트 ID*, hello 사용자의 조직에 대 한 hello ID을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-134">It also contains hello *Tenant ID*, which represents hello ID for hello user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a><span data-ttu-id="6efde-135">보기 toodisplay hello 사용자의 클레임 만들기</span><span class="sxs-lookup"><span data-stu-id="6efde-135">Create a view toodisplay hello user's claims</span></span>

<span data-ttu-id="6efde-136">Visual Studio에서 새 뷰를 웹 페이지에 toodisplay hello 사용자의 클레임 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-136">In Visual Studio, create a new view toodisplay hello user's claims in a web page:</span></span>

1.  <span data-ttu-id="6efde-137">마우스 오른쪽 단추로 클릭 하 여 hello `Views\Claims` 폴더 및:`Add View`</span><span class="sxs-lookup"><span data-stu-id="6efde-137">Right click hello `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="6efde-138">이름을 `Index`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="6efde-139">다음 HTML toohello 파일 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6efde-139">Add hello following HTML toohello file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
