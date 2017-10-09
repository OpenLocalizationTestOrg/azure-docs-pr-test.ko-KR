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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="0061a-103">사용 하 여.Net SDK hello tooinitiate 데이터 변환 (비공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="0061a-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="0061a-104">개요</span><span class="sxs-lookup"><span data-stu-id="0061a-104">Overview</span></span>

<span data-ttu-id="0061a-105">이 문서에서는 hello 데이터 StorSimple Manager 서비스 tootransform StorSimple 장치 데이터 내의 hello 데이터 변환 기능을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="0061a-106">hello 변환 된 데이터는 다음 사용 hello 클라우드에서 다른 Azure 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="0061a-107">hello 문서 샘플.NET 콘솔 응용 프로그램 tooinitiate 데이터 변환 작업을 만들고 다음 완료에 대 한 추적 연습 toohelp에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0061a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0061a-108">Prerequisites</span></span>

<span data-ttu-id="0061a-109">시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="0061a-110">시스템에 Visual Studio 2012, 2013, 2015 또는 2017을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="0061a-111">Azure Powershell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-111">Azure Powershell installed.</span></span> <span data-ttu-id="0061a-112">[Azure Powershell을 다운로드합니다](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="0061a-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="0061a-113">구성 설정 tooinitialize hello 데이터 변환 작업 (지침 tooobtain 이러한 설정을 여기에 포함 됩니다).</span><span class="sxs-lookup"><span data-stu-id="0061a-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="0061a-114">리소스 그룹 내의 하이브리드 데이터 리소스에서 올바르게 구성된 작업 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="0061a-115">모든 필요한 hello dll 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-115">All hello required dlls.</span></span> <span data-ttu-id="0061a-116">이러한 dll hello에서 다운로드 [GitHub 리포지토리](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls)합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="0061a-117">`Get-ConfigurationParams.ps1`[스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) hello github 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="0061a-118">단계별 과정</span><span class="sxs-lookup"><span data-stu-id="0061a-118">Step-by-step</span></span>

<span data-ttu-id="0061a-119">Hello 다음 단계 toouse.NET toolaunch 데이터 변환 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="0061a-120">다음 단계 tooretrieve hello 구성 매개 변수를 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="0061a-121">Hello 다운로드 `Get-ConfigurationParams.ps1` hello github 리포지토리 스크립트에서 `C:\DataTransformation` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="0061a-122">Hello 실행 `Get-ConfigurationParams.ps1` hello github 리포지토리에서 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="0061a-123">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="0061a-124">ActiveDirectoryKey 및 AppName hello에 대 한 값에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="0061a-125">이 스크립트는 다음 값에는 hello를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="0061a-126">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="0061a-126">Client ID</span></span>
    * <span data-ttu-id="0061a-127">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="0061a-127">Tenant ID</span></span>
    * <span data-ttu-id="0061a-128">Active Directory 키 (동일: hello 위에 입력 한 하나)</span><span class="sxs-lookup"><span data-stu-id="0061a-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="0061a-129">구독 ID</span><span class="sxs-lookup"><span data-stu-id="0061a-129">Subscription ID</span></span>

3. <span data-ttu-id="0061a-130">Visual Studio 2012, 2013 또는 2015를 사용하여 C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="0061a-131">**Visual Studio 2012/2013/2015**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="0061a-132">클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="0061a-133">**템플릿**을 확장하고 **Visual C#**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="0061a-134">선택 **콘솔 응용 프로그램** hello hello 오른쪽에 프로젝트 형식 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="0061a-135">입력 **DataTransformationApp** hello에 대 한 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="0061a-136">선택 **C:\DataTransformation** hello에 대 한 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="0061a-137">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="0061a-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="0061a-138">이제 hello에 있는 모든 Dll을 추가 [dll](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) 폴더 **참조** 만든 hello 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="0061a-139">toodownload hello dll 파일을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="0061a-140">Visual Studio에서 이동 너무**보기 > 솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="0061a-141">데이터 변환 응용 프로젝트의 hello 화살표 toohello 왼쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="0061a-142">클릭 **참조** 다음 마우스 오른쪽 단추로 너무**참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="0061a-143">Hello 패키지 폴더의 toohello 위치 찾아보기 hello Dll을 모두 선택 하 고 클릭 **추가**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="0061a-144">Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일 (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="0061a-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="0061a-145">코드 다음 hello hello 데이터 변환 작업 인스턴스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="0061a-146">Hello에 추가 **Main 메서드에**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="0061a-147">Hello 이전에 얻은 구성 매개 변수 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="0061a-148">Hello 값의 연결 **리소스 그룹 이름은** 및 **하이브리드 데이터 리소스 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="0061a-149">hello **리소스 그룹 이름은** hello 하이브리드 데이터 리소스는 hello에 구성 된 작업 정의 호스트 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

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

7. <span data-ttu-id="0061a-150">매개 변수는 hello로 작업 정의 필요한 toobe 실행할 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="0061a-151">또는</span><span class="sxs-lookup"><span data-stu-id="0061a-151">(OR)</span></span>

    <span data-ttu-id="0061a-152">런타임 동안 toochange hello 작업 정의 매개 변수를 원하는 경우 hello 코드 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

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

8. <span data-ttu-id="0061a-153">Hello 초기화 된 후 코드 tootrigger hello 작업 정의에 데이터 변환 작업을 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="0061a-154">적절 한 hello 연결 **작업 정의 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="0061a-155">이 작업 hello StorSimple 볼륨 toohello 지정 된 컨테이너에서 hello 루트 디렉터리 아래에 있는 일치 하는 hello 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="0061a-156">Hello 큐에 메시지를 삭제할 파일을 업로드 (hello에 hello 컨테이너와 동일한 저장소 계정) hello로 이름이 hello 작업 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="0061a-157">이 메시지는 더 이상 hello 파일의 처리 트리거 tooinitiate로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="0061a-158">Hello 작업이 트리거 되었습니다, 되 면 hello 코드 tootrack hello 작업 완료에 대 한 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="0061a-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0061a-159">Next steps</span></span>

<span data-ttu-id="0061a-160">[데이터 tootransform StorSimple 데이터 관리자 UI를 사용 하 여](storsimple-data-manager-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0061a-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
