---
title: "Visual Studio 연결 된 서비스 (ASP.NET) 및 Azure blob 저장소 시작: aaaGet | Microsoft Docs"
description: "Visual Studio에서 ASP.NET 프로젝트에서 Azure blob 저장소를 사용 하 여 Visual Studio 연결 된 서비스를 사용 하 여 tooa 저장소 계정을 연결한 후 tooget을 시작 하는 방법"
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
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="c4233-103">Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c4233-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c4233-104">개요</span><span class="sxs-lookup"><span data-stu-id="c4233-104">Overview</span></span>

<span data-ttu-id="c4233-105">Azure blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="c4233-106">Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c4233-107">Blob 저장소 참조 tooas 개체 저장소 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="c4233-108">이 자습서에서는 Azure blob 저장소를 사용 하 여 몇 가지 일반적인 시나리오에 대 한 ASP.NET toowrite 코드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="c4233-109">시나리오에는 Blob 컨테이너 만들기, Blob 업로드, 나열, 다운로드 및 삭제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="c4233-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4233-110">Prerequisites</span></span>

* [<span data-ttu-id="c4233-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4233-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="c4233-112">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c4233-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="c4233-113">MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="c4233-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="c4233-114">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **컨트롤러**, hello 상황에 맞는 메뉴에서 **추가-컨트롤러 >**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![컨트롤러 tooan ASP.NET MVC 응용 프로그램 추가](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="c4233-116">Hello에 **추가 스 캐 폴드** 대화 상자에서 **MVC 5 컨트롤러-비어 있지**, 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="c4233-118">Hello에 **컨트롤러 추가** 대화 상자에서 이름 hello 컨트롤러 *BlobsController*를 선택 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Hello MVC 컨트롤러 이름](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="c4233-120">Hello 다음 추가 *를 사용 하 여* 지시문 toohello `BlobsController.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="c4233-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="c4233-121">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="c4233-121">Create a blob container</span></span>

<span data-ttu-id="c4233-122">Blob 컨테이너는 Blob 및 폴더의 중첩된 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="c4233-123">hello 아래 단계에 설명 방법을 toocreate blob 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="c4233-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c4233-124">hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="c4233-125">열기 hello `BlobsController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="c4233-126">**ActionResult**를 반환하는 **CreateBlobContainer**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="c4233-127">Hello 내 **CreateBlobContainer** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c4233-128">다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성에서 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="c4233-129">(변경  *&lt;저장소 계정 이름 >* toohello 이름 hello에 액세스 하는 Azure 저장소 계정입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="c4233-130">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="c4233-131">가져오기는 **CloudBlobContainer** 참조 toohello 원하는 blob 컨테이너 이름을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="c4233-132">hello **CloudBlobClient.GetContainerReference** 메서드는 blob 저장소에 대 한 요청을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="c4233-133">hello blob 컨테이너의 존재 여부 hello 참조가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="c4233-134">Hello 호출 **CloudBlobContainer.CreateIfNotExists** 메서드 toocreate hello 컨테이너 아직 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="c4233-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="c4233-135">hello **CloudBlobContainer.CreateIfNotExists** 메서드 반환 **true** hello 컨테이너 존재 하지 않는 하 고 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="c4233-136">그렇지 않으면 **false**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="c4233-137">업데이트 hello **ViewBag** hello blob 컨테이너의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="c4233-138">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **Blob**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="c4233-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c4233-139">Hello에 **뷰 추가** 대화 상자에서 입력 **CreateBlobContainer** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c4233-140">열기 `CreateBlobContainer.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="c4233-141">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c4233-142">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c4233-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="c4233-143">Hello 응용 프로그램을 실행 하 고 선택 **Create Blob Container** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="c4233-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Blob 컨테이너 만들기](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="c4233-145">앞에서 설명한 대로 hello **CloudBlobContainer.CreateIfNotExists** 메서드 반환 **true** hello 컨테이너 존재 하지 않는 있고 만들어지는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="c4233-146">따라서 hello 컨테이너 있을 때 hello 앱을 실행 하면 hello 메서드는 반환 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="c4233-147">toorun hello 앱 여러 번 삭제 해야 hello 컨테이너 hello 응용 프로그램을 다시 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="c4233-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="c4233-148">Hello 통해 hello 컨테이너 삭제를 수행할 수 있습니다 **CloudBlobContainer.Delete** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4233-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="c4233-149">Hello를 사용 하 여 hello 컨테이너를 삭제할 수도 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 hello [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="c4233-150">Blob 컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="c4233-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="c4233-151">[Blob 컨테이너를 만들면](#create-a-blob-container) 해당 컨테이너에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="c4233-152">이 섹션에서는 로컬 파일 tooa blob 컨테이너를 업로드 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="c4233-153">hello 단계 라는 blob 컨테이너를 만들었으면 가정 *테스트 blob 컨테이너*합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="c4233-154">hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="c4233-155">열기 hello `BlobsController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="c4233-156">**EmptyResult**를 반환하는 **UploadBlob**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="c4233-157">Hello 내 **UploadBlob** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c4233-158">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="c4233-159">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="c4233-160">가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="c4233-161">앞에서 설명한 대로 Azure 저장소는 다양한 Blob 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="c4233-162">tooretrieve 참조 tooa 페이지 blob의 경우 호출 hello **CloudBlobContainer.GetPageBlobReference** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4233-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="c4233-163">tooretrieve 참조 tooa 블록 blob 호출 hello **CloudBlobContainer.GetBlockBlobReference** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4233-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="c4233-164">일반적으로 블록 blob는 hello 형식 toouse 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="c4233-165">(변경 < blob-이름 > * toogive hello blob을 한 번 업로드 하려는 toohello 이름입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="c4233-166">Hello blob 참조 개체를 호출 하 여 데이터 스트림이 tooit 모든를 업로드할 수 blob 참조를 만든 후 **UploadFromStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4233-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="c4233-167">hello **UploadFromStream** 파일이 있으면 덮어씁니다 하거나가 존재 하지 않는 경우 메서드는 hello blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="c4233-168">(변경  *&lt;파일 업로드 >* tooa tooupload 원하는 toohello 파일 경로 정규화 합니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="c4233-169">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **Blob**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="c4233-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c4233-170">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c4233-171">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c4233-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="c4233-172">Hello 응용 프로그램을 실행 하 고 선택 **업로드 blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="c4233-173">섹션-hello [blob 컨테이너에서 hello blob 나열](#list-the-blobs-in-a-blob-container) -toolist hello blob 컨테이너에 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="c4233-174">Blob 컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="c4233-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="c4233-175">이 섹션에서는 toolist hello blob 컨테이너에 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="c4233-176">hello 샘플 코드에서 참조 hello *테스트 blob 컨테이너* hello 섹션에서 만든 [blob 컨테이너 만들기](#create-a-blob-container)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c4233-177">hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="c4233-178">열기 hello `BlobsController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="c4233-179">**ActionResult**를 반환하는 **ListBlobs**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="c4233-180">Hello 내 **ListBlobs** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c4233-181">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="c4233-182">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="c4233-183">가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="c4233-184">blob 컨테이너에서 hello blob toolist hello를 사용 하 여 **CloudBlobContainer.ListBlobs** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4233-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="c4233-185">hello **CloudBlobContainer.ListBlobs** 메서드가 반환 되는 **IListBlobItem** tooa 캐스팅 개체 **CloudBlockBlob**, **CloudPageBlob**, 또는 **CloudBlobDirectory** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="c4233-186">hello 다음 코드 조각 열거 된 blob 컨테이너에서 모든 hello blob 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="c4233-187">각 blob은 해당 형식과 해당 이름에 따라 캐스트 toohello 적절 한 개체 (또는 URI의 hello 대/소문자는 **CloudBlobDirectory**) tooa 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

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

    <span data-ttu-id="c4233-188">또한 tooblobs blob 컨테이너 디렉터리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="c4233-189">라는 blob 컨테이너에 있다고 가정 하겠습니다 *테스트 blob 컨테이너* 계층을 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="c4233-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="c4233-190">코드 예제에서는 앞에 오는 hello를 사용 하 여 hello **blob** 값 비슷한 toohello 다음을 포함 하는 문자열 목록:</span><span class="sxs-lookup"><span data-stu-id="c4233-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="c4233-191">볼 수 있듯이 hello 목록 hello 최상위 엔터티만 포함 됩니다. hello 하지는 스토리를 중첩 (*bar.png* 및 *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="c4233-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="c4233-192">toolist hello를 호출 해야 합니다는 blob 컨테이너 내에서 엔터티에 hello 모든 **CloudBlobContainer.ListBlobs** 메서드와 패스 **true** hello에 대 한 **useFlatBlobListing** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="c4233-193">설정 hello **useFlatBlobListing** 매개 변수가 너무**true** hello blob 컨테이너에 있는 모든 엔터티의 플랫 목록 반환 하 고 결과 다음 hello 생성:</span><span class="sxs-lookup"><span data-stu-id="c4233-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="c4233-194">Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **Blob**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.</span><span class="sxs-lookup"><span data-stu-id="c4233-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="c4233-195">Hello에 **뷰 추가** 대화 상자에서 입력 **ListBlobs** hello 뷰 이름과 선택에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="c4233-196">열기 `ListBlobs.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="c4233-197">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c4233-198">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c4233-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="c4233-199">Hello 응용 프로그램을 실행 하 고 선택 **blob 나열** toosee 스크린 샷 다음 유사한 toohello 결과:</span><span class="sxs-lookup"><span data-stu-id="c4233-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Blob 나열](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="c4233-201">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4233-201">Download blobs</span></span>

<span data-ttu-id="c4233-202">이 섹션에서는 어떻게 toodownload blob이 고 보관 toolocal 저장소 또는 읽기 hello 내용을 문자열로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="c4233-203">hello 샘플 코드에서 참조 hello *테스트 blob 컨테이너* hello 섹션에서 만든 [blob 컨테이너 만들기](#create-a-blob-container)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="c4233-204">열기 hello `BlobsController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="c4233-205">**ActionResult**를 반환하는 **DownloadBlob**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="c4233-206">Hello 내 **DownloadBlob** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c4233-207">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="c4233-208">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="c4233-209">가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="c4233-210">**CloudBlobContainer.GetBlockBlobReference** 또는 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출하여 Blob 참조 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="c4233-211">(변경  *&lt;blob 이름 >* 다운로드 하는 hello blob의 toohello 이름입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="c4233-212">toodownload blob를 사용 하 여 hello **CloudBlockBlob.DownloadToStream** 또는 **CloudPageBlob.DownloadToStream** hello blob 유형에 따라 메서드.</span><span class="sxs-lookup"><span data-stu-id="c4233-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="c4233-213">hello 다음 코드 조각을 사용 하 여 hello **CloudBlockBlob.DownloadToStream** blob의 내용을 tooa 스트림 되는 개체 메서드 tootransfer tooa 로컬 파일을 유지 됩니다: (변경  *&lt;로컬 파일 이름 >* toohello 정규화 된 파일 이름을 나타내는 hello blob 다운로드를 원하는.)</span><span class="sxs-lookup"><span data-stu-id="c4233-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="c4233-214">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c4233-215">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c4233-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="c4233-216">Hello 응용 프로그램을 실행 하 고 선택 **다운로드 blob** toodownload hello blob입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="c4233-217">hello에 지정 된 hello blob **CloudBlobContainer.GetBlockBlobReference** 메서드 호출 다운로드 hello에 지정한 toohello 위치 **File.OpenWrite** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="c4233-218">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="c4233-218">Delete blobs</span></span>

<span data-ttu-id="c4233-219">hello 아래 단계에 설명 방법을 toodelete blob:</span><span class="sxs-lookup"><span data-stu-id="c4233-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c4233-220">hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="c4233-221">열기 hello `BlobsController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="c4233-222">**ActionResult**를 반환하는 **DeleteBlob**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="c4233-223">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c4233-224">사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="c4233-225">Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="c4233-226">가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="c4233-227">**CloudBlobContainer.GetBlockBlobReference** 또는 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출하여 Blob 참조 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="c4233-228">(변경  *&lt;blob 이름 >* toohello 이름 삭제 하는 hello blob입니다.)</span><span class="sxs-lookup"><span data-stu-id="c4233-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="c4233-229">Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="c4233-230">Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="c4233-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="c4233-231">Hello 응용 프로그램을 실행 하 고 선택 **Delete blob** hello에 지정 된 toodelete hello blob **CloudBlobContainer.GetBlockBlobReference** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c4233-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4233-232">Next steps</span></span>
<span data-ttu-id="c4233-233">Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c4233-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="c4233-234">Azure 테이블 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c4233-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="c4233-235">Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="c4233-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
