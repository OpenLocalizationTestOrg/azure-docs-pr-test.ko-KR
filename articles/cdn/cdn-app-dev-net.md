---
title: ".NET 용 Azure CDN 라이브러리 hello 시작 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toowrite.NET 응용 프로그램 toomanage Visual Studio를 사용 하 여 Azure CDN 합니다."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="e5f62-103">Azure CDN 개발 시작</span><span class="sxs-lookup"><span data-stu-id="e5f62-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5f62-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e5f62-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="e5f62-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e5f62-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="e5f62-106">Hello를 사용할 수 있습니다 [.NET 용 Azure CDN 라이브러리](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate CDN 프로필 및 끝점의 생성 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="e5f62-107">이 자습서는 몇몇 hello 사용할 수 있는 작업을 보여 주는 간단한.NET 콘솔 응용 프로그램의 hello 만들기를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="e5f62-108">이 자습서가 만들어지지 toodescribe hello Azure CDN 라이브러리의 모든 측면.NET에 대 한 자세히 설명에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="e5f62-109">이 자습서에서는 Visual Studio 2015 toocomplete 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="e5f62-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 는 무료로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="e5f62-111">hello [이 자습서에서 완성 된 프로젝트](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) MSDN에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="e5f62-112">프로젝트 만들기 및 Nuget 패키지 추가하기</span><span class="sxs-lookup"><span data-stu-id="e5f62-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="e5f62-113">우리의 CDN 프로필에 대 한 리소스 그룹을 만들고이 Azure AD 응용 프로그램 사용 권한 toomanage CDN 프로필 및 해당 그룹 내에서 끝점을 지정 했 म, 했으므로 응용 프로그램을 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="e5f62-114">Visual Studio 2015 내에서 클릭 **파일**, **새로**, **프로젝트...**  tooopen hello 새 프로젝트 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e5f62-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="e5f62-115">확장 **Visual C#**을 선택한 후 **Windows** hello hello 왼쪽 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="e5f62-116">클릭 **콘솔 응용 프로그램** hello 가운데 창에서.</span><span class="sxs-lookup"><span data-stu-id="e5f62-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="e5f62-117">프로젝트 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-117">Name your project, then click **OK**.</span></span>  

![새 프로젝트](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="e5f62-119">이 프로젝트는 toouse 일부 Azure 라이브러리 Nuget 패키지에 포함 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="e5f62-120">이러한 toohello 프로젝트를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="e5f62-121">Hello 클릭 **도구** 메뉴 **Nuget 패키지 관리자**, 다음 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Nuget 패키지 관리](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="e5f62-123">Hello 패키지 관리자 콘솔에서에서 실행 하 여 다음 명령 tooinstall hello hello **Active Directory 인증 라이브러리 (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="e5f62-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="e5f62-124">Hello tooinstall hello 다음 실행 **Azure CDN 관리 라이브러리**:</span><span class="sxs-lookup"><span data-stu-id="e5f62-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="e5f62-125">지시문, 상수, 메인 메서드 및 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="e5f62-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="e5f62-126">Hello 작성이 프로그램의 기본 구조를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="e5f62-127">Hello Program.cs 탭에서 다시 hello 대체 `using` hello 다음과 같이 hello 위쪽 지시문:</span><span class="sxs-lookup"><span data-stu-id="e5f62-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. <span data-ttu-id="e5f62-128">이 메서드는 사용 하 여 일부 상수 toodefine 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="e5f62-129">Hello에 `Program` 클래스 전에 hello `Main` 메서드를 hello 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="e5f62-130">수 있는지 tooreplace hello를 포함 하 여 hello 자리 표시자  **&lt;꺾쇠 괄호&gt;**, 필요에 따라 고유한 값으로.</span><span class="sxs-lookup"><span data-stu-id="e5f62-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="e5f62-131">또한 hello 클래스 수준에서 이러한 두 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="e5f62-132">이러한 이후 toodetermine 우리의 프로필 및 끝점 이미 있는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="e5f62-133">Hello 대체 `Main` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-133">Replace hello `Main` method as follows:</span></span>
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="e5f62-134">일부 다른 메서드는 질문을 "Yes/No" tooprompt hello 사용자를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="e5f62-135">다음 메서드 toomake hello를 추가 하는 좀 더 쉽게:</span><span class="sxs-lookup"><span data-stu-id="e5f62-135">Add hello following method toomake that a little easier:</span></span>
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

<span data-ttu-id="e5f62-136">Hello 호출 하는 hello 메서드를 만들어야 했습니다를 hello이 프로그램의 기본 구조를 작성 했으므로 `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e5f62-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="e5f62-137">인증</span><span class="sxs-lookup"><span data-stu-id="e5f62-137">Authentication</span></span>
<span data-ttu-id="e5f62-138">Hello Azure CDN 관리 라이브러리를 사용할 수 있습니다, tooauthenticate 서비스 보안 주체 및 필요 인증 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="e5f62-139">이 메서드는 ADAL tooretrieve hello 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-139">This method uses ADAL tooretrieve hello token.</span></span>

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

<span data-ttu-id="e5f62-140">개별 사용자 인증을 사용 하는 경우 hello `GetAccessToken` 메서드 약간 다르게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5f62-141">서비스 사용자 대신 toohave 개별 사용자 인증을 선택 하는 경우에이 코드 예제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

<span data-ttu-id="e5f62-142">수 있는지 tooreplace `<redirect URI>` hello를 사용 하 여 Azure AD에서 hello 응용 프로그램을 등록할 때 입력 한 URI를 리디렉션할 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="e5f62-143">CDN 프로필 및 끝점 목록화하기</span><span class="sxs-lookup"><span data-stu-id="e5f62-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="e5f62-144">이제 우리 준비 tooperform CDN 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="e5f62-145">hello이 메서드는 먼저 모든 hello 프로필 및이 리소스 그룹에는 끝점은 목록 해지고 우리의 상수에 지정 된 hello 프로필 및 끝점 이름에 대 한 일치 하는 항목이 발견 되 면을 기록 하는 나중에 되었으므로 toocreate 중복 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="e5f62-146">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="e5f62-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="e5f62-147">다음으로 프로필을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-147">Next, we'll create a profile.</span></span>

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

<span data-ttu-id="e5f62-148">Hello 프로필을 만든 후 끝점을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-148">Once hello profile is created, we'll create an endpoint.</span></span>

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> <span data-ttu-id="e5f62-149">위의 예제에서는 hello 라는 origin hello 끝점에 할당 *Contoso* 호스트 이름에 `www.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="e5f62-150">이 toopoint tooyour 고유의 원본의 호스트이 이름을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="e5f62-151">끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="e5f62-151">Purge an endpoint</span></span>
<span data-ttu-id="e5f62-152">Hello 끝점이 만들어졌으며 라고 가정할 경우 일반적인 작업 tooperform 프로그램에서 원하는 수 있는지는 제거 우리의 끝점의 hello 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> <span data-ttu-id="e5f62-153">위의 hello 예제에서 문자열 hello `/*` 원하는 toopurge hello hello 끝점 경로의 루트에 있는 모든 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="e5f62-154">이 해당 toochecking **모든 제거** hello에 Azure 포털의 "제거" 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e5f62-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="e5f62-155">Hello에 `CreateCdnProfile` 우리의 프로필을 만든 메서드를 한 **Verizon에서 Azure CDN** hello 코드를 사용 하 여 프로필 `Sku = new Sku(SkuName.StandardVerizon)`이므로이 성공적으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="e5f62-156">그러나 **Akamai에서 Azure CDN** 프로필을 지원 하지 않는 **모든 제거**이므로 Akamai 프로필을 사용 하 여이 자습서에 대 한가 I, tooinclude 특정 경로 toopurge 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="e5f62-157">CDN 프로필 및 끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="e5f62-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="e5f62-158">hello 마지막 메서드는이 끝점 및 프로필 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-158">hello last methods will delete our endpoint and profile.</span></span>

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a><span data-ttu-id="e5f62-159">Hello 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e5f62-159">Running hello program</span></span>
<span data-ttu-id="e5f62-160">컴파일 및 hello를 클릭 하 여 hello 프로그램을 실행 합니다. 이제 우리 **시작** Visual Studio에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![프로그램 실행](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="e5f62-162">Hello 프로그램 프롬프트 위에 hello에 도달 하면 hello Azure 포털에서에서 수 tooreturn tooyour 리소스 그룹 이어야 하 고 hello 프로필 작성 되었는지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![성공!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="e5f62-164">Hello 프롬프트 toorun hello 프로그램의 나머지 부분과 hello 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![프로그램 완료](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="e5f62-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5f62-166">Next Steps</span></span>
<span data-ttu-id="e5f62-167">이 연습에서 완료 하는 hello 프로젝트 toosee [hello 샘플 다운로드](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="e5f62-168">.NET, 보기 hello에 대 한 hello Azure CDN 관리 라이브러리에 대 한 toofind 추가 설명서 [msdn 참조](https://msdn.microsoft.com/library/mt657769.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="e5f62-169">[PowerShell](cdn-manage-powershell.md)을 사용하여 CDN 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f62-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

