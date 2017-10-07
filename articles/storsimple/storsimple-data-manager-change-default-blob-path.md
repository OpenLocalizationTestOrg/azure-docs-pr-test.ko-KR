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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Hello 기본 경로 (비공개 미리 보기)에서 blob 경로 변경 합니다.

이 문서에서는 Azure tooset 작동 방식을 toorename 기본 blob 파일 경로 설명 합니다. 

## <a name="prerequisites"></a>필수 조건

리소스 그룹 내의 하이브리드 데이터 리소스에서 작업 정의가 올바르게 구성되어 있는지 확인합니다.

## <a name="create-an-azure-function"></a>Azure Function 만들기

Azure에서 함수를 toocreate 다음 hello지 않습니다.

1. Toohello 이동 [Azure 포털](http://portal.azure.com/)합니다.

2. 왼쪽 창의 hello hello 위쪽 클릭 **새로**합니다. 

3. Hello에 **검색** 상자에 입력 합니다 **함수 앱**, 한 다음 Enter 키를 누릅니다.

    !["함수 App" hello 검색 상자에 입력](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. Hello에 **결과** 목록에서 클릭 **함수 앱**합니다.

    ![Hello 함수 응용 프로그램 리소스 hello 결과 목록에서 선택](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    hello **함수 앱** 창이 열립니다.

5. **만들기**를 클릭합니다.

    ![hello 함수 응용 프로그램 창 "만들기" 단추](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. Hello에 **함수 앱** 구성 블레이드 다음 hello지 않습니다.

    a. Hello에 **응용 프로그램 이름** 상자 hello 응용 프로그램 이름을 입력 합니다.
    
    b. Hello에 **구독** 상자 hello 구독의 hello 이름을 입력 합니다.

    c. 아래 **리소스 그룹**, 클릭 **새로 만들기**, 및 hello 리소스 그룹의 hello 이름을 다음 형식입니다.

    d. Hello에 **호스팅 계획** 상자에서 입력 **소비 계획**합니다.

    e. Hello에 **위치** 상자의 형식 hello 위치입니다.

    f. **저장소 계정**에서 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다. Hello 함수에 대 한 저장소 계정은 내부적으로 사용 됩니다.

    ![새 함수 앱 구성 데이터 입력](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. **만들기**를 클릭합니다.  
    hello 함수 앱이 생성 됩니다.

8. Hello 왼쪽된 창에서 클릭 **더 많은 서비스**, 수행가 다음를 hello 다음 및:
    
    a. Hello에 **필터** 상자에서 입력 **응용 프로그램 서비스**합니다.
    
    b. **App Services**를 클릭합니다. 

    ![Hello 왼쪽된 창에서 "더 많은 서비스" 링크](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. 앱 서비스의 hello 목록의 hello 함수 응용 프로그램의 hello 이름을 클릭 합니다.  
    hello 함수 응용 프로그램 페이지가 열립니다.

10. Hello 왼쪽된 창에서 클릭 **새 함수**, 수행가 다음를 hello 다음 및: 

    a. Hello에 **언어** 목록에서 **C#**합니다.
    
    b. 서식 파일 타일의 hello 배열에서 선택 **QueueTrigger CSharp**합니다.

    c. Hello에 **함수 이름을** 함수에 대 한 이름을 입력 합니다.

    d. Hello에 **큐 이름은** 상자, 데이터 변환 작업 정의 이름을 입력 합니다.

    e. 아래 **저장소 계정 연결**, 클릭 **새**, 한 다음 toohello 데이터 변환 작업을 해당 하는 hello 계정을 선택 합니다.  
        Hello 연결 이름을 기록해 둡니다. Azure 함수 hello의 뒷부분에 나오는 hello 이름이 필요 합니다.

       ![새 C# 함수 만들기](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. **만들기**를 클릭합니다.  
    hello **함수** 창이 열립니다.

11. Hello에 **함수** 창 실행 _.csx_ 파일을 선택한 수행가 다음를 hello 다음:

    a. Hello를 코드 다음에 붙여 넣습니다.

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

    b. 11번 줄에서 **STORAGE_CONNECTIONNAME**을 사용자의 저장소 계정 연결로 바꿉니다(포인트 8c 참조).

    c. Hello 왼쪽 위에, 클릭 **저장**합니다.

    ![함수 저장](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete 함수 hello, hello 다음을 수행 하 여 파일을 하나 더 추가 합니다.

    a. **파일 보기**를 클릭합니다.

       ![hello 파일 보기 링크](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. **추가**를 클릭합니다.
    
    c. **project.json**을 입력하고 Enter 키를 누릅니다.
    
    d. Hello에 **project.json** 파일, 코드 다음 hello를 붙여 넣습니다.

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

    e. **Save**를 클릭합니다.

Azure Function이 만들어졌습니다. 이 함수는 hello 데이터 변환 작업에서 새 blob가 생성 될 때마다 발생 합니다.

## <a name="next-steps"></a>다음 단계

[StorSimple 데이터 관리자 UI tootransform 데이터 사용](storsimple-data-manager-ui.md)
