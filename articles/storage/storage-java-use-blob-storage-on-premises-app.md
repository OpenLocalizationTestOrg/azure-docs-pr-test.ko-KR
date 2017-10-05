---
title: "Blob 저장소를 사용하는 온-프레미스 응용 프로그램(Java) | Microsoft Docs"
description: "Azure에 이미지를 업로드한 다음 브라우저에 해당 이미지를 표시하는 콘솔 응용 프로그램을 만드는 방법에 대해 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="cded3-104">Blob 저장소를 사용하는 온-프레미스 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cded3-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="cded3-105">개요</span><span class="sxs-lookup"><span data-stu-id="cded3-105">Overview</span></span>
<span data-ttu-id="cded3-106">다음 예제에서는 Azure 저장소를 사용하여 이미지를 Azure에 저장할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="cded3-107">이 문서의 코드는 Azure에 이미지를 업로드한 다음 그 이미지를 브라우저에 표시하는 HTML 파일을 만드는 콘솔 응용 프로그램용 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cded3-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cded3-108">Prerequisites</span></span>
* <span data-ttu-id="cded3-109">JDK(Java Developer Kit) 버전 1.6 이상이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="cded3-110">Azure SDK가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="cded3-111">Java용 Azure 라이브러리를 위한 JAR 및 해당하는 종속성 JAR이 설치되어 있어야 하며 Java 컴파일러가 사용하는 빌드 경로에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="cded3-112">Java용 Azure 라이브러리 설치에 대한 자세한 내용은 [Java용 Azure SDK 다운로드](../java-download-azure-sdk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cded3-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="cded3-113">Azure 저장소 계정이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="cded3-114">이 문서의 코드에서는 저장소 계정의 계정 이름 및 계정 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="cded3-115">저장소 계정 만들기에 대한 자세한 내용은 [저장소 계정을 만드는 방법](storage-create-storage-account.md#create-a-storage-account)을, 계정 키 검색에 대한 자세한 내용은 [저장소 액세스 키 보기 및 복사](storage-create-storage-account.md#view-and-copy-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cded3-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="cded3-116">이름을 지정한 로컬 이미지 파일을 만들어 c:\\myimages\\image1.jpg 경로에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="cded3-117">또는 예제에서 **FileInputStream** 생성자를 수정하여 다른 이미지 경로 및 파일 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="cded3-118">Azure Blob 저장소를 사용하여 파일을 업로드하려면</span><span class="sxs-lookup"><span data-stu-id="cded3-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="cded3-119">여기서는 단계별 절차를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="cded3-120">건너뛰고 싶은 경우 이 문서의 뒷부분에 전체 코드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="cded3-121">Azure 핵심 저장소 클래스, Azure Blob 클라이언트 클래스, Java IO 클래스, **URISyntaxException** 클래스에 대한 가져오기를 포함하여 코드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="cded3-122">이름이 **StorageSample**인 클래스를 선언하고 여는 중괄호(**{**)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="cded3-123">**StorageSample** 클래스 내에서 Azure 저장소 계정에 지정된 것과 같이 기본 끝점 프로토콜, 저장소 계정 이름, 저장소 액세스 키가 포함될 문자열 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="cded3-124">**your\_account\_name** 및 **your\_account\_key** 자리 표시자 값을 각각 자신의 계정 이름 및 계정 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="cded3-125">**main** 선언을 추가하고 **try** 블록을 포함하며 필요한 여는 중괄호(**{**)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="cded3-126">다음 유형의 변수를 선언합니다. 이 예제에서 변수가 어떻게 사용되는지 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="cded3-127">**CloudStorageAccount**: Azure 저장소 계정 이름 및 키로 계정 개체를 초기화하고 Blob 클라이언트 개체를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="cded3-128">**CloudBlobClient**: Blob 서비스에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="cded3-129">**CloudBlobContainer**: Blob 컨테이너를 만들고, 컨테이너에서 Blob을 나열하고, 컨테이너를 삭제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="cded3-130">**CloudBlockBlob**: 로컬 이미지 파일을 컨테이너에 업로드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="cded3-131">**account** 변수에 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="cded3-132">**serviceClient** 변수에 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="cded3-133">**container** 변수에 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="cded3-134">**gettingstarted**라는 컨테이너에 대한 참조를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="cded3-135">컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-135">Create the container.</span></span> <span data-ttu-id="cded3-136">이 메서드는 컨테이너가 없을 경우 컨테이너를 만들고 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="cded3-137">컨테이너가 있으면 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="cded3-138">**createIfNotExists** 대신 **create** 메서드(컨테이너가 이미 있는 경우 오류를 반환함)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="cded3-139">컨테이너에 대해 익명 액세스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="cded3-140">블록 Blob에 대한 참조를 가져오며 Azure 저장소의 Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="cded3-141">**File** 생성자를 사용하여, 로컬로 만들어졌으며 업로드할 파일에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="cded3-142">이 파일은 코드를 실행하기 전에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="cded3-143">**CloudBlockBlob.upload** 메서드에 대한 호출을 통해 로컬 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="cded3-144">**CloudBlockBlob.upload** 메서드의 첫 번째 매개 변수는 Azure Storage에 업로드할 로컬 파일을 나타내는 **FileInputStream** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="cded3-145">두 번째 매개 변수는 파일의 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="cded3-146">**MakeHTMLPage**라는 도우미 함수를 호출하여 지금 Azure Storage 계정에 있는 Blob에 대한 원본 집합으로 **&lt;image&gt;** 요소가 포함된 기본 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="cded3-147">**MakeHTMLPage** 에 대한 코드는 이 항목의 뒷부분에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="cded3-148">만들어진 HTML 페이지에 대한 상태 메시지 및 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="cded3-149">닫는 중괄호(**}**)를 삽입하여 **try** 블록을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cded3-150">다음 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="cded3-151">**FileNotFoundException**: **FileInputStream** 또는 **FileOutputStream** 생성자가 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="cded3-152">**StorageException**: Azure 클라이언트 저장소 라이브러리가 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="cded3-153">**URISyntaxException**: **ListBlobItem.getUri** 메서드가 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="cded3-154">**Exception**: 일반적인 예외 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-154">**Exception**: Generic exception handling.</span></span>

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="cded3-155">닫는 중괄호(**}**)를 삽입하여 **main**을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cded3-156">이름이 **MakeHTMLPage** 인 메서드를 만들어 기본 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="cded3-157">이 메서드는 업로드된 Blob 목록에서 반복하는 데 사용될 **CloudBlobContainer**유형의 매개 변수를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="cded3-158">이 메서드는 **FileOutputStream** 생성자가 throw할 수 있는 **FileNotFoundException** 유형 및 **ListBlobItem.getUri** 메서드가 throw할 수 있는 **URISyntaxException** 유형의 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="cded3-159">여는 중괄호( **{**)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="cded3-160">이름이 **index.html**인 로컬 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="cded3-161">**&lt;html&gt;**, **&lt;header&gt;**, **&lt;body&gt;** 요소를 포함하여 로컬 파일에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="cded3-162">업로드된 Blob 목록에서 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="cded3-163">Blob이 Azure Storage 계정에 있는 경우 각 Blob에 대해 HTML 페이지에 Blob의 URI에 보낸 **src** 특성이 있는 **&lt;img&gt;** 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="cded3-164">이 샘플에서는 이미지를 하나만 추가했지만 더 추가하면 이 코드는 모든 이미지를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="cded3-165">간단히 하기 위해 이 예제는 업로드된 각 Blob이 이미지라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="cded3-166">이미지가 아닌 Blob을 업데이트했거나 블록 Blob이 아닌 페이지 Blob을 업데이트했으면 필요에 따라 코드를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="cded3-167">**&lt;body&gt;** 요소와 **&lt;html&gt;** 요소를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="cded3-168">로컬 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="cded3-169">닫는 중괄호(**}**)를 삽입하여 **MakeHTMLPage**를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cded3-170">닫는 중괄호(**}**)를 삽입하여 **StorageSample**을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cded3-171">다음은 이 예제의 완성 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-171">The following is the complete code for this example.</span></span> <span data-ttu-id="cded3-172">계정 이름 및 계정 키를 사용하도록 **your\_account\_name** 및 **your\_account\_key** 자리 표시자 값을 각각 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="cded3-173">이 예제 코드는 로컬 이미지 파일을 Azure 저장소에 업로드할 뿐만 아니라 브라우저에서 열어 업로드된 이미지를 볼 수 있는 namedindex.html 로컬 파일도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="cded3-174">코드에 계정 이름 및 계정 키가 포함되어 있으므로 소스 코드가 안전한지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="cded3-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="cded3-175">컨테이너를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="cded3-175">To delete a container</span></span>
<span data-ttu-id="cded3-176">저장소에 대한 요금이 부과되므로 이 예제를 테스트한 후에 **gettingstarted** 컨테이너를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="cded3-177">컨테이너를 삭제하려면 **CloudBlobContainer.delete** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="cded3-178">**CloudBlobContainer.delete** 메서드를 호출하기 위해 **CloudStorageAccount**, **ClodBlobClient**, **CloudBlobContainer** 개체를 초기화하는 프로세스는 **createIfNotExist** 메서드의 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="cded3-179">다음은 **gettingstarted**라는 컨테이너를 삭제하는 완성 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="cded3-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

<span data-ttu-id="cded3-180">기타 Blob 저장소 클래스 및 메서드에 대한 개요는 [Java에서 Blob 저장소를 사용하는 방법](storage-java-how-to-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cded3-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cded3-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cded3-181">Next steps</span></span>
<span data-ttu-id="cded3-182">더 복잡 한 저장소 작업에 대한 자세한 내용을 보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="cded3-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="cded3-183">Java용 Azure 저장소 SDK</span><span class="sxs-lookup"><span data-stu-id="cded3-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="cded3-184">Azure 저장소 클라이언트 SDK 참조</span><span class="sxs-lookup"><span data-stu-id="cded3-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="cded3-185">Azure Storage 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="cded3-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="cded3-186">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="cded3-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

