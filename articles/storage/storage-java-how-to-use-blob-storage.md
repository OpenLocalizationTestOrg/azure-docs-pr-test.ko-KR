---
title: "aaaHow toouse Java에서 Azure Blob 저장소 (개체 저장소) | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>어떻게 toouse Java에서 Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>개요
Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다. Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.

이 문서에서는 보여 tooperform 일반적인 시나리오를 사용 하 여 Microsoft Azure Blob 저장소를 hello 하는 방법을 합니다. hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Java 용 Azure 저장소 SDK][Azure Storage SDK for Java]합니다. hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다. Blob에 대 한 자세한 내용은 참조 hello [다음 단계](#Next-Steps) 섹션.

> [!NOTE]
> SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다. 자세한 내용은 참조 hello [Android 용 Azure 저장소 SDK][Azure Storage SDK for Android]합니다.
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Java 응용 프로그램 만들기
이 문서에서는 Java 응용 프로그램 내에서 로컬로 또는 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.

toodo tooinstall, 나오는 Java Development Kit (JDK) hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다. 그렇게 않은 후에 hello 최소 요구 사항 및 종속성 hello에 나열 되어 있는 개발 시스템 맞는 tooverify 해야 합니다 [Java 용 Azure 저장소 SDK] [ Azure Storage SDK for Java] GitHub의 리포지토리 합니다. 시스템에 이러한 요구 사항을 충족 하는 경우 다운로드 하 고 해당 리포지토리 로부터 시스템에 hello Java 용 Azure 저장소 라이브러리를 설치 하기 위한 hello 지침을 따를 수 있습니다. 이러한 작업을 완료 되 면이 문서의 hello 예제를 사용 하는 Java 응용 프로그램 수 toocreate 됩니다.

## <a name="configure-your-application-tooaccess-blob-storage"></a>사용자 응용 프로그램 tooaccess Blob 저장소 구성
Hello toouse hello Azure 저장소 Api tooaccess blob 저장할 hello Java 파일 맨 문을 toohello 가져오기 뒤에 추가 합니다.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다. 형식에 따라, 사용자의 저장소 계정 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 입력 하 고 hello에 나열 된 hello 저장소 계정의 기본 액세스 키를 hello 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다. hello 다음 예제 방법을 정적 필드 toohold hello 연결 문자열을 선언할 수 있습니다.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Microsoft Azure에서 역할 내에서 실행 하는 응용 프로그램을이 문자열 hello 서비스 구성 파일에 저장 될 수 *ServiceConfiguration.cscfg*, 호출 toohello로 액세스할 수 있습니다 및  **RoleEnvironment.getConfigurationSettings** 메서드. hello 다음 예제에서는 가져옵니다 hello 연결 문자열에서는 **설정** 라는 요소 *StorageConnectionString* hello 서비스 구성 파일에 있습니다.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.

## <a name="create-a-container"></a>컨테이너 만들기
**CloudBlobClient** 개체를 사용하면 컨테이너 및 Blob에 대한 참조 개체를 가져올 수 있습니다. hello 다음 코드에서는 **CloudBlobClient** 개체입니다.

> [!NOTE]
> 다른 방법은 toocreate **CloudStorageAccount** 개체, 자세한 내용은 참조 **CloudStorageAccount** hello에 [Azure 저장소 클라이언트 SDK 참조]합니다.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

사용 하 여 hello **CloudBlobClient** tooget toouse 원하는 참조 toohello 컨테이너 개체입니다. Hello로 존재 하지 않는 경우 hello 컨테이너를 만들 수 있습니다 **경고는 createIfNotExists** 메서드를 그렇지 않으면 hello 기존 컨테이너를 반환 합니다. 기본적으로 hello 새 컨테이너는 private 이므로 (마찬가지로 이전 버전) 저장소 액세스 키를 지정 해야이 컨테이너에서 blob toodownload 합니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>옵션: 공용 액세스에 대한 컨테이너 구성
기본적으로 개인 액세스에 대 한 컨테이너의 사용 권한을 구성 하지만 인터넷 hello에 컨테이너의 권한 tooallow 공용, 읽기 전용 액세스 모든 사용자가 쉽게 구성할 수 있습니다.

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
tooupload 파일 tooa blob 컨테이너 참조를 가져오고 tooget blob 참조를 사용 합니다. Blob 참조를 만든 후 모든 스트림을 hello blob 참조에서 업로드를 호출 하 여 업로드할 수 있습니다. 이 작업을 존재 하지 못하거나 헤더가 있으면 덮어쓰기 hello blob을 만들어집니다. 아래의 코드 예제는 hello이를 보여주며, 해당 hello 컨테이너 이미 만들어진 것으로 가정 합니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
컨테이너에서 hello blob toolist tooupload blob를 했던 것 처럼 먼저를 컨테이너 참조를 가져옵니다. Hello 컨테이너를 사용할 수 있습니다 **listBlobs** 메서드는 **에 대 한** 루프입니다. hello 다음 코드에서는 출력 hello 컨테이너 toohello 콘솔에서 각 blob의 Uri입니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

이름에 대한 경로 정보를 사용하여 Blob 이름을 지정할 수 있습니다. 이렇게 하면 기존 파일 시스템과 같이 구성 및 트래버스할 수 있는 가상 디렉터리 구조를 만듭니다. Hello 디렉터리 구조는 가상-hello만 Blob 저장소에서 사용할 수 있는 리소스가 컨테이너 및 blob note 합니다. 그러나 hello 클라이언트 라이브러리에서 제공 된 **CloudBlobDirectory** toorefer tooa 가상 디렉터리 개체를 이러한 방식으로 구성 된 blob을 사용 하 여 처리 hello 프로세스를 간소화 합니다.

예를 들어 이름이 "photos"인 컨테이너가 있는 경우 이 컨테이너에서 이름이 "rootphoto1", "2010/photo1", "2010/photo2" 및 "2011/photo1"인 Blob을 업로드할 수 있습니다. 이렇게 하면 사항이 hello "2010"과 "2011" hello "사진" 컨테이너 내에서 가상 디렉터리입니다. 호출 하는 경우 **listBlobs** hello "사진" 컨테이너를 반환 하는 hello 컬렉션에 포함 됩니다 **CloudBlobDirectory** 및 **CloudBlob** hello를 나타내는 개체 디렉터리와 hello 최상위 수준에 포함 된 blob를 제공 합니다. 이 경우에는 디렉터리 "2010", "2011" 및 사진 "rootphoto1"이 반환됩니다. Hello를 사용할 수 있습니다 **instanceof** 연산자 toodistinguish 이러한 개체입니다.

필요에 따라 매개 변수 toohello에 전달할 수 있습니다 **listBlobs** hello로 메서드 **useFlatBlobListing** tootrue 매개 변수를 설정 합니다. 그러면 모든 Blob이 디렉터리에 상관없이 반환됩니다. 자세한 내용은 참조 **CloudBlobContainer.listBlobs** hello에 [Azure 저장소 클라이언트 SDK 참조]합니다.

## <a name="download-a-blob"></a>Blob 다운로드
toodownload blob hello 순서 tooget blob 참조에에서 blob을 업로드 하기 위한 수행한 것 처럼 동일한 단계를 수행 합니다. 예제를 업로드 하는 hello, hello blob 개체에 대해 업로드를 호출 합니다. 다음 예제는 hello, 다운로드 tootransfer hello blob 내용을 tooa stream 개체와 같은 호출는 **FileOutputStream** toopersist hello blob tooa 로컬 파일을 사용할 수 있습니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Blob 삭제
toodelete blob을 blob 가져오기 참조 하 고, 호출 **deleteIfExists**합니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Blob 컨테이너 삭제
마지막으로, blob 컨테이너 toodelete 가져오기 blob 컨테이너 참조 및 호출 **deleteIfExists**합니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>다음 단계
Blob 저장소의 기본 사항 hello를 알아보았습니다 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.

* [Java용 Azure Storage SDK][Azure Storage SDK for Java]
* [Azure 저장소 클라이언트 SDK 참조][Azure 저장소 클라이언트 SDK 참조]
* [Azure Storage REST API][Azure Storage REST API]
* [Azure Storage 팀 블로그][Azure Storage Team Blog]

자세한 내용은 참고 항목 hello [Java 개발자 센터](/develop/java/)합니다.

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 저장소 클라이언트 SDK 참조]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
