---
title: ".NET용 Azure CDN 라이브러리 시작하기 | Microsoft Docs"
description: "Visual Studio로 Azure CDN을 관리하는 .NET 응용 프로그램을 만드는 방법에 대해 알아보기"
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="29010-103">Azure CDN 개발 시작</span><span class="sxs-lookup"><span data-stu-id="29010-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29010-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="29010-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="29010-105">.NET</span><span class="sxs-lookup"><span data-stu-id="29010-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="29010-106">[.NET용 Azure CDN 라이브러리](https://msdn.microsoft.com/library/mt657769.aspx) 를 사용하여 CDN 프로필과 끝점의 생성 및 관리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="29010-107">이 자습서에서는 여러 가지 사용 가능한 작업을 보여주는 간단한 .NET 콘솔 응용 프로그램을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="29010-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="29010-108">이 자습서는 .NET용 Azure CDN 라이브러리의 모든 측면을 상세하게 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="29010-109">이 자습서를 완료하려면 Visual Studio 2015가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="29010-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 는 무료로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="29010-111">[이 자습서에서 완성된 프로젝트](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) 는 MSDN에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="29010-112">프로젝트 만들기 및 Nuget 패키지 추가하기</span><span class="sxs-lookup"><span data-stu-id="29010-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="29010-113">CDN 프로필용 리소스 그룹을 만들고 해당 그룹에서 CDN 프로필과 끝점을 관리하기 위한 Azure AD 응용 프로그램 권한을 부여했으므로, 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="29010-114">Visual Studio 2015를 열고 **파일**, **새로 만들기**, **프로젝트...**를 클릭하여 새 프로젝트 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29010-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="29010-115">**Visual C#**을 확장하고 왼쪽 창에서 **Windows**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="29010-116">가운데 창에서 **콘솔 응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="29010-117">프로젝트 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-117">Name your project, then click **OK**.</span></span>  

![새 프로젝트](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="29010-119">이 프로젝트에서는 Nuget 패키지에 포함된 일부 Azure 라이브러리를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29010-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="29010-120">라이브러리를 프로젝트에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="29010-121">**도구** 메뉴, **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Nuget 패키지 관리](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="29010-123">패키지 관리자 콘솔에서 다음 명령을 실행하여 **Active Directory 인증 라이브러리(ADAL)**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="29010-124">다음 명령을 실행하여 **Azure CDN 관리 라이브러리**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="29010-125">지시문, 상수, 메인 메서드 및 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="29010-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="29010-126">작성된 프로그램의 기본 구조를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="29010-127">Program.cs 탭으로 돌아와서 위에 있는 `using` 지시문을 다음으로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="29010-128">메서드가 사용할 몇 가지 상수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="29010-129">`Main` 메서드 전에 `Program` 클래스에 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="29010-130">**&lt;꺽쇠 괄호&gt;**를 포함한 자리 표시자를 필요에 따라 고유 값으로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="29010-131">또한, 클래스 수준에서 다음 두 가지 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="29010-132">이 변수는 프로필과 끝점이 이미 존재하는지 확인할 때 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29010-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="29010-133">`Main` 메서드를 다음과 같이 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="29010-134">일부 다른 메서드는 사용자에게 “Yes/No” 질문을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="29010-135">그 작업을 쉽게 수행할 수 있게 도와줄 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="29010-136">이제 프로그램의 기본 구조가 작성되었으므로 `Main` 메서드가 호출할 메서드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="29010-137">인증</span><span class="sxs-lookup"><span data-stu-id="29010-137">Authentication</span></span>
<span data-ttu-id="29010-138">Azure CDN 관리 라이브러리를 사용하기 전에 서비스 주체를 인증하고 인증 토큰을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="29010-139">이 메서드는 ADAL을 사용하여 토큰을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="29010-140">개별 사용자 인증을 사용한다면 `GetAccessToken` 메서드는 약간 다르게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="29010-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29010-141">서비스 주체가 아닌 개별 사용자 인증을 사용할 경우에만 다음 코드 샘플을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="29010-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="29010-142">`<redirect URI>` 을(를) Azure AD에서 응용 프로그램을 등록할 때 입력한 URI 리디렉션으로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="29010-143">CDN 프로필 및 끝점 목록화하기</span><span class="sxs-lookup"><span data-stu-id="29010-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="29010-144">이제 CDN 작업을 수행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="29010-145">이 메서드는 가장 먼저 리소스 그룹에서 모든 프로필과 끝점의 목록을 작성합니다. 상수에서 정의된 프로필과 끝점 이름에 일치하는 항목이 발견되면, 나중에 중복을 만들지 않도록 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="29010-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="29010-146">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="29010-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="29010-147">다음으로 프로필을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="29010-148">프로필을 만든 후에는 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29010-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="29010-149">위 예제에서는 끝점에 *Contoso*라는 원점을 할당했습니다. 호스트 이름은 `www.contoso.com`입니다.</span><span class="sxs-lookup"><span data-stu-id="29010-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="29010-150">이 값이 원래의 호스트 이름을 가리키도록 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="29010-151">끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="29010-151">Purge an endpoint</span></span>
<span data-ttu-id="29010-152">끝점을 만들었을 경우, 프로그램에서 흔히 수행하는 작업은 끝점의 콘텐츠를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29010-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="29010-153">위 예제에서 `/*` 문자열은 끝점 경로의 루트에 있는 모든 것을 삭제하겠다는 의미를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="29010-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="29010-154">이는 Azure Portal의 "제거" 대화 상자에서 **모두 제거**에 표시하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="29010-155">`CreateCdnProfile` 메서드에서는 `Sku = new Sku(SkuName.StandardVerizon)` 코드를 사용하여 **Verizon에서 Azure CDN** 프로필을 만들었으므로, 이 작업이 성공적으로 수행될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29010-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="29010-156">그러나 **Akamai에서 Azure CDN** 프로필은 **모두 삭제**를 지원하지 않습니다. 이 자습서에서 Akamai 프로필을 사용했다면 삭제할 구체적 경로가 필요했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29010-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="29010-157">CDN 프로필 및 끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="29010-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="29010-158">마지막 메서드는 끝점 및 프로필을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="29010-159">프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="29010-159">Running the program</span></span>
<span data-ttu-id="29010-160">이제 Visual Studio에서 **시작** 단추를 클릭하면 프로그램을 컴파일하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29010-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![프로그램 실행](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="29010-162">프로그램이 위 프롬프트까지 도달하면 Azure 포털의 리소스 그룹에 돌아가서 프로필이 만들어진 것을 확인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![성공!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="29010-164">나머지 프로그램을 실행시키는 프롬프트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-164">We can then confirm the prompts to run the rest of the program.</span></span>

![프로그램 완료](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="29010-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29010-166">Next Steps</span></span>
<span data-ttu-id="29010-167">이 연습에서 작성된 프로젝트를 보려면 [샘플을 다운로드하세요](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="29010-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="29010-168">.NET용 Azure CDN 관리 라이브러리에 관한 추가 설명서는 [MSDN 참조](https://msdn.microsoft.com/library/mt657769.aspx)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="29010-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="29010-169">[PowerShell](cdn-manage-powershell.md)을 사용하여 CDN 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="29010-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

