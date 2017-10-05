---
title: "기본값에서 Blob 경로 변경 | Microsoft Docs"
description: "Azure 함수를 설정하여 Blob 파일 경로의 이름을 변경하는 방법 알아보기(비공개 미리 보기)"
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
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="adc3f-103">기본 경로에서 Blob 경로 변경(비공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="adc3f-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="adc3f-104">이 문서에서는 Azure 함수를 설정하여 기본 Blob 파일 경로의 이름을 변경하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="adc3f-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="adc3f-105">Prerequisites</span></span>

<span data-ttu-id="adc3f-106">리소스 그룹 내의 하이브리드 데이터 리소스에서 작업 정의가 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="adc3f-107">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="adc3f-107">Create an Azure function</span></span>

<span data-ttu-id="adc3f-108">다음 단계를 수행하여 Azure 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="adc3f-109">[Azure 포털](http://portal.azure.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="adc3f-110">왼쪽 창 맨 위에 있는 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="adc3f-111">**검색** 상자에 **함수 앱**을 입력한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![검색 상자에 “함수 앱” 입력](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="adc3f-113">**결과** 목록에서 **함수 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-113">In the **Results** list, click **Function App**.</span></span>

    ![결과 목록에서 함수 앱 리소스 선택](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="adc3f-115">**함수 앱** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="adc3f-116">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-116">Click **Create**.</span></span>

    ![함수 앱 창의 “만들기” 단추](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="adc3f-118">**함수 앱** 구성 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="adc3f-119">a.</span><span class="sxs-lookup"><span data-stu-id="adc3f-119">a.</span></span> <span data-ttu-id="adc3f-120">**앱 이름** 상자에 앱 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="adc3f-121">b.</span><span class="sxs-lookup"><span data-stu-id="adc3f-121">b.</span></span> <span data-ttu-id="adc3f-122">**구독** 상자에 구독의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="adc3f-123">c.</span><span class="sxs-lookup"><span data-stu-id="adc3f-123">c.</span></span> <span data-ttu-id="adc3f-124">**리소스 그룹**에서 **새로 만들기**를 클릭하고 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="adc3f-125">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="adc3f-125">d.</span></span> <span data-ttu-id="adc3f-126">**호스팅 계획** 상자에 **소비 계획**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="adc3f-127">e.</span><span class="sxs-lookup"><span data-stu-id="adc3f-127">e.</span></span> <span data-ttu-id="adc3f-128">**위치** 상자에 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="adc3f-129">f.</span><span class="sxs-lookup"><span data-stu-id="adc3f-129">f.</span></span> <span data-ttu-id="adc3f-130">**저장소 계정**에서 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="adc3f-131">저장소 계정은 함수에 대해 내부적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-131">A storage account is used internally for the function.</span></span>

    ![새 함수 앱 구성 데이터 입력](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="adc3f-133">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-133">Click **Create**.</span></span>  
    <span data-ttu-id="adc3f-134">함수 앱이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-134">The function app is created.</span></span>

8. <span data-ttu-id="adc3f-135">왼쪽 창에서 **더 많은 서비스**를 클릭한 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="adc3f-136">a.</span><span class="sxs-lookup"><span data-stu-id="adc3f-136">a.</span></span> <span data-ttu-id="adc3f-137">**필터** 상자에 **App Services**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="adc3f-138">b.</span><span class="sxs-lookup"><span data-stu-id="adc3f-138">b.</span></span> <span data-ttu-id="adc3f-139">**App Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-139">Click **App Services**.</span></span> 

    ![왼쪽 창의 “더 많은 서비스”](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="adc3f-141">App Services 목록에서 함수 앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="adc3f-142">함수 앱 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-142">The function app page opens.</span></span>

10. <span data-ttu-id="adc3f-143">왼쪽 창에서 **새 함수**를 클릭한 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="adc3f-144">a.</span><span class="sxs-lookup"><span data-stu-id="adc3f-144">a.</span></span> <span data-ttu-id="adc3f-145">**언어** 목록에서 **C#**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="adc3f-146">b.</span><span class="sxs-lookup"><span data-stu-id="adc3f-146">b.</span></span> <span data-ttu-id="adc3f-147">템플릿 타일 배열에서 **QueueTrigger-CSharp**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="adc3f-148">c.</span><span class="sxs-lookup"><span data-stu-id="adc3f-148">c.</span></span> <span data-ttu-id="adc3f-149">**함수 이름 지정** 상자에 함수의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="adc3f-150">d.</span><span class="sxs-lookup"><span data-stu-id="adc3f-150">d.</span></span> <span data-ttu-id="adc3f-151">**큐 이름** 상자에 데이터 변환 작업 정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="adc3f-152">e.</span><span class="sxs-lookup"><span data-stu-id="adc3f-152">e.</span></span> <span data-ttu-id="adc3f-153">**저장소 계정 연결**에서 **새로 만들기**를 클릭하고 데이터 변환 작업에 해당하는 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="adc3f-154">연결 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-154">Make a note of the connection name.</span></span> <span data-ttu-id="adc3f-155">이 이름은 Azure 함수에서 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-155">The name is required later in the Azure function.</span></span>

       ![새 C# 함수 만들기](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="adc3f-157">f.</span><span class="sxs-lookup"><span data-stu-id="adc3f-157">f.</span></span> <span data-ttu-id="adc3f-158">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-158">Click **Create**.</span></span>  
    <span data-ttu-id="adc3f-159">**함수** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="adc3f-160">**함수** 창에서 _.csx_ 파일을 실행하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="adc3f-161">a.</span><span class="sxs-lookup"><span data-stu-id="adc3f-161">a.</span></span> <span data-ttu-id="adc3f-162">다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-162">Paste the following code:</span></span>

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

        // Create the blob client.
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
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
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

    <span data-ttu-id="adc3f-163">b.</span><span class="sxs-lookup"><span data-stu-id="adc3f-163">b.</span></span> <span data-ttu-id="adc3f-164">11번 줄에서 **STORAGE_CONNECTIONNAME**을 사용자의 저장소 계정 연결로 바꿉니다(포인트 8c 참조).</span><span class="sxs-lookup"><span data-stu-id="adc3f-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="adc3f-165">c.</span><span class="sxs-lookup"><span data-stu-id="adc3f-165">c.</span></span> <span data-ttu-id="adc3f-166">왼쪽 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-166">At the top left, click **Save**.</span></span>

    ![함수 저장](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="adc3f-168">함수를 완료하려면 다음을 수행하여 파일을 하나 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="adc3f-169">a.</span><span class="sxs-lookup"><span data-stu-id="adc3f-169">a.</span></span> <span data-ttu-id="adc3f-170">**파일 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-170">Click **View files**.</span></span>

       ![“파일 보기” 링크](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="adc3f-172">b.</span><span class="sxs-lookup"><span data-stu-id="adc3f-172">b.</span></span> <span data-ttu-id="adc3f-173">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-173">Click **Add**.</span></span>
    
    <span data-ttu-id="adc3f-174">c.</span><span class="sxs-lookup"><span data-stu-id="adc3f-174">c.</span></span> <span data-ttu-id="adc3f-175">**project.json**을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="adc3f-176">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="adc3f-176">d.</span></span> <span data-ttu-id="adc3f-177">**project.json** 파일에 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-177">In the **project.json** file, paste the following code:</span></span>

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

    <span data-ttu-id="adc3f-178">e.</span><span class="sxs-lookup"><span data-stu-id="adc3f-178">e.</span></span> <span data-ttu-id="adc3f-179">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-179">Click **Save**.</span></span>

<span data-ttu-id="adc3f-180">Azure Function이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-180">You have created an Azure function.</span></span> <span data-ttu-id="adc3f-181">이 함수는 데이터 변환 작업에서 새 Blob이 생성될 때마다 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="adc3f-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adc3f-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="adc3f-182">Next steps</span></span>

<span data-ttu-id="adc3f-183">[StorSimple 데이터 관리자 UI를 사용하여 데이터를 변환합니다](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="adc3f-183">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md)</span></span>
