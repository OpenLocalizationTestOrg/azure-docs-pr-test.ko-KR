---
title: "Java로 Azure 파일 저장소에 대 한 aaaDevelop | Microsoft Docs"
description: "어떻게 toodevelop Java 응용 프로그램 및 서비스 Azure 파일 저장소 toostore를 사용 하는 파일 데이터에 알아봅니다."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Java를 사용하여 Azure File Storage 개발
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서에서는 Java toodevelop 응용 프로그램이 나 Azure 파일 저장소 toostore 파일 데이터를 사용 하는 서비스를 사용 하 여의 hello 기본 사항을 보여 줍니다. 이 자습서에서는 간단한 콘솔 응용 프로그램 만들어져 표시 방법을 Java 및 Azure 파일 저장소를 사용 하 여 기본 동작 tooperform:

* Azure 파일 공유 만들기 및 삭제
* 디렉터리 만들기 및 삭제
* Azure 파일 공유의 파일 및 디렉터리 열거
* 파일 업로드, 다운로드 및 삭제

> [!Note]  
> SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 hello 표준 Java I/O 클래스를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램. 이 문서를 사용 하는 toowrite 응용 프로그램 hello를 사용 하 여 Azure 저장소 Java SDK hello 하는 방법을 설명 합니다 [Azure 파일 저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.

## <a name="create-a-java-application"></a>Java 응용 프로그램 만들기
toobuild hello 샘플 Java Development Kit (JDK) hello 및 hello [Azure 저장소 SDK for Java] 필요 합니다. Azure 저장소 계정도 만들었어야 합니다.

## <a name="setup-your-application-toouse-azure-file-storage"></a>사용자 응용 프로그램 toouse Azure 파일 저장소를 설정 합니다.
toouse hello Azure 저장소 Api hello tooaccess hello 저장소 서비스에서 이점을 얻을 수 하는 hello Java 파일의 문 toohello 맨 위에 다음을 추가 합니다.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 파일 저장소 toouse tooconnect tooyour Azure 저장소 계정이 필요 합니다. hello 첫 번째 단계 것 tooconfigure 사용 하는 연결 문자열 tooconnect tooyour 저장소 계정입니다. 정적 변수 toodo 정의입니다.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Your_storage_account_name 및 your_storage_account_key hello 저장소 계정에 대 한 실제 값으로 대체 합니다.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Tooan Azure 저장소 계정 연결
toouse hello 해야 tooconnect tooyour 저장소 계정 **CloudStorageAccount** 연결 문자열 tooits 전달 하 여 개체 **구문 분석** 메서드.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** 안에 try/catch 블록 throw InvalidKeyException 되므로 tooput 필요 합니다.

## <a name="create-an-azure-file-share"></a>Azure 파일 공유 만들기
Azure File Storage의 모든 파일 및 디렉터리는 **공유**라는 이름의 컨테이너 안에 있습니다. 저장소 계정은 계정 용량이 허용하는 만큼의 공유를 가질 수 있습니다. tooobtain 액세스 tooa 공유 및 그 내용을 toouse Azure 파일 저장소 클라이언트 해야합니다.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Hello Azure 파일 저장소 클라이언트를 사용 하는 참조 tooa 공유를 얻을 수 있습니다.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually hello 공유 만들기, hello를 사용 하 여 **경고는 createIfNotExists** hello CloudFileShare 개체의 메서드.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

이 시점에서 **공유** 참조 tooa 공유 이름의 보유 **sampleshare**합니다.

## <a name="delete-an-azure-file-share"></a>Azure 파일 공유 삭제
호출 hello 이루어진다는 공유 삭제 **deleteIfExists** CloudFileShare 개체에서 메서드. 다음이 샘플 코드입니다.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>디렉터리 만들기
또한 하는 대신 모든 hello 루트 디렉터리에 하위 디렉터리 내의 파일을 배치 하 여 저장소를 구성할 수 있습니다. Azure 파일 저장소에서는 허용 하는 계정에는 사용자에 따라 많은 디렉터리 만큼 toocreate를 허용 합니다. 아래 hello 코드 라는 하위 디렉터리를 만듭니다. **sampledir** hello 루트 디렉터리 아래.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>디렉터리 삭제
디렉터리의 삭제는 매우 간단한 작업입니다. 단, 여전히 파일 또는 기타 디렉터리가 포함된 디렉터리는 삭제할 수 없습니다.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Azure 파일 공유의 파일 및 디렉터리 열거
공유 내에서 파일 및 디렉터리 목록을 가져오는 것은 CloudFileDirectory 참조에서 **listFilesAndDirectories** 를 호출하여 쉽게 수행할 수 있습니다. hello 메서드에서 반복할 수 있는 ListFileItem 개체 목록을 반환 합니다. 예를 들어, hello 다음 코드는 나열 파일 및 디렉터리 hello 루트 디렉터리 안에 합니다.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>파일 업로드
공유 이상 매우 hello에 포함 되어 있는 Azure 파일, 루트 디렉터리 파일이 있을 수 있습니다. 이 섹션에서는 tooupload hello에 대 한 로컬 저장소에서 파일 루트 디렉터리를 공유 하는 방법을 설명 합니다.

파일 업로드 hello 첫 번째 단계에는 tooobtain 상주해 야 참조 toohello 디렉터리입니다. 이렇게 하려면 호출 hello **getRootDirectoryReference** hello 공유 개체의 메서드.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Hello 공유의 참조 toohello 루트 디렉터리를가지고 코드 다음 hello를 사용 하 여 파일을 업로드할 수 있습니다.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>파일 다운로드
Azure 파일 저장소에 대해 수행한 작업 보다 빈번한 hello 중 하나 toodownload 파일입니다. 다음 예제는 hello, hello 코드 SampleFile.txt 다운로드 하 고 해당 내용을 표시 합니다.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>파일 삭제
다른 일반적인 Azure File Storage 작업은 파일의 삭제입니다. hello 다음 코드 파일을 삭제 하 라는 디렉터리 내에 저장 되어 SampleFile.txt 라는 **sampledir**합니다.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>다음 단계
다른 Azure 저장소 Api에 대 한 자세한 toolearn를 원하는 경우 이러한 링크를 따르십시오.

* [Java 개발자용 Azure](/java/azure)/)
* [Java용 Azure 저장소 SDK](https://github.com/azure/azure-storage-java)
* [Android용 Azure Storage SDK](https://github.com/azure/azure-storage-android)
* [Azure 저장소 클라이언트 SDK 참조](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Storage 서비스 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)