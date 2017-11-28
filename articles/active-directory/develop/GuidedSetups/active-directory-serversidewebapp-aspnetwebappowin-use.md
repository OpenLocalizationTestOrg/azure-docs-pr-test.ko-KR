---
title: "Azure AD v2 ASP.NET 웹 서버 시작 - 사용 | Microsoft Docs"
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
ms.openlocfilehash: 3b7d29e48c91f40e8782a5e32a52998b815fe331
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="add-a-controller-to-handle-sign-in-and-sign-out-requests"></a><span data-ttu-id="51d21-103">로그인 및 로그아웃 요청을 처리하는 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="51d21-103">Add a controller to handle sign-in and sign-out requests</span></span>

<span data-ttu-id="51d21-104">이 단계에서는 로그인 및 로그아웃 메서드를 노출하는 새 컨트롤러를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-104">This step shows how to create a new controller to expose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="51d21-105">`Controllers` 폴더를 마우스 오른쪽 단추로 클릭하고 `Add` > `Controller`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-105">Right click the `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="51d21-106">`MVC (.NET version) Controller – Empty`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="51d21-107">*추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-107">Click *Add*</span></span>
4.  <span data-ttu-id="51d21-108">이름을 `HomeController`로 지정하고 *추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="51d21-109">클래스에 *OWIN* 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-109">Add *OWIN* references to the class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="51d21-110">코드를 통해 인증 질문을 시작하여 로그인 및 로그아웃을 처리하는 아래의 두 메서드를 컨트롤러에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-110">Add the two methods below to handle sign-in and sign-out to your controller by initiating an authentication challenge via code:</span></span>
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate the SignIn method with the [Authorize] attribute
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

## <a name="create-the-apps-home-page-to-sign-in-users-via-a-sign-in-button"></a><span data-ttu-id="51d21-111">로그인 단추를 통해 사용자를 로그인하는 앱의 홈페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="51d21-111">Create the app's home page to sign in users via a sign-in button</span></span>

<span data-ttu-id="51d21-112">Visual Studio에서 로그인 단추를 추가하고 인증 후 사용자 정보를 표시하는 새 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-112">In Visual Studio, create a new view to add the sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="51d21-113">`Views\Home` 폴더를 마우스 오른쪽 단추로 클릭하고 `Add View`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-113">Right click the `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="51d21-114">이름을 `Index`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="51d21-115">로그인 단추를 포함하는 다음 HTML을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-115">Add the following HTML, which includes the sign-in button, to the file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If the user is not authenticated, display the sign-in button -->
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
### <a name="more-information"></a><span data-ttu-id="51d21-116">추가 정보</span><span class="sxs-lookup"><span data-stu-id="51d21-116">More Information</span></span>
> <span data-ttu-id="51d21-117">이 페이지는 SVG 형식으로 검은색 배경의 로그인 단추를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="51d21-118">![Microsoft로 로그인](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="51d21-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="51d21-119">추가 로그인 단추는 [이 페이지](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines")를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d21-119">For more sign-in buttons, please go to the [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-to-display-users-claims"></a><span data-ttu-id="51d21-120">사용자의 클레임을 표시하는 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="51d21-120">Add a controller to display user's claims</span></span>
<span data-ttu-id="51d21-121">이 컨트롤러는 컨트롤러를 보호하는 `[Authorize]` 특성의 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-121">This controller demonstrates the uses of the `[Authorize]` attribute to protect a controller.</span></span> <span data-ttu-id="51d21-122">이 특성은 인증된 사용자만 허용하여 컨트롤러에 대한 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-122">This attribute restricts access to the controller by only allowing authenticated users.</span></span> <span data-ttu-id="51d21-123">아래 코드에서는 이 특성을 활용하여 로그인의 일부로 검색된 사용자 클레임을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-123">The code below makes use of the attribute to display user claims that were retrieved as part of the sign-in.</span></span>

1.  <span data-ttu-id="51d21-124">`Controllers` 폴더를 마우스 오른쪽 단추로 클릭하고 `Add` > `Controller`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-124">Right click the `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="51d21-125">`MVC {version} Controller – Empty`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="51d21-126">*추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-126">Click *Add*</span></span>
4.  <span data-ttu-id="51d21-127">이름을 `ClaimsController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="51d21-128">컨트롤러 클래스의 코드를 아래 코드로 바꿉니다. 그러면 클래스에 `[Authorize]` 특성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-128">Replace the code of your controller class with the code below - this adds the `[Authorize]` attribute to the class:</span></span>

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims to viewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get the user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // The 'preferred_username' claim can be used for showing the username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // The subject claim can be used to uniquely identify the user across the web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is the unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="51d21-129">추가 정보</span><span class="sxs-lookup"><span data-stu-id="51d21-129">More Information</span></span>
> <span data-ttu-id="51d21-130">`[Authorize]` 특성을 사용하므로 이 컨트롤러의 모든 메서드는 사용자가 인증된 경우에만 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-130">Because of the use of the `[Authorize]` attribute, all methods of this controller can only be executed if the user is authenticated.</span></span> <span data-ttu-id="51d21-131">사용자가 인증되지 않은 경우 컨트롤러에 액세스하려고 하면 OWIN에서 인증 질문을 시작하고 사용자가 강제로 인증하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-131">If the user is not authenticated and tries to access the controller, OWIN will initiate an authentication challenge and force the user to authenticate.</span></span> <span data-ttu-id="51d21-132">위 코드에서는 사용자의 토큰에 포함된 특정 사용자 특성에 대해 `ClaimsPrincipal.Current` 인스턴스의 클레임 컬렉션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-132">The code above looks at the claims collection of the `ClaimsPrincipal.Current` instance for specific user attributes included in the user’s token.</span></span> <span data-ttu-id="51d21-133">이러한 특성에는 사용자의 전체 이름과 사용자 이름 및 전역 사용자 식별자 주체가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-133">These attributes include the user’s full name and username, as well as the global user identifier subject.</span></span> <span data-ttu-id="51d21-134">사용자의 조직에 대한 ID를 나타내는 *테넌트 ID*도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-134">It also contains the *Tenant ID*, which represents the ID for the user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-to-display-the-users-claims"></a><span data-ttu-id="51d21-135">사용자의 클레임을 표시하는 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="51d21-135">Create a view to display the user's claims</span></span>

<span data-ttu-id="51d21-136">Visual Studio에서 새 보기를 만들어 사용자의 클레임을 웹 페이지에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-136">In Visual Studio, create a new view to display the user's claims in a web page:</span></span>

1.  <span data-ttu-id="51d21-137">`Views\Claims` 폴더를 마우스 오른쪽 단추로 클릭하고 `Add View`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-137">Right click the `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="51d21-138">이름을 `Index`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="51d21-139">다음 HTML을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d21-139">Add the following HTML to the file:</span></span>

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
