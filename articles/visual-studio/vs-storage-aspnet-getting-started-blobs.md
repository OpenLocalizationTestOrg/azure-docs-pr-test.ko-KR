---
title: "Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET) | Microsoft Docs"
description: "Visual Studio 연결된 서비스를 사용하여 저장소 계정에 연결한 후 Visual Studio의 ASP.NET 프로젝트에서 Azure Blob 저장소를 사용하는 방법에 대해 설명합니다."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: e953c7978705379a28581213e8f1c665473ddd60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="bd7be-103">Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bd7be-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="bd7be-104">개요</span><span class="sxs-lookup"><span data-stu-id="bd7be-104">Overview</span></span>

<span data-ttu-id="bd7be-105">Azure Blob 저장소는 구조화되지 않은 데이터를 개체/Blob으로 클라우드에 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="bd7be-106">Blob 저장소는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="bd7be-107">또한 Blob 저장소를 개체 저장소라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="bd7be-108">이 자습서에서는 Azure Blob 저장소를 사용하여 몇 가지 일반적인 시나리오를 위한 ASP.NET 코드를 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="bd7be-109">시나리오에는 Blob 컨테이너 만들기, Blob 업로드, 나열, 다운로드 및 삭제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="bd7be-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bd7be-110">Prerequisites</span></span>

* [<span data-ttu-id="bd7be-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd7be-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="bd7be-112">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="bd7be-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="bd7be-113">MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="bd7be-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="bd7be-114">**솔루션 탐색기**에서 **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->컨트롤러**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![ASP.NET MVC 앱에 컨트롤러 추가](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="bd7be-116">**스캐폴드 추가** 대화 상자에서 **MVC 5 컨트롤러 - 비어 있음**을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="bd7be-118">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을*BlobsController*로 설정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![MVC 컨트롤러 이름 지정](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="bd7be-120">다음 *using* 지시문을 `BlobsController.cs` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="bd7be-121">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="bd7be-121">Create a blob container</span></span>

<span data-ttu-id="bd7be-122">Blob 컨테이너는 Blob 및 폴더의 중첩된 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="bd7be-123">다음 단계에서는 Blob 컨테이너를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bd7be-124">이 섹션의 코드는 [개발 환경 설정](#set-up-the-development-environment) 섹션의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bd7be-125">`BlobsController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="bd7be-126">**ActionResult**를 반환하는 **CreateBlobContainer**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bd7be-127">**CreateBlobContainer** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bd7be-128">Azure 서비스 구성에서 저장소 연결 문자열 및 저장소 계정 정보를 가져오려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="bd7be-129">(*&lt;storage-account-name>*을 액세스 중인 Azure Storage 계정의 이름으로 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="bd7be-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bd7be-130">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="bd7be-131">원하는 Blob 컨테이너 이름에 대한 참조를 나타내는 **CloudBlobContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="bd7be-132">**CloudBlobClient.GetContainerReference** 메서드는 Blob 저장소에 대한 요청을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="bd7be-133">Blob 컨테이너가 있는지 여부에 관계없이 참조가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="bd7be-134">컨테이너가 아직 없으면 **CloudBlobContainer.CreateIfNotExists** 메서드를 호출하여 해당 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="bd7be-135">컨테이너가 없고 성공적으로 만들어지면 **CloudBlobContainer.CreateIfNotExists** 메서드에서 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="bd7be-136">그렇지 않으면 **false**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="bd7be-137">**ViewBag**을 Blob 컨테이너의 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="bd7be-138">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Blobs**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bd7be-139">**보기 추가** 대화 상자에서 보기 이름으로 **CreateBlobContainer**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bd7be-140">`CreateBlobContainer.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="bd7be-141">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bd7be-142">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="bd7be-143">응용 프로그램을 실행하고 **Blob 컨테이너 만들기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![Blob 컨테이너 만들기](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="bd7be-145">앞에서 언급했듯이 컨테이너가 없고 만들어진 경우에만 **CloudBlobContainer.CreateIfNotExists** 메서드에서 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="bd7be-146">따라서 컨테이너가 있을 때 앱을 실행하면 메서드에서 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="bd7be-147">앱을 여러 번 실행하려면 앱을 다시 실행하기 전에 컨테이너를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="bd7be-148">컨테이너 삭제는 **CloudBlobContainer.Delete** 메서드를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="bd7be-149">또한 [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 [Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 컨테이너를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="bd7be-150">Blob 컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="bd7be-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="bd7be-151">[Blob 컨테이너를 만들면](#create-a-blob-container) 해당 컨테이너에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="bd7be-152">이 섹션에서는 Blob 컨테이너에 로컬 파일을 업로드하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="bd7be-153">이 단계에서는 *test-blob-container*라는 이름의 Blob 컨테이너를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="bd7be-154">이 섹션의 코드는 [개발 환경 설정](#set-up-the-development-environment) 섹션의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bd7be-155">`BlobsController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="bd7be-156">**EmptyResult**를 반환하는 **UploadBlob**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="bd7be-157">**UploadBlob** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bd7be-158">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure Storage 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="bd7be-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bd7be-159">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="bd7be-160">Blob 컨테이너 이름에 대한 참조를 나타내는 **CloudBlobContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="bd7be-161">앞에서 설명한 대로 Azure 저장소는 다양한 Blob 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="bd7be-162">페이지 Blob에 대한 참조를 검색하려면 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="bd7be-163">블록 Blob에 대한 참조를 검색하려면 **CloudBlobContainer.GetBlockBlobReference** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="bd7be-164">일반적으로 블록 Blob을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="bd7be-165">업로드하면 <blob-name>*을 Blob에 부여할 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="bd7be-166">Blob 참조가 있으면 Blob 참조 개체의 **UploadFromStream** 메서드를 호출하여 데이터 스트림을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="bd7be-167">**UploadFromStream** 메서드는 Blob이 없는 경우 새로 만들고, Blob이 있는 경우 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="bd7be-168">*&lt;file-to-upload>*를 업로드하려는 파일의 정규화된 경로로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="bd7be-169">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Blobs**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bd7be-170">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bd7be-171">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="bd7be-172">응용 프로그램을 실행하고 **Blob 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="bd7be-173">이 섹션([Blob 컨테이너에 Blob 나열](#list-the-blobs-in-a-blob-container))에서는 Blob 컨테이너에 Blob을 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="bd7be-174">Blob 컨테이너에 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="bd7be-174">List the blobs in a blob container</span></span>

<span data-ttu-id="bd7be-175">이 섹션에서는 Blob 컨테이너에 Blob을 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="bd7be-176">샘플 코드는 [Blob 컨테이너 만들기](#create-a-blob-container) 섹션에서 만든 *test-blob-container*를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bd7be-177">이 섹션의 코드는 [개발 환경 설정](#set-up-the-development-environment) 섹션의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bd7be-178">`BlobsController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="bd7be-179">**ActionResult**를 반환하는 **ListBlobs**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bd7be-180">**ListBlobs** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bd7be-181">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure Storage 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="bd7be-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bd7be-182">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="bd7be-183">Blob 컨테이너 이름에 대한 참조를 나타내는 **CloudBlobContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="bd7be-184">Blob 컨테이너에 Blob을 나열하려면 **CloudBlobContainer.ListBlobs** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="bd7be-185">**CloudBlobContainer.ListBlobs** 메서드는 **CloudBlockBlob**, **CloudPageBlob** 또는 **CloudBlobDirectory** 개체에 캐스팅하는 **IListBlobItem** 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="bd7be-186">다음 코드 조각은 Blob 컨테이너에 있는 모든 Blob를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="bd7be-187">각 Blob은 형식에 따라 적절한 개체로 캐스팅되며 해당 이름(또는 **CloudBlobDirectory**의 경우에 URI)이 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="bd7be-188">Blob 컨테이너는 Blob 외에도 디렉터리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="bd7be-189">다음 계층 구조를 가진 *test-blob-container*라는 Blob 컨테이너가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="bd7be-190">앞의 코드 예제를 사용하면 **Blob** 문자열 목록에 다음과 비슷한 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="bd7be-191">여기서 볼 수 있듯이 목록에는 중첩된 엔터티가 아닌 최상위 엔터티만 포함됩니다(*bar.png* 및 *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="bd7be-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="bd7be-192">Blob 컨테이너 내의 모든 엔터티를 나열하려면 **CloudBlobContainer.ListBlobs** 메서드를 호출하고 **useFlatBlobListing** 매개 변수에 대해 **true**를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="bd7be-193">**useFlatBlobListing** 매개 변수를 **true**로 설정하면 Blob 컨테이너의 모든 항목에 대한 플랫 목록이 반환되고 다음 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="bd7be-194">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Blobs**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bd7be-195">**보기 추가** 대화 상자에서 보기 이름으로 **ListBlobs**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bd7be-196">`ListBlobs.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="bd7be-197">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bd7be-198">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="bd7be-199">응용 프로그램을 실행하고 **Blob 나열**을 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![Blob 나열](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="bd7be-201">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="bd7be-201">Download blobs</span></span>

<span data-ttu-id="bd7be-202">이 섹션에서는 Blob을 다운로드하고 로컬 저장소에 저장하거나 내용을 문자열로 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="bd7be-203">샘플 코드는 [Blob 컨테이너 만들기](#create-a-blob-container) 섹션에서 만든 *test-blob-container*를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="bd7be-204">`BlobsController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="bd7be-205">**ActionResult**를 반환하는 **DownloadBlob**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="bd7be-206">**DownloadBlob** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bd7be-207">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure Storage 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="bd7be-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bd7be-208">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="bd7be-209">Blob 컨테이너 이름에 대한 참조를 나타내는 **CloudBlobContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="bd7be-210">**CloudBlobContainer.GetBlockBlobReference** 또는 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출하여 Blob 참조 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="bd7be-211">*&lt;blob-name>*을 다운로드하는 Blob의 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="bd7be-212">Blob을 다운로드하려면 Blob 유형에 따라 **CloudBlockBlob.DownloadToStream** 또는 **CloudPageBlob.DownloadToStream** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="bd7be-213">다음 코드 조각에서는 **CloudBlockBlob.DownloadToStream** 메서드를 사용하여 Blob의 내용을 스트림 개체로 전송하고 로컬 파일에 저장합니다. (*&lt;local-file-name>*을 Blob을 다운로드하려는 위치를 나타내는 정규화된 파일 이름으로 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="bd7be-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="bd7be-214">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bd7be-215">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="bd7be-216">응용 프로그램을 실행하고 **Blob 다운로드**를 선택하여 Blob을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="bd7be-217">**CloudBlobContainer.GetBlockBlobReference** 메서드 호출에서 지정한 Blob은 **File.OpenWrite** 메서드 호출에서 지정한 위치로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="bd7be-218">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="bd7be-218">Delete blobs</span></span>

<span data-ttu-id="bd7be-219">다음 단계에서는 Blob을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bd7be-220">이 섹션의 코드는 [개발 환경 설정](#set-up-the-development-environment) 섹션의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bd7be-221">`BlobsController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="bd7be-222">**ActionResult**를 반환하는 **DeleteBlob**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="bd7be-223">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bd7be-224">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure Storage 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="bd7be-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bd7be-225">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="bd7be-226">Blob 컨테이너 이름에 대한 참조를 나타내는 **CloudBlobContainer** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="bd7be-227">**CloudBlobContainer.GetBlockBlobReference** 또는 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출하여 Blob 참조 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="bd7be-228">*&lt;blob-name>*을 삭제하는 Blob의 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="bd7be-229">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bd7be-230">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="bd7be-231">응용 프로그램을 실행하고 **Blob 삭제**를 선택하여 **CloudBlobContainer.GetBlockBlobReference** 메서드 호출에서 지정한 Blob을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7be-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bd7be-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd7be-232">Next steps</span></span>
<span data-ttu-id="bd7be-233">Azure에 데이터를 저장하기 위한 추가 옵션에 대한 자세한 내용은 추가 기능 가이드를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="bd7be-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="bd7be-234">Azure 테이블 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bd7be-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="bd7be-235">Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bd7be-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
