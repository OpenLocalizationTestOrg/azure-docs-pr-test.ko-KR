---
title: "Azure 저장소에 blob의 읽기 전용 스냅숏 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 주어진 시점에 blob 데이터를 blob tooback의 스냅숏 합니다. 하 고 스냅숏을 요금을 청구 하는 방법 이해 toouse toominimize 용량 요금을 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Blob 스냅숏 만들기

스냅숏은 특정 시점에 생성된 Blob의 읽기 전용 버전입니다. 스냅숏은 blob를 백업하는데 유용 합니다. 스냅숏을 만든 후에 읽기, 복사 또는 삭제할 수 있지만 수정할 수 없습니다.

Blob의 스냅숏을 기본 blob와 동일한 tooits 이면 해당 hello blob를 제외 하 고 URI에는 **DateTime** 값 toohello blob URI tooindicate hello 이루어진 지정 시간은 hello에 스냅숏 추가 합니다. 예를 들어, 페이지 blob URI가 `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello 스냅숏 URI는 너무 유사`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`합니다.

> [!NOTE]
> 모든 스냅숏이 hello 기본 blob URI를 공유 합니다. hello 기본 blob와 hello 스냅숏 차이 추가 hello만 hello **DateTime** 값입니다.
>

Blob 하나에 여러 스냅숏이 있을 수 있습니다. 스냅숏을 명시적으로 삭제하기 전까지 유지됩니다. 스냅숏은 해당 기본 Blob보다 수명이 길 수 없습니다. 기본 blob tootrack hello와 연결 된 hello 스냅숏을 열거할 수 현재 스냅숏을 합니다.

Blob의 스냅숏을 만들 때 hello blob의 시스템 속성은 hello로 복사한 toohello 스냅숏 동일한 값입니다. hello 기본 blob의 메타 데이터 스냅숏을 만들 때 hello에 대 한 별도 메타 데이터를 지정 하지 않으면 복사 된 toohello 스냅숏을 이기도 합니다.

Hello 기본 blob와 연결 된 모든 임대 hello 스냅숏 영향을 주지 않습니다. 스냅숏에 대해 임대를 가져올 수 없습니다.

VHD 파일이 사용 되는 toostore hello에 대 한 현재 정보 및 VM 디스크에 대 한 상태입니다. Hello VM 내에서 디스크를 분리 hello VM 종료 한 다음 해당 VHD 파일의 스냅숏을 수 있습니다. 해당 스냅숏 파일을 사용할 수 이후 tooretrieve hello VHD 시간 해당 시점에 파일 및 hello VM을 다시 만듭니다.

Hello 저장소 계정의 저장소 서비스 암호화 SSE () 사용 하는 경우는 hello에서 blob이 있는 다음 해당 blob의 스냅숏을 휴지 암호화 됩니다.

## <a name="create-a-snapshot"></a>스냅숏 만들기
hello 다음 코드 예제에서는 방법을 사용 하 여 스냅숏 toocreate hello [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)합니다. 이 예제에서는 생성 될 때 hello 스냅숏에 대 한 추가 메타 데이터를 지정 합니다.

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a>스냅숏 복사
Blob 및 스냅숏 관련 복사 작업에는 다음 규칙이 적용됩니다.

* 기본 Blob에 대해 스냅숏을 복사할 수 있습니다. Hello 기본 blob의 스냅숏 toohello 위치를 홍보 하 여 이전 버전의 blob 복원할 수 있습니다. hello 스냅숏은 그대로 유지 하지만 hello 기본 blob에 쓰기 가능한 스냅숏 hello 덮어쓰여집니다.
* 다른 이름 사용 하 여 스냅숏 tooa 대상 blob를 복사할 수 있습니다. hello 결과 대상 blob에 쓰기 가능한 blob 이며 스냅숏이 아닙니다.
* 원본 blob 복사 되 면 hello 원본 blob의 스냅숏도 모두 복사한 toohello 대상 않습니다. 복사본으로 대상 blob을 덮어씀을 hello 원래 대상 blob와 연결 된 모든 스냅숏은 그대로 유지 됩니다.
* 블록 blob의 스냅숏을 만들 때 hello blob의 커밋된 블록 목록 복사한 toohello 스냅숏 이기도 합니다. 커밋되지 않은 블록은 복사되지 않습니다.

## <a name="specify-an-access-condition"></a>액세스 조건 지정
호출 하는 경우 [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], hello 스냅숏이 생성 된 조건이 충족 될 경우에 되도록 액세스 조건을 지정할 수 있습니다. toospecify 액세스 조건을 사용 하 여 hello [AccessCondition] [ dotnet_AccessCondition] 매개 변수입니다. Hello 지정한 조건이 충족 되지 않으면, hello 스냅숏이 만들어지지 않으면 및 hello Blob 서비스가 상태 코드를 반환 하는 경우 [HTTPStatusCode][dotnet_HTTPStatusCode]합니다. PreconditionFailed 합니다.

## <a name="delete-snapshots"></a>스냅숏 삭제
Hello 스냅숏을 삭제 하지 않는 한 스냅숏과 함께 blob을 삭제할 수 없습니다. 스냅숏을 개별적으로 삭제 하거나 hello 원본 blob 삭제 될 때 모든 스냅숏을 삭제 되도록 지정할 수 있습니다. Toodelete 스냅숏이 있는 blob을 시도 하면 오류가 발생 합니다.

코드 예제에서 보여 주는 방법을 다음 hello toodelete blob와 스냅숏이.net, 여기서 `blockBlob` 형식의 개체가 [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Azure 프리미엄 저장소를 사용한 스냅숏
프리미엄 저장소 스냅숏을 사용 하는 경우 규칙에 따라 hello 적용 됩니다.

* 프리미엄 저장소 계정에 페이지 blob 당 스냅숏 hello 최대 수는 100입니다. 해당 제한을 초과 하는 hello 스냅숏 Blob 작업 반환 오류 코드 409 (`SnapshotCountExceeded`).
* 프리미엄 저장소 계정의 페이지 Blob 스냅숏은 10분마다 한 번 생성할 수 있습니다. Hello 스냅숏 Blob 작업 오류 코드 409 반환 해당 속도 초과 하는 경우 (`SnapshotOperationRateExceeded`).
* 스냅숏을 tooread hello 계정에서 Blob 복사 작업 toocopy hello 스냅숏 tooanother 페이지 blob를 사용할 수 있습니다. hello 복사 작업에 대 한 hello 대상 blob에 기존 스냅숏이 없어야 합니다. Hello 대상 blob는 스냅숏, 한 경우 오류 코드 409를 반환 하는 hello Blob 복사 작업 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>절대 URI tooa 스냅숏 hello를 반환 합니다.
이 C# 코드 예제에서는 스냅숏을 만들고 hello 작성 hello 기본 위치에 대 한 절대 URI입니다.

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>스냅숏 요금 청구 방법 이해
Blob의 읽기 전용 복사본 인 스냅숏을 만들면 추가 데이터 저장소 요금 tooyour 계정에서 발생할 수 있습니다. 응용 프로그램을 디자인할 때 중요 한 toobe 비용을 최소화할 수 있도록 이러한 비용 수 발생 하는 방법을 인식 합니다.

### <a name="important-billing-considerations"></a>청구 관련 중요 고려 사항
hello 목록 다음에 스냅숏을 만들 때 주요 사항을 tooconsider를 포함 합니다.

* 저장소 계정 hello blob 또는 스냅숏의 hello 되었든 관계 없이 개별 블록 또는 페이지에 대 한 요금을 발생 시킵니다. 계정 기반는 hello blob를 업데이트할 때까지 blob와 연결 된 스냅숏 위한 추가 비용이 발생 하지 않습니다. Hello 기본 blob를 업데이트 한 후 해당 스냅숏에서 모델과. 이 경우 hello 고유 블록이 나 페이지에 각 blob 또는 스냅숏에 대 한 요금이 청구 됩니다.
* 블록 Blob 내의 블록을 바꾸고 나면 해당 블록은 이후부터 고유 블록으로 요금이 청구됩니다. 이 hello 블록의 블록 ID를 동일 하 고 동일한 hello hello 하는 경우에 마찬가지 hello 스냅숏의 데이터를 했습니다. Hello 블록이 커밋된 후 다시, 모든 스냅숏의 바뀌므로 모델과 하 고 해당 데이터에 대 한 청구 됩니다. 마찬가지 페이지에 대 한 동일한 데이터로 업데이트 하는 페이지 blob의 번호입니다.
* Hello를 호출 하 여 블록 blob를 교체 [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], 또는 [UploadFromByteArray] [ dotnet_UploadFromByteArray] 메서드 hello blob에서 블록을 모두 바꿉니다. 해당 blob와 연결 된 스냅숏이 있는 경우에 hello 기본 blob와 스냅숏의 모든 블록을 이제 분기 하 고 모든 hello 블록에에서 대 한 청구 됩니다. Hello 데이터 hello 기본 blob와 hello 스냅숏에 동일 하 게 유지 하는 경우에 마찬가지입니다.
* hello Azure Blob 서비스는 동일한 데이터를 포함 하는 두 개의 블록 여부 수단 toodetermine가 필요가 없습니다. 업로드 및 커밋되는 각 블록은 고유한 것으로 간주, 동일한 블록 id입니다. 동일한 데이터 및 hello hello에 경우에 고유한 블록에 대 한 비용 발생을 이므로 추가 비용이 발생 하 고 고유한 블록이 추가적으로 인해 스냅숏이 포함 된 blob를 업데이트 하는 중요 한 tooconsider 합니다.

### <a name="minimize-cost-with-snapshot-management"></a>스냅숏 관리 비용을 최소화

전자 메일로 신중 하 게 관리 하는 것이 좋습니다 tooavoid 추가 비용이 있습니다. Toohelp 스냅숏의 hello 저장소에서 발생 하는 hello 비용을 최소화 하는 다음 모범 사례를 따르면 됩니다.

* 삭제 하 고 blob에 연결 된 hello blob를 업데이트할 때마다 응용 프로그램 디자인에서 스냅숏을 유지 하도록 요청 하지 않는 동일한 데이터로 업데이트 하는 경우에 스냅숏을 다시 만듭니다. 삭제 하 고 다시 hello blob의 스냅숏 만들기, hello blob 및 스냅숏을 분기 하지 않는 것을 확인할 수 있습니다.
* Blob의 스냅숏을 유지 관리할 때는 호출 하지 마세요. [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], 또는 [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob입니다. 이러한 메서드를 대체 하 여 모든 사용자 기본 blob와 해당 스냅숏 toodiverge 현저 하 게 발생 하는 hello blob에 블록 hello 합니다. 대신, 업데이트 가능한 가장 적은 수의 블록을 hello를 사용 하 여 hello [PutBlock] [ dotnet_PutBlock] 및 [PutBlockList] [ dotnet_PutBlockList] 메서드.

### <a name="snapshot-billing-scenarios"></a>스냅숏 청구 시나리오
다음 시나리오는 hello 블록 blob 및 그 스냅숏에 대 한 비용 발생 하는 방법을 보여 줍니다.

**시나리오 1**

시나리오 1의에서 hello 기본 blob 업데이트 되지 않은 hello 스냅숏이 만들어진 후 하므로 고유 블록 1, 2 및 3에 대해서만 청구 됩니다.

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**시나리오 2**

시나리오 2에서는 hello 기본 blob가 업데이트 된 있지만 hello 스냅숏이 없습니다. 블록 3 업데이트 된 하 고 있는 경우에 동일한 데이터 hello 및 동일한 ID hello에 하지 블록 3 hello 스냅숏의 hello 합니다. 결과적으로, hello 계정에 4 개의 블록에 대 한 청구 됩니다.

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**시나리오 3**

3 시나리오에서는 hello 기본 blob가 업데이트 되지만 hello 스냅숏이 없습니다. 블록 3이 hello 기본 blob에 블록 4로 교체 되지만 hello 스냅숏 여전히 블록 3이 남아 있습니다. 결과적으로, hello 계정에 4 개의 블록에 대 한 청구 됩니다.

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**시나리오 4**

시나리오 4 hello 기본 blob은 완전히 업데이트 하 고 원래 블록 모두 달라졌습니다. 결과적으로, hello 계정 전체 8 개의 블록에 대 한 요금이 부과 됩니다. 이 시나리오는 같은 업데이트 메서드를 사용 하는 경우에 발생할 수 있습니다 [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], 또는 [UploadFromByteArray][dotnet_UploadFromByteArray]이러한 메서드를 대체 하는 모든 blob의 내용을 hello 때문에 있습니다.

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>다음 단계

* VM(가상 컴퓨터) 디스크 스냅숏 사용에 대한 자세한 내용은 [증분 스냅숏을 사용하여 Azure 관리되지 않는 VM 디스크 백업](storage-incremental-snapshots.md)에서 확인할 수 있습니다.

* Blob Storage를 사용하는 추가 코드 예제는 [Azure 코드 샘플](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)을 참조하세요. 샘플 응용 프로그램을 다운로드 하 고 실행 하거나 GitHub에서 hello 코드를 찾아보려면 수 있습니다.

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx