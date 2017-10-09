---
title: "Microsoft Azure StorSimple Data Manager 작업에 대 한.NET SDK aaaUse | Microsoft Docs"
description: "Toouse.NET SDK toolaunch StorSimple 데이터 관리자 (비공개 미리 보기)를 작업 하는 방법에 대해 알아봅니다"
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
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>사용 하 여.Net SDK hello tooinitiate 데이터 변환 (비공개 미리 보기)

## <a name="overview"></a>개요

이 문서에서는 hello 데이터 StorSimple Manager 서비스 tootransform StorSimple 장치 데이터 내의 hello 데이터 변환 기능을 사용 하는 방법을 설명 합니다. hello 변환 된 데이터는 다음 사용 hello 클라우드에서 다른 Azure 서비스 합니다. hello 문서 샘플.NET 콘솔 응용 프로그램 tooinitiate 데이터 변환 작업을 만들고 다음 완료에 대 한 추적 연습 toohelp에 있습니다.

## <a name="prerequisites"></a>필수 조건

시작하기 전에 다음 항목이 있어야 합니다.
*   시스템에 Visual Studio 2012, 2013, 2015 또는 2017을 설치합니다.
*   Azure Powershell을 설치합니다. [Azure Powershell을 다운로드합니다](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   구성 설정 tooinitialize hello 데이터 변환 작업 (지침 tooobtain 이러한 설정을 여기에 포함 됩니다).
*   리소스 그룹 내의 하이브리드 데이터 리소스에서 올바르게 구성된 작업 정의입니다.
*   모든 필요한 hello dll 파일입니다. 이러한 dll hello에서 다운로드 [GitHub 리포지토리](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)합니다.
*   `Get-ConfigurationParams.ps1`[스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) hello github 리포지토리에서 합니다.

## <a name="step-by-step"></a>단계별 과정

Hello 다음 단계 toouse.NET toolaunch 데이터 변환 작업을 수행 합니다.

1. 다음 단계 tooretrieve hello 구성 매개 변수를 hello지 않습니다.
    1. Hello 다운로드 `Get-ConfigurationParams.ps1` hello github 리포지토리 스크립트에서 `C:\DataTransformation` 위치 합니다.
    1. Hello 실행 `Get-ConfigurationParams.ps1` hello github 리포지토리에서 스크립트입니다. Hello 다음 명령을 입력 합니다.

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        ActiveDirectoryKey 및 AppName hello에 대 한 값에 전달할 수 있습니다.


2. 이 스크립트는 다음 값에는 hello를 출력 합니다.
    * 클라이언트 ID
    * 테넌트 ID
    * Active Directory 키 (동일: hello 위에 입력 한 하나)
    * 구독 ID

3. Visual Studio 2012, 2013 또는 2015를 사용하여 C# .NET 콘솔 응용 프로그램을 만듭니다.

    1. **Visual Studio 2012/2013/2015**을 실행합니다.
    1. 클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.
    2. **템플릿**을 확장하고 **Visual C#**를 선택합니다.
    3. 선택 **콘솔 응용 프로그램** hello hello 오른쪽에 프로젝트 형식 목록에서 합니다.
    4. 입력 **DataTransformationApp** hello에 대 한 **이름**합니다.
    5. 선택 **C:\DataTransformation** hello에 대 한 **위치**합니다.
    6. 클릭 **확인** toocreate hello 프로젝트.

4.  이제 hello에 있는 모든 Dll을 추가 [dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) 폴더 **참조** 만든 hello 프로젝트에 있습니다. toodownload hello dll 파일을 다음 hello지 않습니다.

    1. Visual Studio에서 이동 너무**보기 > 솔루션 탐색기**합니다.
    1. 데이터 변환 응용 프로젝트의 hello 화살표 toohello 왼쪽을 클릭 합니다. 클릭 **참조** 다음 마우스 오른쪽 단추로 너무**참조 추가**합니다.
    2. Hello 패키지 폴더의 toohello 위치 찾아보기 hello Dll을 모두 선택 하 고 클릭 **추가**, 클릭 하 고 **확인**합니다.

5. Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일 (Program.cs).

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. 코드 다음 hello hello 데이터 변환 작업 인스턴스를 초기화 합니다. Hello에 추가 **Main 메서드에**합니다. Hello 이전에 얻은 구성 매개 변수 값을 대체 합니다. Hello 값의 연결 **리소스 그룹 이름은** 및 **하이브리드 데이터 리소스 이름**합니다. hello **리소스 그룹 이름은** hello 하이브리드 데이터 리소스는 hello에 구성 된 작업 정의 호스트 하는 hello 합니다.

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. 매개 변수는 hello로 작업 정의 필요한 toobe 실행할 hello를 지정 합니다.

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    또는

    런타임 동안 toochange hello 작업 정의 매개 변수를 원하는 경우 hello 코드 다음에 추가 합니다.

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. Hello 초기화 된 후 코드 tootrigger hello 작업 정의에 데이터 변환 작업을 수행 하는 hello를 추가 합니다. 적절 한 hello 연결 **작업 정의 이름**합니다.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. 이 작업 hello StorSimple 볼륨 toohello 지정 된 컨테이너에서 hello 루트 디렉터리 아래에 있는 일치 하는 hello 파일을 업로드합니다. Hello 큐에 메시지를 삭제할 파일을 업로드 (hello에 hello 컨테이너와 동일한 저장소 계정) hello로 이름이 hello 작업 정의 합니다. 이 메시지는 더 이상 hello 파일의 처리 트리거 tooinitiate로 사용할 수 있습니다.

10. Hello 작업이 트리거 되었습니다, 되 면 hello 코드 tootrack hello 작업 완료에 대 한 다음 추가 합니다.

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a>다음 단계

[데이터 tootransform StorSimple 데이터 관리자 UI를 사용 하 여](storsimple-data-manager-ui.md)합니다.
