---
title: "aaaCreate 공유 액세스 서명 (SAS)를 사용 하 여 Azure Blob 저장소와 | Microsoft Docs"
description: "이 자습서에서는 Blob 저장소를 통해 toocreate 공유 액세스 서명을 사용 하기 위해 방법 등에 tooconsume 클라이언트 응용 프로그램에서 해당 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="14d55-103">공유 액세스 서명, 2부: Blob 저장소를 사용하여 SAS 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="14d55-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="14d55-104">[1부](storage-dotnet-shared-access-signature-part-1.md) 에서는 SAS(공유 액세스 서명)에 대해 설명하고 SAS 사용을 위한 모범 사례를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="14d55-105">2 부를 보면 어떻게 toogenerate 하 고 다음 사용 하 여 공유 액세스 서명은 Blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="14d55-106">hello 예제 C#으로 작성 하 고.NET 용 hello Azure 저장소 클라이언트 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="14d55-107">이 자습서에서는 예제 hello:</span><span class="sxs-lookup"><span data-stu-id="14d55-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="14d55-108">컨테이너에서 공유 액세스 서명 생성</span><span class="sxs-lookup"><span data-stu-id="14d55-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="14d55-109">Blob에서 공유 액세스 서명 생성</span><span class="sxs-lookup"><span data-stu-id="14d55-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="14d55-110">컨테이너의 리소스에 저장 된 액세스 정책 toomanage 서명 만들기</span><span class="sxs-lookup"><span data-stu-id="14d55-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="14d55-111">Hello 공유 액세스 서명을 클라이언트 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="14d55-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="14d55-112">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="14d55-112">About this tutorial</span></span>
<span data-ttu-id="14d55-113">이 자습서에서는 두 개의 콘솔 응용 프로그램을 만들어 컨테이너 및 Blob에 대한 공유 액세스 서명을 만들고 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="14d55-114">**응용 프로그램 1**: hello 관리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="14d55-115">컨테이너 및 Blob에 대한 공유 액세스 서명을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="14d55-116">소스 코드에 hello 저장소 계정 액세스 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="14d55-117">**응용 프로그램 2**: hello 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="14d55-118">액세스 컨테이너 및 blob 리소스 hello 첫 번째 응용 프로그램을 사용 하 여 만든 hello 공유 액세스 서명을 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="14d55-119">가 사용 하 여만 hello 공유 액세스 서명 tooaccess 컨테이너 및 blob 리소스- *하지* hello 저장소 계정 액세스 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="14d55-120">1 단계: 콘솔 응용 프로그램 toogenerate 공유 액세스 서명 만들기</span><span class="sxs-lookup"><span data-stu-id="14d55-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="14d55-121">먼저,.NET 설치에 대 한 Azure 저장소 클라이언트 라이브러리 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="14d55-122">Hello를 설치할 수 있습니다 [NuGet 패키지](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet 패키지") hello 클라이언트 라이브러리에 대 한 hello 가장 최신 어셈블리를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="14d55-123">이 hello 권장 hello 가장 최근 픽스를 확보 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="14d55-124">Hello hello 가장 최신 버전의 일부로 hello 클라이언트 라이브러리를 다운로드할 수도 있습니다 [Azure SDK for.NET](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="14d55-125">Visual Studio에서 새 Windows 콘솔 응용 프로그램을 만들고 이름을 **GenerateSharedAccessSignatures**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="14d55-126">참조를 너무 추가[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) 및 [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) hello 다음 방법 중 하나를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="14d55-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="14d55-127">사용 하 여 hello [NuGet 패키지 관리자](https://docs.nuget.org/consume/installing-nuget) Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="14d55-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="14d55-128">**프로젝트** > **NuGet 패키지 관리**를 선택하여 각 패키지(Microsoft.WindowsAzure.ConfigurationManager 및 WindowsAzure.Storage)를 온라인으로 검색하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="14d55-129">Hello Azure SDK 설치에서 이러한 어셈블리를 찾아서 toothem 참조 추가 또는:</span><span class="sxs-lookup"><span data-stu-id="14d55-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="14d55-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="14d55-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="14d55-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="14d55-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="14d55-132">Hello Program.cs 파일의 hello 위쪽 hello 다음 추가 **를 사용 하 여** 지시문:</span><span class="sxs-lookup"><span data-stu-id="14d55-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="14d55-133">Tooyour 저장소 계정을 가리키는 연결 문자열을 사용 하는 구성 설정 포함 되도록 hello app.config 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="14d55-134">App.config 파일은 유사한 toothis 하나 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-134">Your app.config file should look similar toothis one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="14d55-135">컨테이너에 대한 공유 액세스 서명 URI 생성</span><span class="sxs-lookup"><span data-stu-id="14d55-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="14d55-136">와 toobegin, 새 컨테이너에 메서드 toogenerate 공유 액세스 서명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="14d55-137">이 경우 hello 서명을 저장 된 액세스 정책과 연결 되어 있지 않습니다., 부여 hello 만료 시간 및 hello 사용 권한을 나타내는 URI hello 정보에 전달 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="14d55-138">먼저 추가 하는 코드 toohello **main ()** 메서드 tooauthenticate tooyour 저장소 계정에 액세스 하 고 새 컨테이너 만들기:</span><span class="sxs-lookup"><span data-stu-id="14d55-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

<span data-ttu-id="14d55-139">다음으로 hello 컨테이너에 대 한 hello 공유 액세스 서명을 생성 하 고 hello 서명 URI를 반환 하는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="14d55-140">위의 hello hello 맨 아래에 있는 삼각형 hello 추가 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**, toocall **GetContainerSasUri()** hello 및 서명 URI toohello 콘솔 창:</span><span class="sxs-lookup"><span data-stu-id="14d55-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="14d55-141">컴파일하고 hello 새 컨테이너에 대 한 toooutput hello 공유 액세스 서명 URI를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="14d55-142">hello URI 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="14d55-143">Hello 코드를 실행 하면 hello 컨테이너에 대해 만든 hello 공유 액세스 서명을 수 hello에 대 한 유효한 다음 24 시간.</span><span class="sxs-lookup"><span data-stu-id="14d55-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="14d55-144">hello 서명은 클라이언트 hello 컨테이너와 toowrite 새 blob toohello 컨테이너의 권한 toolist blob을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="14d55-145">Blob에 대한 공유 액세스 서명 URI 생성</span><span class="sxs-lookup"><span data-stu-id="14d55-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="14d55-146">다음으로, 비슷한 코드 toocreate hello 컨테이너 내에서 새 blob을 쓰는 하 고 그에 대 한 공유 액세스 서명을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="14d55-147">Hello 시작 시간, 만료 시간 및 사용 권한 정보 hello URI에에서 포함 하도록이 공유 액세스 서명을 저장 된 액세스 정책과 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="14d55-148">새 메서드를 추가 새 blob을 만듭니다 및 일부 텍스트 tooit 작성 한 다음 공유 액세스 서명을 생성 hello 서명 URI를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="14d55-149">Hello hello 맨 아래에 **main ()** 메서드를 다음 줄 toocall hello 추가 **GetBlobSasUri()**hello 너무 호출 전에,**console.readline ()**를 공유 하는 hello 및 액세스 서명 URI toohello 콘솔 창:</span><span class="sxs-lookup"><span data-stu-id="14d55-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="14d55-150">컴파일하고 hello 새 blob에 대 한 toooutput hello 공유 액세스 서명 URI를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="14d55-151">hello URI 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="14d55-152">Hello 컨테이너에 저장 된 액세스 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="14d55-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="14d55-153">이제 연결 된 모든 공유 액세스 서명에 대 한 hello 제약 조건을 정의 하는 hello 컨테이너에 저장된 된 액세스 정책을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="14d55-154">Hello 이전 예제의 (암시적 또는 명시적) hello 시작 시간 지정, hello 만료 시간 및 hello에 대 한 hello 권한을 공유 액세스 서명 URI 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="14d55-155">다음 예제는 hello, 이러한 hello 공유 액세스 서명을 아니라 hello 저장 된 액세스 정책에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="14d55-156">이렇게 하면 우리 toochange hello를 다시 발급 하지 않고도 이러한 제약 조건을 공유 서명에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="14d55-157">Hello 공유 액세스 서명에 대 한 hello 제약 조건 및 hello 나머지 hello 저장 된 액세스 정책에서 하나 이상의 가능한 toohave 것합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="14d55-158">그러나 hello 시작 시간, 만료 시간 및 권한을 한 위치 또는 다른 hello에만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="14d55-159">예를 들어 hello 공유 액세스 서명에서 사용 권한을 지정 하 고 hello 저장 된 액세스 정책에서 지정할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="14d55-160">저장 된 액세스 정책 tooa 컨테이너를 추가 하면 기존 사용 권한을 가지 hello 컨테이너, hello 새 액세스 정책 추가 하며 다음 hello 컨테이너의 사용 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="14d55-161">컨테이너에 새 저장 된 액세스 정책을 만들고 hello 정책 hello 이름을 반환 하는 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="14d55-162">Hello hello 맨 아래에 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**다음 hello toofirst 지우기 모든 기존 액세스 정책을 줄을 추가 하 고, 다음 호출 hello  **CreateSharedAccessPolicy()** 메서드:</span><span class="sxs-lookup"><span data-stu-id="14d55-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="14d55-163">컨테이너에서 hello 액세스 정책을 선택을 취소 하면 먼저 hello 컨테이너의 기존 사용 권한을 다음 지우기 hello 사용 권한을 가져올 하십시오 hello 권한을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="14d55-164">공유 액세스 서명 URI에 대 한 액세스 정책을 사용 하는 hello 컨테이너 생성</span><span class="sxs-lookup"><span data-stu-id="14d55-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="14d55-165">다음으로, 앞에서 만든 hello 컨테이너에 대 한 다른 공유 액세스 서명을 만듭니다 하지만이 이번 म hello 서명을와 연결 hello 이전 예제에서 만든 hello 저장 된 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="14d55-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="14d55-166">새 메서드 toogenerate hello 컨테이너에 대 한 다른 공유 액세스 서명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="14d55-167">Hello hello 맨 아래에 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**, 다음 줄 toocall hello hello 추가 **GetContainerSasUriWithPolicy** 메서드 :</span><span class="sxs-lookup"><span data-stu-id="14d55-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="14d55-168">액세스 정책에 Blob을 사용 하는 hello는 공유 액세스 서명 URI 생성</span><span class="sxs-lookup"><span data-stu-id="14d55-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="14d55-169">마지막으로, 비슷한 메서드 toocreate 다른 blob을 추가 하 고 저장 된 액세스 정책은 연관 된 공유 액세스 서명을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="14d55-170">새 메서드 toocreate blob을 추가 하 고 공유 액세스 서명을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="14d55-171">Hello hello 맨 아래에 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**, 다음 줄 toocall hello hello 추가 **GetBlobSasUriWithPolicy** 메서드:</span><span class="sxs-lookup"><span data-stu-id="14d55-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="14d55-172">hello **main ()** 메서드는 이제 한 번에 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="14d55-173">Toowrite hello 공유 액세스 서명 Uri toohello 콘솔 창 실행 복사 및 hello이이 자습서의 두 번째 부분에서 사용 하기 위해 텍스트 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="14d55-174">Hello GenerateSharedAccessSignatures 콘솔 응용 프로그램을 실행 하면 유사한 toohello 다음 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="14d55-175">이들은 hello 자습서의 2 부에에서는 사용 하 여 hello 공유 액세스 서명입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="14d55-176">2 단계: 콘솔 응용 프로그램 tootest hello 공유 액세스 서명 만들기</span><span class="sxs-lookup"><span data-stu-id="14d55-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="14d55-177">tootest hello 공유 액세스 서명을 hello 이전 예제에서 만든, blob 및 hello 컨테이너에서 hello 서명 tooperform 작업을 사용 하는 두 번째 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="14d55-178">Hello hello 자습서의 첫 번째 단계를 완료 후 24 시간 이상 경과할 hello 서명을 생성 하는 더 이상 유효 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="14d55-179">이 경우 hello hello 자습서의 두 번째 부분에서 사용 하기 위해 새 공유 액세스 서명을 hello 첫 번째 콘솔 응용 프로그램 toogenerate에 hello 코드를 실행 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="14d55-180">Visual Studio에서 새 Windows 콘솔 응용 프로그램을 만들고 이름을 **ConsumeSharedAccessSignatures**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="14d55-181">참조를 너무 추가[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) 및 [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/)위에서 설명한 것 처럼, 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="14d55-182">Hello Program.cs 파일의 hello 위쪽 hello 다음 추가 **를 사용 하 여** 지시문:</span><span class="sxs-lookup"><span data-stu-id="14d55-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="14d55-183">Hello의 hello 본문에서 **main ()** 메서드를 추가 hello 문자열 상수 뒤, hello 자습서의 1 단계에서 생성 한 해당 값 toohello 공유 액세스 서명을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="14d55-184">공유 액세스 서명을 사용 하 여 지정 하 여 메서드 tootry 컨테이너 작업 추가</span><span class="sxs-lookup"><span data-stu-id="14d55-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="14d55-185">다음으로 hello 컨테이너에 대 한 공유 액세스 서명을 사용 하 여 일부 컨테이너 작업을 테스트 하는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="14d55-186">hello 공유 액세스 서명을 사용 하는 tooreturn 단독 hello 서명 기반의 액세스 toohello 컨테이너를 인증 하는 참조 toohello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="14d55-187">다음 메서드 tooProgram.cs hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-187">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="14d55-188">업데이트 hello **main ()** 메서드 toocall **UseContainerSAS()** hello를 모두 사용 하 여 공유 액세스 서명 hello 컨테이너에서 만든:</span><span class="sxs-lookup"><span data-stu-id="14d55-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="14d55-189">공유 액세스 서명을 사용 하는 메서드 tootry blob 작업 추가</span><span class="sxs-lookup"><span data-stu-id="14d55-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="14d55-190">마지막으로, 공유 액세스 서명을 사용 하 여 hello blob에서 일부 blob 작업을 테스트 하는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="14d55-191">이 경우 hello 생성자 사용 **CloudBlockBlob(String)**tooreturn 참조 toohello blob, 공유 액세스 서명을 hello에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="14d55-192">다른 인증이 필요 하지 않습니다. hello 시그니처 만으로는 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="14d55-193">다음 메서드 tooProgram.cs hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-193">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="14d55-194">업데이트 hello **main ()** 메서드 toocall **UseBlobSAS()** hello를 모두 사용 하 여 공유 hello blob에 만든 액세스 서명:</span><span class="sxs-lookup"><span data-stu-id="14d55-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="14d55-195">Hello 콘솔 응용 프로그램을 실행 하 고 hello 출력 toosee 어떤 서명에 대 한 허용 되는 작업을 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="14d55-196">hello 콘솔 창의 hello 출력에는 비슷한 toohello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d55-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="14d55-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14d55-197">Next Steps</span></span>

* [<span data-ttu-id="14d55-198">이해 hello 공유 액세스 서명, 1 부: SAS 모델</span><span class="sxs-lookup"><span data-stu-id="14d55-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="14d55-199">익명 읽기 권한을 toocontainers 및 blob 관리</span><span class="sxs-lookup"><span data-stu-id="14d55-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="14d55-200">공유 액세스 서명을 사용하여 액세스 위임(REST API)</span><span class="sxs-lookup"><span data-stu-id="14d55-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="14d55-201">테이블 및 큐 SAS 소개</span><span class="sxs-lookup"><span data-stu-id="14d55-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
