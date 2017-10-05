---
title: "Azure Storage에서 개체 속성 및 메타데이터를 설정 및 검색 | Microsoft Docs"
description: "Azure 저장소의 개체에 사용자 지정 메타데이터를 저장하고 시스템 속성을 설정 및 검색합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="5bb3e-103">속성 및 메타데이터 설정 및 검색</span><span class="sxs-lookup"><span data-stu-id="5bb3e-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="5bb3e-104">Azure Storage의 개체는 시스템 속성 및 사용자 정의 메타데이터와 포함된 데이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="5bb3e-105">이 문서에서는 [.NET용 Azure Storage 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)를 사용하여 관리 시스템 속성 및 사용자 정의 메타데이터를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="5bb3e-106">**시스템 속성**: 각 저장소 리소스에 시스템 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="5bb3e-107">그 중 일부를 읽거나 설정할 수 있지만 나머지는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="5bb3e-108">일부 시스템 속성은 내부적으로 특정 표준 HTTP 헤더에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="5bb3e-109">Azure 저장소 클라이언트 라이브러리에서 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="5bb3e-110">**사용자 정의 메타데이터**: 사용자 정의 메타 데이터는 이름-값 쌍의 형태로 제공된 리소스에서 지정 하는 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="5bb3e-111">메타데이터를 사용하여 저장소 리소스와 함께 추가 값을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="5bb3e-112">이러한 추가 메타데이터 값은 고유한 목적으로만 사용되며 리소스의 동작 방식에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="5bb3e-113">저장소 리소스에 대한 속성 및 메타데이터 값 검색은 두 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="5bb3e-114">이러한 값을 읽으려면 먼저 **FetchAttributes** 메서드를 호출하여 명시적으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bb3e-115">**FetchAttributes** 메서드 중 하나를 호출하지 않으면 저장소 리소스에 대한 속성 및 메타데이터 값이 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="5bb3e-116">이름/값 쌍에 ASCII 문자가 아닌 문자가 포함되어 있으면 `400 Bad Request`를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="5bb3e-117">메타데이터 이름/값 쌍은 유효한 HTTP 헤더이며, HTTP 헤더와 관련된 모든 제한 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="5bb3e-118">따라서 ASCII 문자가 아닌 문자가 포함된 이름 및 값에 URL 인코딩 또는 Base64 인코딩을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="5bb3e-119">속성 설정 및 검색</span><span class="sxs-lookup"><span data-stu-id="5bb3e-119">Setting and retrieving properties</span></span>
<span data-ttu-id="5bb3e-120">속성 값을 검색하려면 Blob 또는 컨테이너에서 **FetchAttributes** 메서드를 호출하여 속성을 채운 다음 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="5bb3e-121">개체에서 속성을 설정하려면 속성 값을 지정한 다음 **SetProperties** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="5bb3e-122">다음 코드 예제는 컨테이너를 만들고 콘솔 창에 속성 값 일부를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="5bb3e-123">메타데이터 설정 및 검색</span><span class="sxs-lookup"><span data-stu-id="5bb3e-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="5bb3e-124">Blob 또는 컨테이너 리소스에 하나 이상의 이름-값 쌍으로 메타 데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="5bb3e-125">메타데이터를 설정하려면 이름-값 쌍을 리소스의 **메타데이터** 컬렉션에 추가한 다음, **SetMetadata** 메서드를 호출하여 값을 서비스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="5bb3e-126">메타데이터의 이름은 C# 식별자에 대한 명명 규칙을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="5bb3e-127">다음 코드 예제에서는 컨테이너에서 메타데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="5bb3e-128">하나의 값은 컬렉션의 **추가** 메서드를 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="5bb3e-129">다른 값은 암시적 키/값 구문을 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="5bb3e-130">둘 다 모두 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="5bb3e-131">메타데이터를 검색하려면 아래 예제에 나온 것처럼 Blob 또는 컨테이너에서 **FetchAttributes** 메서드를 호출하여 **Metadata** 컬렉션을 채운 다음 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb3e-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5bb3e-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5bb3e-132">Next steps</span></span>
* [<span data-ttu-id="5bb3e-133">.NET용 Azure Storage 클라이언트 라이브러리 참조</span><span class="sxs-lookup"><span data-stu-id="5bb3e-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="5bb3e-134">.NET용 Azure Storage 클라이언트 라이브러리 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="5bb3e-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
