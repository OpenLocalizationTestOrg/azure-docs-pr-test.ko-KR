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
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="42d52-103">어떻게 toouse Java에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="42d52-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="42d52-104">개요</span><span class="sxs-lookup"><span data-stu-id="42d52-104">Overview</span></span>
<span data-ttu-id="42d52-105">Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="42d52-106">Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="42d52-107">Blob 저장소 참조 tooas 개체 저장소 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="42d52-108">이 문서에서는 보여 tooperform 일반적인 시나리오를 사용 하 여 Microsoft Azure Blob 저장소를 hello 하는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="42d52-109">hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Java 용 Azure 저장소 SDK][Azure Storage SDK for Java]합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="42d52-110">hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="42d52-111">Blob에 대 한 자세한 내용은 참조 hello [다음 단계](#Next-Steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="42d52-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="42d52-112">SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="42d52-113">자세한 내용은 참조 hello [Android 용 Azure 저장소 SDK][Azure Storage SDK for Android]합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="42d52-114">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="42d52-114">Create a Java application</span></span>
<span data-ttu-id="42d52-115">이 문서에서는 Java 응용 프로그램 내에서 로컬로 또는 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="42d52-116">toodo tooinstall, 나오는 Java Development Kit (JDK) hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="42d52-117">그렇게 않은 후에 hello 최소 요구 사항 및 종속성 hello에 나열 되어 있는 개발 시스템 맞는 tooverify 해야 합니다 [Java 용 Azure 저장소 SDK] [ Azure Storage SDK for Java] GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="42d52-118">시스템에 이러한 요구 사항을 충족 하는 경우 다운로드 하 고 해당 리포지토리 로부터 시스템에 hello Java 용 Azure 저장소 라이브러리를 설치 하기 위한 hello 지침을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="42d52-119">이러한 작업을 완료 되 면이 문서의 hello 예제를 사용 하는 Java 응용 프로그램 수 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="42d52-120">사용자 응용 프로그램 tooaccess Blob 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="42d52-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="42d52-121">Hello toouse hello Azure 저장소 Api tooaccess blob 저장할 hello Java 파일 맨 문을 toohello 가져오기 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="42d52-122">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="42d52-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="42d52-123">Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="42d52-124">형식에 따라, 사용자의 저장소 계정 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 입력 하 고 hello에 나열 된 hello 저장소 계정의 기본 액세스 키를 hello 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="42d52-125">hello 다음 예제 방법을 정적 필드 toohold hello 연결 문자열을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="42d52-126">Microsoft Azure에서 역할 내에서 실행 하는 응용 프로그램을이 문자열 hello 서비스 구성 파일에 저장 될 수 *ServiceConfiguration.cscfg*, 호출 toohello로 액세스할 수 있습니다 및  **RoleEnvironment.getConfigurationSettings** 메서드.</span><span class="sxs-lookup"><span data-stu-id="42d52-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="42d52-127">hello 다음 예제에서는 가져옵니다 hello 연결 문자열에서는 **설정** 라는 요소 *StorageConnectionString* hello 서비스 구성 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="42d52-128">hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="42d52-129">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="42d52-129">Create a container</span></span>
<span data-ttu-id="42d52-130">**CloudBlobClient** 개체를 사용하면 컨테이너 및 Blob에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="42d52-131">hello 다음 코드에서는 **CloudBlobClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="42d52-132">다른 방법은 toocreate **CloudStorageAccount** 개체, 자세한 내용은 참조 **CloudStorageAccount** hello에 [Azure 저장소 클라이언트 SDK 참조]합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="42d52-133">사용 하 여 hello **CloudBlobClient** tooget toouse 원하는 참조 toohello 컨테이너 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="42d52-134">Hello로 존재 하지 않는 경우 hello 컨테이너를 만들 수 있습니다 **경고는 createIfNotExists** 메서드를 그렇지 않으면 hello 기존 컨테이너를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="42d52-135">기본적으로 hello 새 컨테이너는 private 이므로 (마찬가지로 이전 버전) 저장소 액세스 키를 지정 해야이 컨테이너에서 blob toodownload 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

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

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="42d52-136">옵션: 공용 액세스에 대한 컨테이너 구성</span><span class="sxs-lookup"><span data-stu-id="42d52-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="42d52-137">기본적으로 개인 액세스에 대 한 컨테이너의 사용 권한을 구성 하지만 인터넷 hello에 컨테이너의 권한 tooallow 공용, 읽기 전용 액세스 모든 사용자가 쉽게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="42d52-138">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="42d52-138">Upload a blob into a container</span></span>
<span data-ttu-id="42d52-139">tooupload 파일 tooa blob 컨테이너 참조를 가져오고 tooget blob 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="42d52-140">Blob 참조를 만든 후 모든 스트림을 hello blob 참조에서 업로드를 호출 하 여 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="42d52-141">이 작업을 존재 하지 못하거나 헤더가 있으면 덮어쓰기 hello blob을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="42d52-142">아래의 코드 예제는 hello이를 보여주며, 해당 hello 컨테이너 이미 만들어진 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="42d52-143">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="42d52-143">List hello blobs in a container</span></span>
<span data-ttu-id="42d52-144">컨테이너에서 hello blob toolist tooupload blob를 했던 것 처럼 먼저를 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="42d52-145">Hello 컨테이너를 사용할 수 있습니다 **listBlobs** 메서드는 **에 대 한** 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="42d52-146">hello 다음 코드에서는 출력 hello 컨테이너 toohello 콘솔에서 각 blob의 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

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

<span data-ttu-id="42d52-147">이름에 대한 경로 정보를 사용하여 Blob 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="42d52-148">이렇게 하면 기존 파일 시스템과 같이 구성 및 트래버스할 수 있는 가상 디렉터리 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="42d52-149">Hello 디렉터리 구조는 가상-hello만 Blob 저장소에서 사용할 수 있는 리소스가 컨테이너 및 blob note 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="42d52-150">그러나 hello 클라이언트 라이브러리에서 제공 된 **CloudBlobDirectory** toorefer tooa 가상 디렉터리 개체를 이러한 방식으로 구성 된 blob을 사용 하 여 처리 hello 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="42d52-151">예를 들어 이름이 "photos"인 컨테이너가 있는 경우 이 컨테이너에서 이름이 "rootphoto1", "2010/photo1", "2010/photo2" 및 "2011/photo1"인 Blob을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="42d52-152">이렇게 하면 사항이 hello "2010"과 "2011" hello "사진" 컨테이너 내에서 가상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="42d52-153">호출 하는 경우 **listBlobs** hello "사진" 컨테이너를 반환 하는 hello 컬렉션에 포함 됩니다 **CloudBlobDirectory** 및 **CloudBlob** hello를 나타내는 개체 디렉터리와 hello 최상위 수준에 포함 된 blob를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="42d52-154">이 경우에는 디렉터리 "2010", "2011" 및 사진 "rootphoto1"이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="42d52-155">Hello를 사용할 수 있습니다 **instanceof** 연산자 toodistinguish 이러한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="42d52-156">필요에 따라 매개 변수 toohello에 전달할 수 있습니다 **listBlobs** hello로 메서드 **useFlatBlobListing** tootrue 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="42d52-157">그러면 모든 Blob이 디렉터리에 상관없이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="42d52-158">자세한 내용은 참조 **CloudBlobContainer.listBlobs** hello에 [Azure 저장소 클라이언트 SDK 참조]합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="42d52-159">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="42d52-159">Download a blob</span></span>
<span data-ttu-id="42d52-160">toodownload blob hello 순서 tooget blob 참조에에서 blob을 업로드 하기 위한 수행한 것 처럼 동일한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="42d52-161">예제를 업로드 하는 hello, hello blob 개체에 대해 업로드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="42d52-162">다음 예제는 hello, 다운로드 tootransfer hello blob 내용을 tooa stream 개체와 같은 호출는 **FileOutputStream** toopersist hello blob tooa 로컬 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="42d52-163">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="42d52-163">Delete a blob</span></span>
<span data-ttu-id="42d52-164">toodelete blob을 blob 가져오기 참조 하 고, 호출 **deleteIfExists**합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="42d52-165">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="42d52-165">Delete a blob container</span></span>
<span data-ttu-id="42d52-166">마지막으로, blob 컨테이너 toodelete 가져오기 blob 컨테이너 참조 및 호출 **deleteIfExists**합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="42d52-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42d52-167">Next steps</span></span>
<span data-ttu-id="42d52-168">Blob 저장소의 기본 사항 hello를 알아보았습니다 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="42d52-169">[Java용 Azure Storage SDK][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="42d52-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="42d52-170">[Azure 저장소 클라이언트 SDK 참조][Azure 저장소 클라이언트 SDK 참조]</span><span class="sxs-lookup"><span data-stu-id="42d52-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="42d52-171">[Azure Storage REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="42d52-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="42d52-172">[Azure Storage 팀 블로그][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="42d52-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="42d52-173">자세한 내용은 참고 항목 hello [Java 개발자 센터](/develop/java/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42d52-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 저장소 클라이언트 SDK 참조]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
