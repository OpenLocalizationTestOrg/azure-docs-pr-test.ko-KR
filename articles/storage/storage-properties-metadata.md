---
title: "aaaSet 및 검색 하 고 개체 속성 및 메타 데이터를 Azure 저장소 | Microsoft Docs"
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
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="265eb-103">속성 및 메타데이터 설정 및 검색</span><span class="sxs-lookup"><span data-stu-id="265eb-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="265eb-104">개체에 Azure 저장소 지원 시스템 속성과 사용자 정의 메타 데이터 뿐만 아니라 toohello 포함 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="265eb-105">이 문서에서는 관리 시스템 속성 및 사용자 정의 메타 데이터 hello로 [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="265eb-106">**시스템 속성**: 각 저장소 리소스에 시스템 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="265eb-107">그 중 일부를 읽거나 설정할 수 있지만 나머지는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="265eb-108">일부 시스템 속성 hello 내부적 toocertain 표준 HTTP 헤더에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="265eb-109">hello Azure 저장소 클라이언트 라이브러리를 유지 관리 하기 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="265eb-110">**사용자 정의 메타 데이터**: 사용자 정의 메타 데이터는 지정된 된 리소스 이름-값 쌍 형식의 hello에에서 지정 하는 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="265eb-111">저장소 리소스와 메타 데이터 toostore 추가 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="265eb-112">이러한 추가 메타 데이터 값이 고유한 목적 으로만 되어 hello 리소스 동작 하는 방식에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="265eb-113">저장소 리소스에 대한 속성 및 메타데이터 값 검색은 두 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="265eb-114">이 값을 읽을 수 있습니다, 전에 하면 명시적으로 인출 해야 hello를 호출 하 여 **FetchAttributes** 메서드.</span><span class="sxs-lookup"><span data-stu-id="265eb-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="265eb-115">저장소 리소스에 대 한 속성 및 메타 데이터 값 hello 중 하나를 호출 하지 않으면 적용 하지 않고 **FetchAttributes** 메서드.</span><span class="sxs-lookup"><span data-stu-id="265eb-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="265eb-116">이름/값 쌍에 ASCII 문자가 아닌 문자가 포함되어 있으면 `400 Bad Request`를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="265eb-117">메타 데이터 이름/값 쌍은 유효한 HTTP 헤더 등과 HTTP 헤더를 제어 하는 tooall 제한 사항을 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="265eb-118">따라서 ASCII 문자가 아닌 문자가 포함된 이름 및 값에 URL 인코딩 또는 Base64 인코딩을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="265eb-119">속성 설정 및 검색</span><span class="sxs-lookup"><span data-stu-id="265eb-119">Setting and retrieving properties</span></span>
<span data-ttu-id="265eb-120">tooretrieve 속성 값, 호출 hello **FetchAttributes** blob 또는 컨테이너 toopopulate hello 속성, 메서드는 다음 hello 값을 읽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="265eb-121">개체에 대 한 tooset 속성 hello 속성 값을 지정한 다음 호출 해야 hello **SetProperties** 메서드.</span><span class="sxs-lookup"><span data-stu-id="265eb-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="265eb-122">hello 다음 코드 예제에서는 컨테이너를 만듭니다 다음 해당 속성 값 tooa 콘솔 창 중 일부를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="265eb-123">메타데이터 설정 및 검색</span><span class="sxs-lookup"><span data-stu-id="265eb-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="265eb-124">Blob 또는 컨테이너 리소스에 하나 이상의 이름-값 쌍으로 메타 데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="265eb-125">tooset 메타 데이터 이름-값 쌍 toohello 추가 **메타 데이터** hello 리소스에 대 한 컬렉션 hello 호출 **SetMetadata** 메서드 toosave hello toohello 서비스 값.</span><span class="sxs-lookup"><span data-stu-id="265eb-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="265eb-126">메타 데이터의 hello 이름은 C# 식별자에 대 한 toohello 명명 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="265eb-127">hello 다음 코드 예제에서는 메타 데이터에서 설정 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="265eb-128">Hello 컬렉션을 사용 하 여 하나의 값이 설정 **추가** 메서드.</span><span class="sxs-lookup"><span data-stu-id="265eb-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="265eb-129">hello 다른 값이 설정 암시적 키/값 구문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="265eb-130">둘 다 모두 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="265eb-131">tooretrieve 메타 데이터를 호출 hello **FetchAttributes** 프로그램 blob 또는 컨테이너 toopopulate hello에서 메서드가 **메타 데이터** 다음 아래 hello 예에 나와 있는 것 처럼 hello 값을 읽을 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="265eb-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="265eb-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="265eb-132">Next steps</span></span>
* [<span data-ttu-id="265eb-133">.NET용 Azure Storage 클라이언트 라이브러리 참조</span><span class="sxs-lookup"><span data-stu-id="265eb-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="265eb-134">.NET용 Azure Storage 클라이언트 라이브러리 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="265eb-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
