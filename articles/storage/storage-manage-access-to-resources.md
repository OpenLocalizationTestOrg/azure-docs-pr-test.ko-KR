---
title: "Azure Blob 저장소에서 컨테이너 및 blob에 대 한 aaaEnable 공용 읽기 권한 | Microsoft Docs"
description: "자세한 방법을 toomake 컨테이너 및 blob에 익명 액세스를 사용할 수 있는 방법과 tooaccess에 프로그래밍 방식으로 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>익명 읽기 권한을 toocontainers 및 blob 관리
익명 공용 읽기 액세스 tooa 컨테이너와 그 blob Azure Blob 저장소에 사용할 수 있습니다. 이렇게 하면 사용자의 계정 키를 공유 하지 않고 및 공유 액세스 서명 (SAS)를 요구 하지 않고 toothese 리소스 읽기 전용 액세스를 부여할 수 있습니다.

공용 읽기 액세스 권한을 있는 시나리오는 특정 blob tooalways 익명 읽기 액세스용으로 제공 수에 대 한 가장 좋습니다. 보다 세부적인 제어를 위해 공유 액세스 서명을 만들 수 있습니다. 공유 액세스 서명을 사용 하면 서로 다른 사용 권한을 사용 하 여 특정 기간에 대 한 제한 된 tooprovide 액세스 있습니다. 공유 액세스 서명 만들기에 대한 자세한 내용은 [Azure Storage에서 SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>익명 사용자에 게 사용 권한 toocontainers 및 blob를 부여 합니다.
기본적으로 컨테이너와 그 안에 모든 blob hello 저장소 계정의 소유자 hello에 의해서만 액세스할 수 있습니다. toogive 익명 사용자에 게 읽기 권한이 있으면 tooa 컨테이너와 그 blob hello 컨테이너 권한을 tooallow 공용 액세스를 설정할 수 있습니다. 익명 사용자에 게 hello 요청을 인증 하지 않고 공개적으로 액세스할 수 있는 컨테이너 내 blob를 읽을 수 있습니다.

다음 권한을 hello로 컨테이너를 구성할 수 있습니다.

* **공용 읽기 권한 없음:** hello 컨테이너와 그 blob 저장소 계정 소유자 hello에 의해서만 액세스할 수 있습니다. 모든 새 컨테이너에 대 한 hello 기본값입니다.
* **공용 읽기 권한 blob에 대해서만:** 익명 요청에 의해 hello 컨테이너 내 Blob를 읽을 수 있지만 컨테이너 데이터를 사용할 수 없습니다. 익명 클라이언트 hello 컨테이너에서 hello blob를 열거할 수 없습니다.
* **전체 공용 읽기 권한:** 익명 요청을 통해 모든 컨테이너와 Blob 데이터를 읽을 수 있습니다. 클라이언트가 익명 요청을 하 여 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.

Hello 다음 tooset 컨테이너 권한을 사용할 수 있습니다.

* [Azure 포털](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Azure CLI 2.0](storage-azure-cli.md#create-and-manage-blobs)
* Hello 저장소 클라이언트 라이브러리 또는 hello REST API 중 하나를 사용 하 여 프로그래밍 방식으로,

### <a name="set-container-permissions-in-hello-azure-portal"></a>Hello Azure 포털에서에서 컨테이너 사용 권한 설정
hello에 tooset 컨테이너 권한 [Azure 포털](https://portal.azure.com), 다음이 단계를 수행 합니다.

1. Open 프로그램 **저장소 계정** 블레이드 hello 포털에서. 선택 하 여 저장소 계정을 찾을 수 있습니다 **저장소 계정은** hello 주 포털 메뉴 블레이드에서 합니다.
1. 아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **컨테이너**합니다.
1. Hello 컨테이너 행 이나 선택 hello 줄임표 tooopen hello 컨테이너에서 마우스 오른쪽 단추로 클릭 **상황에 맞는 메뉴**합니다.
1. 선택 **액세스 정책** hello 상황에 맞는 메뉴에서입니다.
1. 선택 된 **액세스 형식** hello에서 드롭다운 메뉴.

    ![컨테이너 메타데이터 편집 대화 상자](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>.NET으로 컨테이너 사용 권한 설정
.net, C# 및 hello 저장소 클라이언트 라이브러리를 사용 하 여 컨테이너에 대 한 사용 권한을 tooset hello를 호출 하 여 hello 컨테이너의 기존 사용 권한을 먼저 검색 **GetPermissions** 메서드. 그런 다음 세트 hello **PublicAccess** hello에 대 한 속성 **BlobContainerPermissions** hello에서 반환 되는 개체 **GetPermissions** 메서드. 마지막으로 hello 호출 **SetPermissions** hello로 메서드 사용 권한을 업데이트 합니다.

다음 예제는 hello toofull 공용 읽기 액세스 권한을 hello 컨테이너의 권한을 설정 합니다. blob에만 hello 설정에 대 한 읽기 액세스를 tooset 권한 toopublic **PublicAccess** 속성 너무**BlobContainerPublicAccessType.Blob**합니다. tooremove 익명 사용자에 대 한 모든 사용 권한이 설정 속성을 너무 hello**BlobContainerPublicAccessType.Off**합니다.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>컨테이너 및 Blob에 익명으로 액세스
컨테이너 및 Blob에 익명으로 액세스하는 클라이언트는 자격 증명을 필요로 하지 않는 생성자를 사용할 수 있습니다. 다음 예제는 hello 몇 가지 방법을 보여 줍니다 tooreference Blob 서비스 리소스 익명으로 합니다.

### <a name="create-an-anonymous-client-object"></a>익명 클라이언트 개체 만들기
Hello 계정에 대 한 hello Blob 서비스 끝점을 제공 하 여 익명 액세스에 대 한 새 서비스 클라이언트 개체를 만들 수 있습니다. 그러나 익명 액세스에 사용할 수 있는 해당 계정에 컨테이너의 hello 이름을 또한 알아야 합니다.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>컨테이너를 익명으로 참조
익명으로 사용할 수 있는 hello URL tooa 컨테이너를 설정한 경우 사용할 수 있습니다 tooreference hello 컨테이너 직접 합니다.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Blob을 익명으로 참조
익명 액세스에 사용할 수 있는 hello URL tooa blob를 설정한 경우 해당 URL을 사용 하 여 직접 hello blob를 참조할 수 있습니다.

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>사용 가능한 tooanonymous 사용자 기능
다음 표에서 hello 컨테이너의 ACL tooallow 공용 액세스가 설정 된 경우 익명 사용자가 어떤 작업을 호출할 수 있습니다.

| REST 작업 | 전체 공용 읽기가 가능한 권한 | Blob 전용 공용 읽기가 가능한 권한 |
| --- | --- | --- |
| 컨테이너 나열 |소유자만 |소유자만 |
| 컨테이너 만들기 |소유자만 |소유자만 |
| 컨테이너 속성 가져오기 |모두 |소유자만 |
| 컨테이너 메타데이터 가져오기 |모두 |소유자만 |
| 컨테이너 메타데이터 설정 |소유자만 |소유자만 |
| 컨테이너 ACL 가져오기 |소유자만 |소유자만 |
| 컨테이너 ACL 설정 |소유자만 |소유자만 |
| 컨테이너 삭제 |소유자만 |소유자만 |
| Blob 나열 |모두 |소유자만 |
| Blob 배치 |소유자만 |소유자만 |
| Blob 가져오기 |모두 |모두 |
| Blob 속성 가져오기 |모두 |모두 |
| Blob 속성 설정 |소유자만 |소유자만 |
| Blob 메타데이터 가져오기 |모두 |모두 |
| Blob 메타데이터 설정 |소유자만 |소유자만 |
| 블록 배치 |소유자만 |소유자만 |
| 블록 목록 가져오기(커밋된 블록만) |모두 |모두 |
| 블록 목록 가져오기(커밋되지 않은 블록만 또는 모든 블록) |소유자만 |소유자만 |
| 블록 목록 배치 |소유자만 |소유자만 |
| Blob 삭제 |소유자만 |소유자만 |
| Blob 복사 |소유자만 |소유자만 |
| Blob 스냅숏 |소유자만 |소유자만 |
| Blob 임대 |소유자만 |소유자만 |
| 페이지 가져오기 |소유자만 |소유자만 |
| 페이지 범위 가져오기 |모두 |모두 |
| Blob 추가 |소유자만 |소유자만 |

## <a name="next-steps"></a>다음 단계

* [Hello Azure 저장소 서비스에 대 한 인증](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)
* [공유 액세스 서명을 사용하여 액세스 위임](https://msdn.microsoft.com/library/azure/ee395415.aspx)
