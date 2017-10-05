---
title: ".NET을 사용하여 Media Services 계정에 연결하기"
description: "이 항목에서는 .NET을 사용하여 Media Services에 연결하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="8389c-103">.NET용 Media Services SDK을 사용하여 미디어 서비스 계정에 연결하기</span><span class="sxs-lookup"><span data-stu-id="8389c-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8389c-104">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="8389c-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="8389c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8389c-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="8389c-106">이 토픽에서는.NET용 Media Services SDK를 프로그래밍할 때 Microsoft Azure Media Services에 프로그래밍 방식의 연결을 가져오는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="8389c-107">Media Services에 연결하기</span><span class="sxs-lookup"><span data-stu-id="8389c-107">Connecting to Media Services</span></span>
<span data-ttu-id="8389c-108">Media Services에 프로그래밍 방식으로 연결하려면 이전에 Azure 계정을 설정하고, 해당 계정에 Media Services를 구성한 다음, .NET용 Media Services SDK를 사용하여 개발을 위한 Visual Studio 프로젝트를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="8389c-109">자세한 내용은 .NET용 Media Services SDK를 사용하여 개발을 위한 설정을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8389c-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="8389c-110">Media Services 계정 설정 과정이 끝나면 다음과 같은 필수 연결 값을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="8389c-111">이를 사용하여 Media Services에 프로그래밍 방식으로 연결하기</span><span class="sxs-lookup"><span data-stu-id="8389c-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="8389c-112">Media Services 계정 이름.</span><span class="sxs-lookup"><span data-stu-id="8389c-112">Your Media Services account name.</span></span>
* <span data-ttu-id="8389c-113">Media Services 계정 키.</span><span class="sxs-lookup"><span data-stu-id="8389c-113">Your Media Services account key.</span></span>

<span data-ttu-id="8389c-114">이러한 값을 찾으려면 Azure 관리 포털을 방문하여 미디어 서비스 계정을 선택하고 포털 창의 하단에 있는 "**키 관리**" 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="8389c-115">각 텍스트 상자 옆에 있는 아이콘을 클릭하면 값을 시스템 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="8389c-116">CloudMediaContext 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="8389c-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="8389c-117">서버 컨텍스트를 나타내는 **CloudMediaContext** 인스턴스를 만드는 데 필요한 Media Services에 대한 프로그래밍을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="8389c-118">**CloudMediaContext** 에는 작업, 자산, 파일, 액세스 정책 및 로케이터를 비롯하여 중요한 컬렉션에 대한 참조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="8389c-119">**CloudMediaContext** 클래스는 스레드로부터 안전하게 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="8389c-120">스레드마다 또는 작업 집합마다 새 CloudMediaContext를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="8389c-121">CloudMediaContext에는 5개의 생성자 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="8389c-122">**MediaServicesCredentials** 를 매개 변수로 사용하는 생성자를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="8389c-123">자세한 내용은 이어지는 **액세스 제어 서비스 토큰 다시 사용** 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8389c-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="8389c-124">다음 예제에서는 공용 CloudMediaContext(MediaServicesCredentials 자격 증명) 생성자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="8389c-125">액세스 제어 서비스 토큰 다시 사용</span><span class="sxs-lookup"><span data-stu-id="8389c-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="8389c-126">이 섹션에서는 MediaServicesCredentials을 매개 변수로 사용하는 CloudMediaContext 생성자를 사용하여 액세스 제어 서비스 토큰을 다시 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="8389c-127">[Azure Active Directory 액세스 제어](https://msdn.microsoft.com/library/hh147631.aspx) (액세스 제어 서비스 또는 ACS)는 웹 응용 프로그램에 대한 액세스 권한을 얻기 위해 인증하고 권한을 부여하는 쉬운 방법을 제공하는 클라우드 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="8389c-128">Microsoft Azure Media Services는 ACS 토큰을 필요로 하는 OAuth 프로토콜을 통해 서비스에 대한 액세스 권한을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="8389c-129">Media Services는 권한 부여 서버에서 ACS 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="8389c-130">Media Services SDK를 사용하여 개발할 때 SDK 코드가 이를 관리하기 때문에 토큰을 처리하지 않도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="8389c-131">하지만 SDK가 불필요한 토큰 요청으로 이어지는 ACS 토큰을 완벽하게 관리하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="8389c-132">토큰 요청은 시간이 걸리며 클라이언트 및 서버 리소스를 소모합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="8389c-133">뿐만 아니라, 속도가 너무 높은 경우 ACS 서버가 요청을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="8389c-134">초당 30개로 제한하며 [ACS 서비스 제한](https://msdn.microsoft.com/library/gg185909.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8389c-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="8389c-135">Media Services SDK 버전 3.0.0.0부터 ACS 토큰을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="8389c-136">**MediaServicesCredentials**를 매개 변수로 사용하는 **CloudMediaContext** 생성자는 여러 컨텍스트 사이에서 ACS 토큰을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="8389c-137">MediaServicesCredentials 클래스는 Media Services 자격 증명을 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="8389c-138">ACS 토큰을 사용할 수 있으며 해당 만료 시간을 알고 있는 경우, 토큰으로 새 MediaServicesCredentials 인스턴스를 만들고 CloudMediaContext 생성자에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="8389c-139">만료될 때마다 Media Services SDK가 토큰을 자동으로 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="8389c-140">아래 예에서 보이는 것처럼 ACS 토큰을 다시 사용한느 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="8389c-141">메모리에서 **MediaServicesCredentials** 개체를 캐시할 수 있습니다(예: 정적 클래스 변수).</span><span class="sxs-lookup"><span data-stu-id="8389c-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="8389c-142">그런 다음 CloudMediaContext 생성자에 캐시된 개체를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="8389c-143">MediaServicesCredentials 개체는 여전히 유효한 경우에 다시 사용할 수 있는 ACS 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="8389c-144">토큰이 유효하지 않은 경우, MediaServicesCredentials 생성자에 주어진 자격 증명을 사용하여 Media Services SDK를 통해 새로 고침됩니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="8389c-145">**MediaServicesCredentials** 개체가 RefreshToken 호출 후 유요한 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="8389c-146">**CloudMediaContext**는 생성자에서 **RefreshToken** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="8389c-147">외부 저장소에 토큰 값을 저장하려는 경우 토큰 데이터를 저장하기 전에 TokenExpiration 값이 유효한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="8389c-148">유효하지 않으면 캐싱 전에 RefreshToken을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="8389c-149">AccessToken 문자열 및 TokenExpiration 값도 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="8389c-150">값은 캐시된 토큰 데이터를 새 MediaServicesCredentials 개체로 만들기 위해 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="8389c-151">여러 프로세스 또는 컴퓨터 사이에서 토큰을 안전하게 공유할 수 있는 시나리오에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="8389c-152">다음 코드 조각은 이 예에서 정의되지 않은 SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage 및 UpdateTokenDataInExternalStorageIfNeeded 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="8389c-153">외부 저장소에서 토큰 데이터를 저장, 검색 및 업데이트하기 위해 이러한 메서드를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="8389c-154">저장된 토큰 값을 사용하여 MediaServicesCredentials를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-154">Use the saved token values to create MediaServicesCredentials.</span></span>

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    <span data-ttu-id="8389c-155">토큰이 미디어 서비스 SDK에서 업데이트된 경우 토큰 복사본을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="8389c-156">여러 Media Services 계정이 있는 경우(예: 로드 공유 목적 또는 지역 배포) System.Collections.Concurrent.ConcurrentDictionary 컬렉션을 사용하여 MediaServicesCredentials 개체를 캐시할 수 있습니다(ConcurrentDictionary 컬렉션은 여러 스레드에서 동시에 액세스할 수 있는 키/값 쌍의 스레드로부터 안전하게 보호되는 컬렉션을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="8389c-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="8389c-157">그런 다음 캐시된 자격 증명을 가져오는 GetOrAdd 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="8389c-158">중국 북부 지역에 있는 Media Services 계정에 연결하기</span><span class="sxs-lookup"><span data-stu-id="8389c-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="8389c-159">계정이 중국 북부 지역에 있으면 다음 생성자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="8389c-160">예:</span><span class="sxs-lookup"><span data-stu-id="8389c-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="8389c-161">구성에서 연결 값 저장</span><span class="sxs-lookup"><span data-stu-id="8389c-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="8389c-162">구성에서 연결 값, 사용자 계정 이름 및 암호와 같은 특히 중요한 값을 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="8389c-163">중요한 구성 데이터를 암호화하는 것도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="8389c-164">Windows EFS(파일 시스템 암호화)를 사용하여 전체 구성 파일을 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="8389c-165">파일에서 EFS를 사용하려면 파일을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하여 **고급** 설정 탭에서 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="8389c-166">또는 보호되는 구성을 사용하여 구성 파일에서 선택한 부분을 암호화하기 위해 사용자 지정 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="8389c-167">[보호되는 구성을 사용하여 구성 정보 암호화](https://msdn.microsoft.com/library/53tyfkaw.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8389c-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="8389c-168">다음 App.config 파일에는 필수 연결 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="8389c-169"><appSettings> 요소의 값은 Media Services 게정 설정 과정에서 가져온 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="8389c-170">구성에서 연결 값을 검색하려면 **ConfigurationManager** 클래스를 사용한 다음 코드에서 필드에 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="8389c-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="8389c-171">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="8389c-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8389c-172">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="8389c-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

