---
title: "Visual Studio 연결 된 서비스 (ASP.NET) 및 Azure blob 저장소 시작: aaaGet | Microsoft Docs"
description: "Visual Studio에서 ASP.NET 프로젝트에서 Azure blob 저장소를 사용 하 여 Visual Studio 연결 된 서비스를 사용 하 여 tooa 저장소 계정을 연결한 후 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요

Azure blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다. Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.

이 자습서에서는 Azure blob 저장소를 사용 하 여 몇 가지 일반적인 시나리오에 대 한 ASP.NET toowrite 코드 하는 방법을 보여 줍니다. 시나리오에는 Blob 컨테이너 만들기, Blob 업로드, 나열, 다운로드 및 삭제가 포함됩니다.

##<a name="prerequisites"></a>필수 조건

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>MVC 컨트롤러 만들기 

1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **컨트롤러**, hello 상황에 맞는 메뉴에서 **추가-컨트롤러 >**합니다.

    ![컨트롤러 tooan ASP.NET MVC 응용 프로그램 추가](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. Hello에 **추가 스 캐 폴드** 대화 상자에서 **MVC 5 컨트롤러-비어 있지**, 선택한 **추가**합니다.

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. Hello에 **컨트롤러 추가** 대화 상자에서 이름 hello 컨트롤러 *BlobsController*를 선택 하 고 **추가**합니다.

    ![Hello MVC 컨트롤러 이름](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Hello 다음 추가 *를 사용 하 여* 지시문 toohello `BlobsController.cs` 파일:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Blob 컨테이너 만들기

Blob 컨테이너는 Blob 및 폴더의 중첩된 계층 구조입니다. hello 아래 단계에 설명 방법을 toocreate blob 컨테이너:

> [!NOTE]
> 
> hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `BlobsController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **CreateBlobContainer**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **CreateBlobContainer** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성에서 hello를 사용 합니다. (변경  *&lt;저장소 계정 이름 >* toohello 이름 hello에 액세스 하는 Azure 저장소 계정입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 가져오기는 **CloudBlobContainer** 참조 toohello 원하는 blob 컨테이너 이름을 나타내는 개체입니다. hello **CloudBlobClient.GetContainerReference** 메서드는 blob 저장소에 대 한 요청을 만들지 않습니다. hello blob 컨테이너의 존재 여부 hello 참조가 반환 됩니다. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Hello 호출 **CloudBlobContainer.CreateIfNotExists** 메서드 toocreate hello 컨테이너 아직 존재 하지 않는 경우. hello **CloudBlobContainer.CreateIfNotExists** 메서드 반환 **true** hello 컨테이너 존재 하지 않는 하 고 성공적으로 만들었습니다. 그렇지 않으면 **false**가 반환됩니다.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. 업데이트 hello **ViewBag** hello blob 컨테이너의 hello 이름의 합니다.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **Blob**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **CreateBlobContainer** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `CreateBlobContainer.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **Create Blob Container** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![Blob 컨테이너 만들기](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    앞에서 설명한 대로 hello **CloudBlobContainer.CreateIfNotExists** 메서드 반환 **true** hello 컨테이너 존재 하지 않는 있고 만들어지는 경우에 합니다. 따라서 hello 컨테이너 있을 때 hello 앱을 실행 하면 hello 메서드는 반환 **false**합니다. toorun hello 앱 여러 번 삭제 해야 hello 컨테이너 hello 응용 프로그램을 다시 실행 하기 전에. Hello 통해 hello 컨테이너 삭제를 수행할 수 있습니다 **CloudBlobContainer.Delete** 메서드. Hello를 사용 하 여 hello 컨테이너를 삭제할 수도 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 hello [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.  

## <a name="upload-a-blob-into-a-blob-container"></a>Blob 컨테이너에 Blob 업로드

[Blob 컨테이너를 만들면](#create-a-blob-container) 해당 컨테이너에 파일을 업로드할 수 있습니다. 이 섹션에서는 로컬 파일 tooa blob 컨테이너를 업로드 하는 과정을 안내 합니다. hello 단계 라는 blob 컨테이너를 만들었으면 가정 *테스트 blob 컨테이너*합니다. 

> [!NOTE]
> 
> hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `BlobsController.cs` 파일입니다.

1. **EmptyResult**를 반환하는 **UploadBlob**라는 메서드를 추가합니다.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Hello 내 **UploadBlob** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. 앞에서 설명한 대로 Azure 저장소는 다양한 Blob 유형을 지원합니다. tooretrieve 참조 tooa 페이지 blob의 경우 호출 hello **CloudBlobContainer.GetPageBlobReference** 메서드. tooretrieve 참조 tooa 블록 blob 호출 hello **CloudBlobContainer.GetBlockBlobReference** 메서드. 일반적으로 블록 blob는 hello 형식 toouse 것이 좋습니다. (변경 < blob-이름 > * toogive hello blob을 한 번 업로드 하려는 toohello 이름입니다.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Hello blob 참조 개체를 호출 하 여 데이터 스트림이 tooit 모든를 업로드할 수 blob 참조를 만든 후 **UploadFromStream** 메서드. hello **UploadFromStream** 파일이 있으면 덮어씁니다 하거나가 존재 하지 않는 경우 메서드는 hello blob을 만듭니다. (변경  *&lt;파일 업로드 >* tooa tooupload 원하는 toohello 파일 경로 정규화 합니다.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **Blob**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **업로드 blob**합니다.  
  
섹션-hello [blob 컨테이너에서 hello blob 나열](#list-the-blobs-in-a-blob-container) -toolist hello blob 컨테이너에 blob 하는 방법을 보여 줍니다.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Blob 컨테이너에서 hello blob 나열

이 섹션에서는 toolist hello blob 컨테이너에 blob 하는 방법을 보여 줍니다. hello 샘플 코드에서 참조 hello *테스트 blob 컨테이너* hello 섹션에서 만든 [blob 컨테이너 만들기](#create-a-blob-container)합니다.

> [!NOTE]
> 
> hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `BlobsController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **ListBlobs**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Hello 내 **ListBlobs** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. blob 컨테이너에서 hello blob toolist hello를 사용 하 여 **CloudBlobContainer.ListBlobs** 메서드. hello **CloudBlobContainer.ListBlobs** 메서드가 반환 되는 **IListBlobItem** tooa 캐스팅 개체 **CloudBlockBlob**, **CloudPageBlob**, 또는 **CloudBlobDirectory** 개체입니다. hello 다음 코드 조각 열거 된 blob 컨테이너에서 모든 hello blob 합니다. 각 blob은 해당 형식과 해당 이름에 따라 캐스트 toohello 적절 한 개체 (또는 URI의 hello 대/소문자는 **CloudBlobDirectory**) tooa 목록에 추가 됩니다.

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

    또한 tooblobs blob 컨테이너 디렉터리를 포함할 수 있습니다. 라는 blob 컨테이너에 있다고 가정 하겠습니다 *테스트 blob 컨테이너* 계층을 따라 hello로:

        foo.png
        dir1/bar.png
        dir2/baz.png

    코드 예제에서는 앞에 오는 hello를 사용 하 여 hello **blob** 값 비슷한 toohello 다음을 포함 하는 문자열 목록:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    볼 수 있듯이 hello 목록 hello 최상위 엔터티만 포함 됩니다. hello 하지는 스토리를 중첩 (*bar.png* 및 *baz.png*). toolist hello를 호출 해야 합니다는 blob 컨테이너 내에서 엔터티에 hello 모든 **CloudBlobContainer.ListBlobs** 메서드와 패스 **true** hello에 대 한 **useFlatBlobListing** 매개 변수입니다.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    설정 hello **useFlatBlobListing** 매개 변수가 너무**true** hello blob 컨테이너에 있는 모든 엔터티의 플랫 목록 반환 하 고 결과 다음 hello 생성:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **Blob**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **ListBlobs** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `ListBlobs.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

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

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **blob 나열** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![Blob 나열](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Blob 다운로드

이 섹션에서는 어떻게 toodownload blob이 고 보관 toolocal 저장소 또는 읽기 hello 내용을 문자열로 보여 줍니다. hello 샘플 코드에서 참조 hello *테스트 blob 컨테이너* hello 섹션에서 만든 [blob 컨테이너 만들기](#create-a-blob-container)합니다.

1. 열기 hello `BlobsController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **DownloadBlob**이라는 메서드를 추가합니다.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Hello 내 **DownloadBlob** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. **CloudBlobContainer.GetBlockBlobReference** 또는 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출하여 Blob 참조 개체를 가져옵니다. (변경  *&lt;blob 이름 >* 다운로드 하는 hello blob의 toohello 이름입니다.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload blob를 사용 하 여 hello **CloudBlockBlob.DownloadToStream** 또는 **CloudPageBlob.DownloadToStream** hello blob 유형에 따라 메서드. hello 다음 코드 조각을 사용 하 여 hello **CloudBlockBlob.DownloadToStream** blob의 내용을 tooa 스트림 되는 개체 메서드 tootransfer tooa 로컬 파일을 유지 됩니다: (변경  *&lt;로컬 파일 이름 >* toohello 정규화 된 파일 이름을 나타내는 hello blob 다운로드를 원하는.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **다운로드 blob** toodownload hello blob입니다. hello에 지정 된 hello blob **CloudBlobContainer.GetBlockBlobReference** 메서드 호출 다운로드 hello에 지정한 toohello 위치 **File.OpenWrite** 메서드를 호출 합니다. 

## <a name="delete-blobs"></a>Blob 삭제

hello 아래 단계에 설명 방법을 toodelete blob:

> [!NOTE]
> 
> hello이 섹션의 코드 가정 hello 섹션의 hello 단계를 완료 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `BlobsController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **DeleteBlob**이라는 메서드를 추가합니다.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Blob service 클라이언트를 나타내는 **CloudBlobClient** 개체를 가져옵니다.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 가져오기는 **CloudBlobContainer** 참조 toohello blob 컨테이너 이름을 나타내는 개체입니다. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. **CloudBlobContainer.GetBlockBlobReference** 또는 **CloudBlobContainer.GetPageBlobReference** 메서드를 호출하여 Blob 참조 개체를 가져옵니다. (변경  *&lt;blob 이름 >* toohello 이름 삭제 하는 hello blob입니다.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **Delete blob** hello에 지정 된 toodelete hello blob **CloudBlobContainer.GetBlockBlobReference** 메서드를 호출 합니다. 

## <a name="next-steps"></a>다음 단계
Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.

  * [Azure 테이블 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
  * [Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
