---
title: "hello 기본값과에서 aaaChange blob 경로 | Microsoft Docs"
description: "Azure tooset 작동 방식을 toorename blob 파일 경로 (비공개 미리 보기)에 대해 알아봅니다"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="0aef3-103">Hello 기본 경로 (비공개 미리 보기)에서 blob 경로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="0aef3-104">이 문서에서는 Azure tooset 작동 방식을 toorename 기본 blob 파일 경로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0aef3-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0aef3-105">Prerequisites</span></span>

<span data-ttu-id="0aef3-106">리소스 그룹 내의 하이브리드 데이터 리소스에서 작업 정의가 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="0aef3-107">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="0aef3-107">Create an Azure function</span></span>

<span data-ttu-id="0aef3-108">Azure에서 함수를 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="0aef3-109">Toohello 이동 [Azure 포털](http://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="0aef3-110">왼쪽 창의 hello hello 위쪽 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="0aef3-111">Hello에 **검색** 상자에 입력 합니다 **함수 앱**, 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    !["함수 App" hello 검색 상자에 입력](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="0aef3-113">Hello에 **결과** 목록에서 클릭 **함수 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-113">In hello **Results** list, click **Function App**.</span></span>

    ![Hello 함수 응용 프로그램 리소스 hello 결과 목록에서 선택](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="0aef3-115">hello **함수 앱** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="0aef3-116">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-116">Click **Create**.</span></span>

    ![hello 함수 응용 프로그램 창 "만들기" 단추](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="0aef3-118">Hello에 **함수 앱** 구성 블레이드 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="0aef3-119">a.</span><span class="sxs-lookup"><span data-stu-id="0aef3-119">a.</span></span> <span data-ttu-id="0aef3-120">Hello에 **응용 프로그램 이름** 상자 hello 응용 프로그램 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="0aef3-121">b.</span><span class="sxs-lookup"><span data-stu-id="0aef3-121">b.</span></span> <span data-ttu-id="0aef3-122">Hello에 **구독** 상자 hello 구독의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="0aef3-123">c.</span><span class="sxs-lookup"><span data-stu-id="0aef3-123">c.</span></span> <span data-ttu-id="0aef3-124">아래 **리소스 그룹**, 클릭 **새로 만들기**, 및 hello 리소스 그룹의 hello 이름을 다음 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="0aef3-125">d.</span><span class="sxs-lookup"><span data-stu-id="0aef3-125">d.</span></span> <span data-ttu-id="0aef3-126">Hello에 **호스팅 계획** 상자에서 입력 **소비 계획**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="0aef3-127">e.</span><span class="sxs-lookup"><span data-stu-id="0aef3-127">e.</span></span> <span data-ttu-id="0aef3-128">Hello에 **위치** 상자의 형식 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="0aef3-129">f.</span><span class="sxs-lookup"><span data-stu-id="0aef3-129">f.</span></span> <span data-ttu-id="0aef3-130">**저장소 계정**에서 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="0aef3-131">Hello 함수에 대 한 저장소 계정은 내부적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-131">A storage account is used internally for hello function.</span></span>

    ![새 함수 앱 구성 데이터 입력](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="0aef3-133">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-133">Click **Create**.</span></span>  
    <span data-ttu-id="0aef3-134">hello 함수 앱이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-134">hello function app is created.</span></span>

8. <span data-ttu-id="0aef3-135">Hello 왼쪽된 창에서 클릭 **더 많은 서비스**, 수행가 다음를 hello 다음 및:</span><span class="sxs-lookup"><span data-stu-id="0aef3-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="0aef3-136">a.</span><span class="sxs-lookup"><span data-stu-id="0aef3-136">a.</span></span> <span data-ttu-id="0aef3-137">Hello에 **필터** 상자에서 입력 **응용 프로그램 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="0aef3-138">b.</span><span class="sxs-lookup"><span data-stu-id="0aef3-138">b.</span></span> <span data-ttu-id="0aef3-139">**App Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-139">Click **App Services**.</span></span> 

    ![Hello 왼쪽된 창에서 "더 많은 서비스" 링크](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="0aef3-141">앱 서비스의 hello 목록의 hello 함수 응용 프로그램의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="0aef3-142">hello 함수 응용 프로그램 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-142">hello function app page opens.</span></span>

10. <span data-ttu-id="0aef3-143">Hello 왼쪽된 창에서 클릭 **새 함수**, 수행가 다음를 hello 다음 및:</span><span class="sxs-lookup"><span data-stu-id="0aef3-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="0aef3-144">a.</span><span class="sxs-lookup"><span data-stu-id="0aef3-144">a.</span></span> <span data-ttu-id="0aef3-145">Hello에 **언어** 목록에서 **C#**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="0aef3-146">b.</span><span class="sxs-lookup"><span data-stu-id="0aef3-146">b.</span></span> <span data-ttu-id="0aef3-147">서식 파일 타일의 hello 배열에서 선택 **QueueTrigger CSharp**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="0aef3-148">c.</span><span class="sxs-lookup"><span data-stu-id="0aef3-148">c.</span></span> <span data-ttu-id="0aef3-149">Hello에 **함수 이름을** 함수에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="0aef3-150">d.</span><span class="sxs-lookup"><span data-stu-id="0aef3-150">d.</span></span> <span data-ttu-id="0aef3-151">Hello에 **큐 이름은** 상자, 데이터 변환 작업 정의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="0aef3-152">e.</span><span class="sxs-lookup"><span data-stu-id="0aef3-152">e.</span></span> <span data-ttu-id="0aef3-153">아래 **저장소 계정 연결**, 클릭 **새**, 한 다음 toohello 데이터 변환 작업을 해당 하는 hello 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="0aef3-154">Hello 연결 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-154">Make a note of hello connection name.</span></span> <span data-ttu-id="0aef3-155">Azure 함수 hello의 뒷부분에 나오는 hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-155">hello name is required later in hello Azure function.</span></span>

       ![새 C# 함수 만들기](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="0aef3-157">f.</span><span class="sxs-lookup"><span data-stu-id="0aef3-157">f.</span></span> <span data-ttu-id="0aef3-158">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-158">Click **Create**.</span></span>  
    <span data-ttu-id="0aef3-159">hello **함수** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="0aef3-160">Hello에 **함수** 창 실행 _.csx_ 파일을 선택한 수행가 다음를 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="0aef3-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="0aef3-161">a.</span><span class="sxs-lookup"><span data-stu-id="0aef3-161">a.</span></span> <span data-ttu-id="0aef3-162">Hello를 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-162">Paste hello following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create hello blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="0aef3-163">b.</span><span class="sxs-lookup"><span data-stu-id="0aef3-163">b.</span></span> <span data-ttu-id="0aef3-164">11번 줄에서 **STORAGE_CONNECTIONNAME**을 사용자의 저장소 계정 연결로 바꿉니다(포인트 8c 참조).</span><span class="sxs-lookup"><span data-stu-id="0aef3-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="0aef3-165">c.</span><span class="sxs-lookup"><span data-stu-id="0aef3-165">c.</span></span> <span data-ttu-id="0aef3-166">Hello 왼쪽 위에, 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-166">At hello top left, click **Save**.</span></span>

    ![함수 저장](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="0aef3-168">toocomplete 함수 hello, hello 다음을 수행 하 여 파일을 하나 더 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="0aef3-169">a.</span><span class="sxs-lookup"><span data-stu-id="0aef3-169">a.</span></span> <span data-ttu-id="0aef3-170">**파일 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-170">Click **View files**.</span></span>

       ![hello 파일 보기 링크](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="0aef3-172">b.</span><span class="sxs-lookup"><span data-stu-id="0aef3-172">b.</span></span> <span data-ttu-id="0aef3-173">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-173">Click **Add**.</span></span>
    
    <span data-ttu-id="0aef3-174">c.</span><span class="sxs-lookup"><span data-stu-id="0aef3-174">c.</span></span> <span data-ttu-id="0aef3-175">**project.json**을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="0aef3-176">d.</span><span class="sxs-lookup"><span data-stu-id="0aef3-176">d.</span></span> <span data-ttu-id="0aef3-177">Hello에 **project.json** 파일, 코드 다음 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-177">In hello **project.json** file, paste hello following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="0aef3-178">e.</span><span class="sxs-lookup"><span data-stu-id="0aef3-178">e.</span></span> <span data-ttu-id="0aef3-179">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-179">Click **Save**.</span></span>

<span data-ttu-id="0aef3-180">Azure Function이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-180">You have created an Azure function.</span></span> <span data-ttu-id="0aef3-181">이 함수는 hello 데이터 변환 작업에서 새 blob가 생성 될 때마다 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aef3-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aef3-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0aef3-182">Next steps</span></span>

[<span data-ttu-id="0aef3-183">StorSimple 데이터 관리자 UI tootransform 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="0aef3-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
