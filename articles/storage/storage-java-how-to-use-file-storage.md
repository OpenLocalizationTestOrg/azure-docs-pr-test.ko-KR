---
title: "Java를 사용하여 Azure File Storage 개발 | Microsoft Docs"
description: "Azure File Storage를 사용하여 파일 데이터를 저장하는 Java 응용 프로그램 및 서비스를 개발하는 방법을 알아봅니다."
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
ms.openlocfilehash: 16924599e49990265e07f7a58613756d93c46942
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="0edd4-103">Java를 사용하여 Azure File Storage 개발</span><span class="sxs-lookup"><span data-stu-id="0edd4-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="0edd4-104">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="0edd4-104">About this tutorial</span></span>
<span data-ttu-id="0edd4-105">이 자습서에서는 Java를 사용하여 Azure File Storage를 사용하여 파일 데이터를 저장하는 응용 프로그램이나 서비스를 개발하는 데 필요한 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="0edd4-106">즉 간단한 콘솔 응용 프로그램을 만들고, Java 및 Azure File Storage를 통해 기본 동작을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="0edd4-107">Azure 파일 공유 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0edd4-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="0edd4-108">디렉터리 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0edd4-108">Create and delete directories</span></span>
* <span data-ttu-id="0edd4-109">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="0edd4-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="0edd4-110">파일 업로드, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0edd4-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="0edd4-111">Azure File Storage는 SMB를 통해 액세스할 수 있기 때문에 표준 Java I/O 클래스를 사용하여 Azure 파일 공유에 액세스하는 간단한 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="0edd4-112">이 문서에서는 [Azure File Storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api)를 사용하여 Azure File Storage와 통신하는 Azure Storage Java SDK를 사용하는 응용 프로그램을 작성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="0edd4-113">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0edd4-113">Create a Java application</span></span>
<span data-ttu-id="0edd4-114">샘플을 빌드하려면 JDK(Java 개발 키트)와 [Java용 Azure 저장소 SDK][]가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="0edd4-115">Azure 저장소 계정도 만들었어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="0edd4-116">Azure File Storage를 사용하도록 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="0edd4-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="0edd4-117">Azure 저장소 API를 사용하려면 저장소 서비스를 액세스하고자 하는 위치에서 Java 파일의 맨 위에 다음 명령문을 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="0edd4-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="0edd4-118">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="0edd4-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="0edd4-119">Azure File Storage를 사용하려면 Azure Storage 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="0edd4-120">첫 번째 단계는 저장소 계정에 연결하는 데 사용할 연결 문자열을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="0edd4-121">이를 위해 정적 변수를 정의해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="0edd4-122">your_storage_account_name과 your_storage_account_key를 자신의 저장소 계정에 대한 실제 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="0edd4-123">Azure 저장소 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="0edd4-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="0edd4-124">저장소 계정에 연결하려면, **CloudStorageAccount** 개체를 사용하여 **구문 분석** 메서드로 연결 문자열을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="0edd4-125">**CloudStorageAccount.parse** 는 InvalidKeyException을 발생시키므로 try/catch 블록 안에 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="0edd4-126">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="0edd4-126">Create an Azure File share</span></span>
<span data-ttu-id="0edd4-127">Azure File Storage의 모든 파일 및 디렉터리는 **공유**라는 이름의 컨테이너 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="0edd4-128">저장소 계정은 계정 용량이 허용하는 만큼의 공유를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="0edd4-129">공유 및 그 내용에 액세스하려면 Azure File Storage 클라이언트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="0edd4-130">Azure File Storage 클라이언트를 사용하면 공유에 대한 참조를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="0edd4-131">공유를 실제로 만들고자 한다면 CloudFileShare 개체의 **createIfNotExists** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="0edd4-132">이 시점에서, **공유**는 **sampleshare**라는 이름의 공유에 대한 참조를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="0edd4-133">Azure 파일 공유 삭제</span><span class="sxs-lookup"><span data-stu-id="0edd4-133">Delete an Azure File share</span></span>
<span data-ttu-id="0edd4-134">공유 삭제는 CloudFileShare 개체에서 **deleteIfExists** 메서드를 호출하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="0edd4-135">다음이 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="0edd4-136">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="0edd4-136">Create a directory</span></span>
<span data-ttu-id="0edd4-137">또한 루트 디렉터리에 이들 모두를 포함하는 대신 하위 디렉터리 내에서 파일을 배치하여 저장소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="0edd4-138">Azure File Storage를 사용하면 계정이 허용하는 만큼 많은 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="0edd4-139">아래 코드는 루트 디렉터리 아래에 **sampledir** 라는 이름의 하위 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="0edd4-140">디렉터리 삭제</span><span class="sxs-lookup"><span data-stu-id="0edd4-140">Delete a directory</span></span>
<span data-ttu-id="0edd4-141">디렉터리의 삭제는 매우 간단한 작업입니다. 단, 여전히 파일 또는 기타 디렉터리가 포함된 디렉터리는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="0edd4-142">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="0edd4-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="0edd4-143">공유 내에서 파일 및 디렉터리 목록을 가져오는 것은 CloudFileDirectory 참조에서 **listFilesAndDirectories** 를 호출하여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="0edd4-144">메서드는 반복할 수 있는 ListFileItem 개체 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="0edd4-145">한 예로, 다음 코드는 파일 및 디렉터리를 루트 디렉터리 안에 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="0edd4-146">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="0edd4-146">Upload a file</span></span>
<span data-ttu-id="0edd4-147">Azure 파일 공유에는 파일이 상주할 수 있는 최소한의 루트 디렉터리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="0edd4-148">이 섹션에서는 로컬 저장소에서 공유의 루트 디렉터리로 파일을 업로드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="0edd4-149">파일을 업로드하는 첫 번째 단계는 상주해야 하는 디렉터리에 대한 참조를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="0edd4-150">공유 개체의 **getRootDirectoryReference** 메서드를 호출하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="0edd4-151">이제 공유의 루트 디렉터리에 대한 참조를 가졌으므로 다음 코드를 사용하여 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="0edd4-152">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="0edd4-152">Download a file</span></span>
<span data-ttu-id="0edd4-153">Azure File Storage에 대해 가장 자주 수행하게 될 작업 중 하나는 파일의 다운로드입니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="0edd4-154">다음 예제에서 코드가 SampleFile.txt를 다운로드하고 그 내용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="0edd4-155">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="0edd4-155">Delete a file</span></span>
<span data-ttu-id="0edd4-156">다른 일반적인 Azure File Storage 작업은 파일의 삭제입니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="0edd4-157">다음 코드는 **sampledir**라는 이름의 디렉터리 안에 저장된 SampleFile.txt라는 이름의 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0edd4-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="0edd4-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0edd4-158">Next steps</span></span>
<span data-ttu-id="0edd4-159">다른 Azure 저장소 API에 대해 더 알아보려면 다음 링크를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="0edd4-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="0edd4-160">Java 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="0edd4-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="0edd4-161">Java용 Azure 저장소 SDK</span><span class="sxs-lookup"><span data-stu-id="0edd4-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="0edd4-162">Android용 Azure Storage SDK</span><span class="sxs-lookup"><span data-stu-id="0edd4-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="0edd4-163">Azure 저장소 클라이언트 SDK 참조</span><span class="sxs-lookup"><span data-stu-id="0edd4-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="0edd4-164">Azure Storage 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="0edd4-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="0edd4-165">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="0edd4-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="0edd4-166">AzCopy 명령줄 유틸리티로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="0edd4-166">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)