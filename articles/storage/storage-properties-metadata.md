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
# <a name="set-and-retrieve-properties-and-metadata"></a>속성 및 메타데이터 설정 및 검색

개체에 Azure 저장소 지원 시스템 속성과 사용자 정의 메타 데이터 뿐만 아니라 toohello 포함 된 데이터입니다. 이 문서에서는 관리 시스템 속성 및 사용자 정의 메타 데이터 hello로 [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)합니다.

* **시스템 속성**: 각 저장소 리소스에 시스템 속성이 있습니다. 그 중 일부를 읽거나 설정할 수 있지만 나머지는 읽기 전용입니다. 일부 시스템 속성 hello 내부적 toocertain 표준 HTTP 헤더에 해당 합니다. hello Azure 저장소 클라이언트 라이브러리를 유지 관리 하기 위해 합니다.

* **사용자 정의 메타 데이터**: 사용자 정의 메타 데이터는 지정된 된 리소스 이름-값 쌍 형식의 hello에에서 지정 하는 메타 데이터입니다. 저장소 리소스와 메타 데이터 toostore 추가 값을 사용할 수 있습니다. 이러한 추가 메타 데이터 값이 고유한 목적 으로만 되어 hello 리소스 동작 하는 방식에 영향을 주지 않습니다.

저장소 리소스에 대한 속성 및 메타데이터 값 검색은 두 단계로 이루어집니다. 이 값을 읽을 수 있습니다, 전에 하면 명시적으로 인출 해야 hello를 호출 하 여 **FetchAttributes** 메서드.

> [!IMPORTANT]
> 저장소 리소스에 대 한 속성 및 메타 데이터 값 hello 중 하나를 호출 하지 않으면 적용 하지 않고 **FetchAttributes** 메서드.
>
> 이름/값 쌍에 ASCII 문자가 아닌 문자가 포함되어 있으면 `400 Bad Request`를 수신합니다. 메타 데이터 이름/값 쌍은 유효한 HTTP 헤더 등과 HTTP 헤더를 제어 하는 tooall 제한 사항을 준수 해야 합니다. 따라서 ASCII 문자가 아닌 문자가 포함된 이름 및 값에 URL 인코딩 또는 Base64 인코딩을 사용하는 것이 좋습니다.
>

## <a name="setting-and-retrieving-properties"></a>속성 설정 및 검색
tooretrieve 속성 값, 호출 hello **FetchAttributes** blob 또는 컨테이너 toopopulate hello 속성, 메서드는 다음 hello 값을 읽을 합니다.

개체에 대 한 tooset 속성 hello 속성 값을 지정한 다음 호출 해야 hello **SetProperties** 메서드.

hello 다음 코드 예제에서는 컨테이너를 만듭니다 다음 해당 속성 값 tooa 콘솔 창 중 일부를 씁니다.

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

## <a name="setting-and-retrieving-metadata"></a>메타데이터 설정 및 검색
Blob 또는 컨테이너 리소스에 하나 이상의 이름-값 쌍으로 메타 데이터를 지정할 수 있습니다. tooset 메타 데이터 이름-값 쌍 toohello 추가 **메타 데이터** hello 리소스에 대 한 컬렉션 hello 호출 **SetMetadata** 메서드 toosave hello toohello 서비스 값.

> [!NOTE]
> 메타 데이터의 hello 이름은 C# 식별자에 대 한 toohello 명명 규칙을 따라야 합니다.
>
>

hello 다음 코드 예제에서는 메타 데이터에서 설정 컨테이너입니다. Hello 컬렉션을 사용 하 여 하나의 값이 설정 **추가** 메서드. hello 다른 값이 설정 암시적 키/값 구문을 사용 하 여 합니다. 둘 다 모두 유효합니다.

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

tooretrieve 메타 데이터를 호출 hello **FetchAttributes** 프로그램 blob 또는 컨테이너 toopopulate hello에서 메서드가 **메타 데이터** 다음 아래 hello 예에 나와 있는 것 처럼 hello 값을 읽을 컬렉션입니다.

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

## <a name="next-steps"></a>다음 단계
* [.NET용 Azure Storage 클라이언트 라이브러리 참조](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [.NET용 Azure Storage 클라이언트 라이브러리 NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.Storage/)
