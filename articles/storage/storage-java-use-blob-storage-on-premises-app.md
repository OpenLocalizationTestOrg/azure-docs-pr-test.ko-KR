---
title: "blob 저장소 (Java) aaaOn 온-프레미스 응용 프로그램 | Microsoft Docs"
description: "Toocreate 업로드 한 이미지 tooAzure 차례로 표시 하는 콘솔 응용 프로그램 브라우저에서 이미지를 hello 하는 방법에 대해 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
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
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="8b96e-104">Blob 저장소를 사용하는 온-프레미스 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b96e-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="8b96e-105">개요</span><span class="sxs-lookup"><span data-stu-id="8b96e-105">Overview</span></span>
<span data-ttu-id="8b96e-106">hello 다음 예제에 나와 Azure 저장소를 사용 하 여 Azure에서 이미지를 저장 하는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="8b96e-107">이 문서에 hello 코드 이미지 tooAzure를 업로드 하 고 다음 브라우저에서 hello 이미지를 표시 하는 HTML 파일을 만듭니다는 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b96e-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8b96e-108">Prerequisites</span></span>
* <span data-ttu-id="8b96e-109">JDK(Java Developer Kit) 버전 1.6 이상이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="8b96e-110">hello Azure SDK가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="8b96e-111">Java 용 Azure 라이브러리 hello JAR hello 및 모든 해당 종속성 Jar 설치 되 고 Java 컴파일러에서 사용 하는 hello 빌드 경로에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="8b96e-112">Java 용 Azure 라이브러리 hello를 설치 하는 방법에 대 한 정보를 참조 하십시오. [다운로드 hello Azure SDK for Java](../java-download-azure-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="8b96e-113">Azure 저장소 계정이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="8b96e-114">hello 계정 이름과 계정 키 hello 저장소 계정에 대 한 사용 됩니다이 문서의 hello 코드에서.</span><span class="sxs-lookup"><span data-stu-id="8b96e-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="8b96e-115">참조 [어떻게 tooCreate 저장소 계정을](storage-create-storage-account.md#create-a-storage-account) 저장소 계정을 만드는 방법에 대 한 내용은 및 [저장소 액세스 키 보기 및 복사](storage-create-storage-account.md#view-and-copy-storage-access-keys) hello 계정 키를 검색 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="8b96e-116">명명 된 로컬 이미지 파일을 만든 hello path c:에 저장 되지만\\myimages\\image1.jpg 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="8b96e-117">또는 수정할는 **FileInputStream** hello 예제 toouse 다른 이미지 경로 및 파일 이름에에서는 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="8b96e-118">toouse Azure blob 저장소 tooupload 파일</span><span class="sxs-lookup"><span data-stu-id="8b96e-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="8b96e-119">여기서는 단계별 절차를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="8b96e-120">Tooskip 미리, 원하는 경우 hello 전체 코드는이 문서의 뒷부분에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="8b96e-121">Hello Azure 핵심 저장소 클래스, hello Azure blob 클라이언트 클래스, hello Java IO 클래스 및 hello에 대 한 가져오기를 포함 하 여 hello 코드 시작 **URISyntaxException** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="8b96e-122">이라는 클래스를 선언 **StorageSample**, hello 괄호를 포함 하 고 **{**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="8b96e-123">Hello 내 **StorageSample** 클래스, 기본 끝점 프로토콜 hello, 저장소 계정 이름 및 Azure 저장소 계정에 지정 된 저장소 액세스 키를 포함 될 문자열 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="8b96e-124">Hello 자리 표시자 값을 대체 **프로그램\_계정\_이름** 및 **프로그램\_계정\_키** 사용자 고유의 계정 이름과 계정 키를 각각.</span><span class="sxs-lookup"><span data-stu-id="8b96e-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="8b96e-125">에 대 한 선언에서 추가 **주**, 포함 한 **시도** 블록과 hello 필요한 여는 괄호를 포함 **{**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="8b96e-126">Hello 형식 (이 예제에서 사용 방법에 대 한 설명은 됩니다 hello) 다음의 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="8b96e-127">**CloudStorageAccount**: 사용 되는 tooinitialize hello 계정 blob 클라이언트 개체를 Azure 저장소 계정 이름 및 키 및 toocreate 포함 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="8b96e-128">**CloudBlobClient**: tooaccess hello blob 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="8b96e-129">**CloudBlobContainer**: blob 컨테이너를 사용 하는 toocreate hello 컨테이너 및 delete hello 컨테이너에 blob를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="8b96e-130">**CloudBlockBlob**: 사용 되는 tooupload 로컬 이미지 파일 toothe 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="8b96e-131">할당 값 toohello **계정** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="8b96e-132">할당 값 toohello **serviceClient** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="8b96e-133">할당 값 toohello **컨테이너** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="8b96e-134">라는 참조 tooa 컨테이너 살펴보겠습니다 **gettingstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="8b96e-135">Hello 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-135">Create hello container.</span></span> <span data-ttu-id="8b96e-136">사이트 존재 하지 않는 경우이 메서드는 hello 컨테이너를 만듭니다 (다음 다시 돌아와 **true**).</span><span class="sxs-lookup"><span data-stu-id="8b96e-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="8b96e-137">Hello 컨테이너가 존재 하는 경우 반환 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="8b96e-138">대신 너무**경고는 createIfNotExists** 는 hello **만들** 메서드 (hello 컨테이너가 이미 존재 하는 경우 오류가 반환 됩니다).</span><span class="sxs-lookup"><span data-stu-id="8b96e-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="8b96e-139">Hello 컨테이너에 대 한 익명 액세스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="8b96e-140">Azure 저장소에 blob hello를 나타내는 참조 toohello 블록 blob을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="8b96e-141">사용 하 여 hello **파일** 생성자 tooget 참조 toohello 로컬로 만들어진 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="8b96e-142">Hello 코드를 실행 하기 전에이 파일을 만들었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="8b96e-143">호출 toohello 통해 hello 로컬 파일을 업로드 **CloudBlockBlob.upload** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8b96e-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="8b96e-144">첫 번째 매개 변수 toohello hello **CloudBlockBlob.upload** 메서드는 한 **FileInputStream** 될 해당 나타냅니다 hello 로컬 파일 업로드 tooAzure 저장소 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="8b96e-145">hello 두 번째 매개 변수는 hello 파일의 바이트에서 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="8b96e-146">도우미 함수를 호출 **MakeHTMLPage**, toomake 기본 HTML 페이지를 포함 하는  **&lt;이미지&gt;**  이제 Azure에 있는 hello 소스 집합 toohello blob과 함께 요소 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="8b96e-147">에 대 한 코드 hello **MakeHTMLPage** 이 문서의 뒷부분에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="8b96e-148">상태 메시지 및 생성 된 HTML 페이지 hello에 대 한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="8b96e-149">닫기 hello **시도** 닫는 괄호를 삽입 하 여 블록: **}**</span><span class="sxs-lookup"><span data-stu-id="8b96e-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="8b96e-150">Hello 다음 예외를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="8b96e-151">**FileNotFoundException**: hello throw 될 수 있는 **FileInputStream** 또는 **FileOutputStream** 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="8b96e-152">**StorageException**: hello Azure 클라이언트 저장소 라이브러리에 의해 throw 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="8b96e-153">**URISyntaxException**: hello throw 될 수 있는 **ListBlobItem.getUri** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8b96e-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="8b96e-154">**Exception**: 일반적인 예외 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="8b96e-155">닫는 중괄호(**}**)를 삽입하여 **main**을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="8b96e-156">라는 메서드를 만듭니다 **MakeHTMLPage** toocreate 기본 HTML 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="8b96e-157">이 메서드는 형식 매개 변수가 **CloudBlobContainer**, 업로드 된 blob의 hello 목록에서 사용 되는 tooiterate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="8b96e-158">이 메서드는 형식의 예외를 throw **FileNotFoundException**, hello에 의해 throw 될 수 있는 **FileOutputStream** 생성자 및 **URISyntaxException**를 수 있습니다 hello를 통해 throw 될 **ListBlobItem.getUri** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8b96e-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="8b96e-159">여는 중괄호( **{**)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="8b96e-160">이름이 **index.html**인 로컬 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="8b96e-161">Hello에 추가 하는 toohello 로컬 파일을 작성할  **&lt;html&gt;**,  **&lt;헤더&gt;**, 및  **&lt;본문&gt;**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="8b96e-162">업로드 된 blob의 hello 목록을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="8b96e-163">각 blob에 대 한 만들기에 hello HTML 페이지에는  **&lt;img&gt;**  를 가진 요소가 해당 **src** 특성을 Azure 저장소 계정에 있는 hello hello blob의 URI에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="8b96e-164">이 샘플에서는 이미지를 하나만 추가했지만 더 추가하면 이 코드는 모든 이미지를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="8b96e-165">간단히 하기 위해 이 예제는 업로드된 각 Blob이 이미지라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="8b96e-166">이미지 이외의 blob 또는 페이지 blob 대신 블록 blob 업데이트 한 경우 필요에 따라 hello 코드를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="8b96e-167">닫기 hello  **&lt;본문&gt;**  요소와 hello  **&lt;html&gt;**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="8b96e-168">로컬 파일을 닫기 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="8b96e-169">닫는 중괄호(**}**)를 삽입하여 **MakeHTMLPage**를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="8b96e-170">닫는 중괄호(**}**)를 삽입하여 **StorageSample**을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="8b96e-171">hello 다음은이 예제에 대 한 hello 전체 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="8b96e-172">Toomodify hello 자리 표시자 값을 기억 **프로그램\_계정\_이름** 및 **프로그램\_계정\_키** toouse 계정 이름 및 계정 키를, 각각.</span><span class="sxs-lookup"><span data-stu-id="8b96e-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
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

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

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

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="8b96e-173">또한 toouploading 로컬 이미지 파일 tooAzure 저장소 hello 예제 코드를 만듭니다 브라우저 toosee에서 열 수 있는 한 로컬 파일 namedindex.html 업로드 된 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="8b96e-174">Hello 코드 계정 이름과 계정 키에 포함 되어 있으므로 소스 코드 보안 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="8b96e-175">toodelete 컨테이너</span><span class="sxs-lookup"><span data-stu-id="8b96e-175">toodelete a container</span></span>
<span data-ttu-id="8b96e-176">저장소에 대 한 요금이 청구 되므로 toodelete 경우가 **gettingstarted** 컨테이너 완료 한 후이 예제에서는 작업할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="8b96e-177">toodelete 컨테이너를 사용 하 여 hello **CloudBlobContainer.delete** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8b96e-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="8b96e-178">toocall hello **CloudBlobContainer.delete** 메서드를 초기화 하는 hello 프로세스 **CloudStorageAccount**, **ClodBlobClient**, 및  **CloudBlobContainer** 개체에 대 한 표시 된 것 처럼 동일 hello는 **createIfNotExist** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8b96e-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="8b96e-179">hello 다음은 hello 라는 컨테이너를 삭제 하는 전체 예제 **gettingstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

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

<span data-ttu-id="8b96e-180">다른 blob 저장소 클래스와 메서드의 개요를 참조 하십시오. [어떻게 toouse Java에서 Blob 저장소](storage-java-how-to-use-blob-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b96e-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b96e-181">Next steps</span></span>
<span data-ttu-id="8b96e-182">이러한 링크 toolearn 더 복잡 한 저장소 작업에 대 한 자세한를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b96e-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="8b96e-183">Java용 Azure 저장소 SDK</span><span class="sxs-lookup"><span data-stu-id="8b96e-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="8b96e-184">Azure 저장소 클라이언트 SDK 참조</span><span class="sxs-lookup"><span data-stu-id="8b96e-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="8b96e-185">Azure Storage 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="8b96e-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="8b96e-186">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="8b96e-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

