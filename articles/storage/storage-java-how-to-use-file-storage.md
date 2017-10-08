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
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="af19d-103">Java를 사용하여 Azure File Storage 개발</span><span class="sxs-lookup"><span data-stu-id="af19d-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="af19d-104">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="af19d-104">About this tutorial</span></span>
<span data-ttu-id="af19d-105">이 자습서에서는 Java toodevelop 응용 프로그램이 나 Azure 파일 저장소 toostore 파일 데이터를 사용 하는 서비스를 사용 하 여의 hello 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="af19d-106">이 자습서에서는 간단한 콘솔 응용 프로그램 만들어져 표시 방법을 Java 및 Azure 파일 저장소를 사용 하 여 기본 동작 tooperform:</span><span class="sxs-lookup"><span data-stu-id="af19d-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="af19d-107">Azure 파일 공유 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="af19d-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="af19d-108">디렉터리 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="af19d-108">Create and delete directories</span></span>
* <span data-ttu-id="af19d-109">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="af19d-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="af19d-110">파일 업로드, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="af19d-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="af19d-111">SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 hello 표준 Java I/O 클래스를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="af19d-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="af19d-112">이 문서를 사용 하는 toowrite 응용 프로그램 hello를 사용 하 여 Azure 저장소 Java SDK hello 하는 방법을 설명 합니다 [Azure 파일 저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.</span><span class="sxs-lookup"><span data-stu-id="af19d-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="af19d-113">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="af19d-113">Create a Java application</span></span>
<span data-ttu-id="af19d-114">toobuild hello 샘플 Java Development Kit (JDK) hello 및 hello [Azure 저장소 SDK for Java] 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="af19d-115">Azure 저장소 계정도 만들었어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="af19d-116">사용자 응용 프로그램 toouse Azure 파일 저장소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="af19d-117">toouse hello Azure 저장소 Api hello tooaccess hello 저장소 서비스에서 이점을 얻을 수 하는 hello Java 파일의 문 toohello 맨 위에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="af19d-118">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="af19d-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="af19d-119">Azure 파일 저장소 toouse tooconnect tooyour Azure 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="af19d-120">hello 첫 번째 단계 것 tooconfigure 사용 하는 연결 문자열 tooconnect tooyour 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="af19d-121">정적 변수 toodo 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="af19d-122">Your_storage_account_name 및 your_storage_account_key hello 저장소 계정에 대 한 실제 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="af19d-123">Tooan Azure 저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="af19d-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="af19d-124">toouse hello 해야 tooconnect tooyour 저장소 계정 **CloudStorageAccount** 연결 문자열 tooits 전달 하 여 개체 **구문 분석** 메서드.</span><span class="sxs-lookup"><span data-stu-id="af19d-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="af19d-125">**CloudStorageAccount.parse** 안에 try/catch 블록 throw InvalidKeyException 되므로 tooput 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="af19d-126">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="af19d-126">Create an Azure File share</span></span>
<span data-ttu-id="af19d-127">Azure File Storage의 모든 파일 및 디렉터리는 **공유**라는 이름의 컨테이너 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="af19d-128">저장소 계정은 계정 용량이 허용하는 만큼의 공유를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="af19d-129">tooobtain 액세스 tooa 공유 및 그 내용을 toouse Azure 파일 저장소 클라이언트 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="af19d-130">Hello Azure 파일 저장소 클라이언트를 사용 하는 참조 tooa 공유를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="af19d-131">tooactually hello 공유 만들기, hello를 사용 하 여 **경고는 createIfNotExists** hello CloudFileShare 개체의 메서드.</span><span class="sxs-lookup"><span data-stu-id="af19d-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="af19d-132">이 시점에서 **공유** 참조 tooa 공유 이름의 보유 **sampleshare**합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="af19d-133">Azure 파일 공유 삭제</span><span class="sxs-lookup"><span data-stu-id="af19d-133">Delete an Azure File share</span></span>
<span data-ttu-id="af19d-134">호출 hello 이루어진다는 공유 삭제 **deleteIfExists** CloudFileShare 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="af19d-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="af19d-135">다음이 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-135">Here's sample code that does that.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="af19d-136">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="af19d-136">Create a directory</span></span>
<span data-ttu-id="af19d-137">또한 하는 대신 모든 hello 루트 디렉터리에 하위 디렉터리 내의 파일을 배치 하 여 저장소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="af19d-138">Azure 파일 저장소에서는 허용 하는 계정에는 사용자에 따라 많은 디렉터리 만큼 toocreate를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="af19d-139">아래 hello 코드 라는 하위 디렉터리를 만듭니다. **sampledir** hello 루트 디렉터리 아래.</span><span class="sxs-lookup"><span data-stu-id="af19d-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="af19d-140">디렉터리 삭제</span><span class="sxs-lookup"><span data-stu-id="af19d-140">Delete a directory</span></span>
<span data-ttu-id="af19d-141">디렉터리의 삭제는 매우 간단한 작업입니다. 단, 여전히 파일 또는 기타 디렉터리가 포함된 디렉터리는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="af19d-142">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="af19d-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="af19d-143">공유 내에서 파일 및 디렉터리 목록을 가져오는 것은 CloudFileDirectory 참조에서 **listFilesAndDirectories** 를 호출하여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="af19d-144">hello 메서드에서 반복할 수 있는 ListFileItem 개체 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="af19d-145">예를 들어, hello 다음 코드는 나열 파일 및 디렉터리 hello 루트 디렉터리 안에 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="af19d-146">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="af19d-146">Upload a file</span></span>
<span data-ttu-id="af19d-147">공유 이상 매우 hello에 포함 되어 있는 Azure 파일, 루트 디렉터리 파일이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="af19d-148">이 섹션에서는 tooupload hello에 대 한 로컬 저장소에서 파일 루트 디렉터리를 공유 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="af19d-149">파일 업로드 hello 첫 번째 단계에는 tooobtain 상주해 야 참조 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="af19d-150">이렇게 하려면 호출 hello **getRootDirectoryReference** hello 공유 개체의 메서드.</span><span class="sxs-lookup"><span data-stu-id="af19d-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="af19d-151">Hello 공유의 참조 toohello 루트 디렉터리를가지고 코드 다음 hello를 사용 하 여 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="af19d-152">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="af19d-152">Download a file</span></span>
<span data-ttu-id="af19d-153">Azure 파일 저장소에 대해 수행한 작업 보다 빈번한 hello 중 하나 toodownload 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="af19d-154">다음 예제는 hello, hello 코드 SampleFile.txt 다운로드 하 고 해당 내용을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="af19d-155">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="af19d-155">Delete a file</span></span>
<span data-ttu-id="af19d-156">다른 일반적인 Azure File Storage 작업은 파일의 삭제입니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="af19d-157">hello 다음 코드 파일을 삭제 하 라는 디렉터리 내에 저장 되어 SampleFile.txt 라는 **sampledir**합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="af19d-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af19d-158">Next steps</span></span>
<span data-ttu-id="af19d-159">다른 Azure 저장소 Api에 대 한 자세한 toolearn를 원하는 경우 이러한 링크를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="af19d-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="af19d-160">Java 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="af19d-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="af19d-161">Java용 Azure 저장소 SDK</span><span class="sxs-lookup"><span data-stu-id="af19d-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="af19d-162">Android용 Azure Storage SDK</span><span class="sxs-lookup"><span data-stu-id="af19d-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="af19d-163">Azure 저장소 클라이언트 SDK 참조</span><span class="sxs-lookup"><span data-stu-id="af19d-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="af19d-164">Azure Storage 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="af19d-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="af19d-165">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="af19d-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="af19d-166">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="af19d-166">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
