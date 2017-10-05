---
title: "Azure Stream Analytics용 관리 .NET SDK | Microsoft Docs"
description: "Stream Analytics 관리 .NET SDK를 시작합니다. 분석 작업을 설정 및 실행하는 방법에 대해 알아봅니다. 프로젝트, 입력, 출력 및 변환을 만듭니다."
keywords: ".net SDK, 분석 API"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: f9aa812e6e82cc0f72d0cd1fe63058e53f794775
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="8d985-106">관리 .NET SDK: .NET용 Azure Stream Analytics API를 사용하여 분석 작업 설정 및 실행</span><span class="sxs-lookup"><span data-stu-id="8d985-106">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="8d985-107">관리 .NET SDK에서 .NET용 Azure Stream Analytics API를 사용하여 분석 작업을 설정 및 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="8d985-108">프로젝트를 설정하고, 입출력 소스를 만들고, 변환하고, 작업을 시작 및 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="8d985-109">분석 작업에 대해 Blob 저장소 또는 이벤트 허브에서 데이터를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="8d985-110">[.NET용 Stream Analytics API에 대한 관리 참조 설명서](https://msdn.microsoft.com/library/azure/dn889315.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="8d985-111">Azure Stream Analytics은 완전히 관리되는 서비스로, 클라우드의 스트리밍 데이터에 대해 대기 시간이 짧고 확장성이 뛰어난 고가용성의 복합 이벤트 처리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="8d985-112">Stream Analytics 기능은 고객이 데이터 스트림을 분석하도록 스트리밍 작업을 설정하고 거의 실시간으로 분석할 수 있도록 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="8d985-113">이 문서의 샘플 코드를 Azure Stream Analytics Management .NET SDK v2.x 버전으로 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-113">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="8d985-114">레거시(1.x) SDK 버전을 사용하는 샘플 코드는 [Stream Analytics용 관리 .NET SDK v1.x](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-114">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d985-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8d985-115">Prerequisites</span></span>
<span data-ttu-id="8d985-116">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="8d985-117">Visual Studio 2017 또는 2015를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="8d985-118">[Azure .NET SDK](https://azure.microsoft.com/downloads/)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="8d985-119">구독에서 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="8d985-120">다음은 샘플 Azure PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="8d985-121">Azure PowerShell 정보는 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="8d985-122">사용하려는 입력 소스 및 출력 대상을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="8d985-123">샘플 입력 설정 방법에 대한 자세한 지침은 [입력 추가](stream-analytics-add-inputs.md)를 참조하고 샘플 출력 설정 방법에 대한 자세한 지침은 [출력 추가](stream-analytics-add-outputs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="8d985-124">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="8d985-124">Set up a project</span></span>
<span data-ttu-id="8d985-125">.NET용 Stream Analytics API를 사용하여 분석 작업을 만들려면 먼저 프로젝트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="8d985-126">Visual Studio C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="8d985-127">패키지 관리자 콘솔에서 NuGet 패키지를 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="8d985-128">첫 번째는 Azure Stream Analytics 관리.NET SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="8d985-129">두 번째는 Azure 클라이언트 인증에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-129">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="8d985-130">다음 **appSettings** 섹션을 App.config 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-130">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="8d985-131">**SubscriptionId**와 **ActiveDirectoryTenantId**의 값을 Azure 구독 및 테넌트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="8d985-132">다음 Azure PowerShell cmdlet을 실행하여 이러한 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="8d985-133">.csproj 파일에서 다음 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="8d985-134">다음 **using** 문을 프로젝트의 원본 파일(Program.cs)에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="8d985-135">인증 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="8d985-136">스트림 분석 관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="8d985-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="8d985-137">**StreamAnalyticsManagementClient** 개체를 사용하면 입력, 출력 및 변환 등의 작업 구성 요소와 작업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="8d985-138">**Main** 메서드의 시작에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-138">Add the following code to the beginning of the **Main** method:</span></span>

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

<span data-ttu-id="8d985-139">**resourceGroupName** 변수의 값은 이전 단계에서 만들거나 선택한 리소스 그룹의 이름과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="8d985-140">작업 만들기의 자격 증명 프레젠테이션 측면을 자동화하려면 [Azure 리소스 관리자를 사용하여 서비스 주체 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="8d985-141">이 문서의 나머지 섹션에서는 이 코드가 **Main** 메서드의 시작 부분에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="8d985-142">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="8d985-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="8d985-143">다음 코드는 사용자가 정의한 리소스 그룹 아래 Stream Analytics 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="8d985-144">나중에 입력, 출력 및 변환을 작업에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-144">You will add an input, output, and transformation to the job later.</span></span>

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="8d985-145">Stream Analytics 입력 소스 만들기</span><span class="sxs-lookup"><span data-stu-id="8d985-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="8d985-146">다음 코드는 blob 입력 소스 형식 및 CSV serialization으로 Stream Analytics 입력 소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="8d985-147">이벤트 허브 입력 소스를 만들려면 **BlobStreamInputDataSource** 대신 **EventHubStreamInputDataSource**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="8d985-148">마찬가지로, 입력 소스의 serialization 형식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-148">Similarly, you can customize the serialization type of the input source.</span></span>

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

<span data-ttu-id="8d985-149">Blob 저장소 또는 이벤트 허브의 입력 소스는 특정 작업에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="8d985-150">다른 작업에 대해 동일한 입력 소스를 사용하려면, 메서드를 다시 호출하고 다른 작업 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="8d985-151">Stream Analytics 입력 소스 테스트</span><span class="sxs-lookup"><span data-stu-id="8d985-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="8d985-152">**TestConnection** 메서드는 Stream Analytics 작업이 입력 소스 및 입력 소스 유형에 특정한 다른 측면에도 연결할 수 있는지 여부를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="8d985-153">예를 들어 이전 단계에서 만든 blob 입력 소스에서 메서드는 저장소 계정 이름 및 키 쌍을 사용하여 저장소 계정에 연결할 수 있는지를 확인하고 지정된 컨테이너가 존재하는지 점검합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="8d985-154">Stream Analytics 출력 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="8d985-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="8d985-155">출력 대상 만들기는 Stream Analytics 입력 소스 만들기와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="8d985-156">입력 소스와 같이 출력 대상은 특정 작업에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="8d985-157">다른 작업에 대해 동일한 출력 소스를 사용하려면, 메서드를 다시 호출하고 다른 작업 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="8d985-158">다음 코드는 출력 대상(Azure SQL 데이터베이스)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="8d985-159">출력 대상의 데이터 형식 및/또는 serialization 형식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-159">You can customize the output target's data type and/or serialization type.</span></span>

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="8d985-160">Stream Analytics 출력 대상 테스트</span><span class="sxs-lookup"><span data-stu-id="8d985-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="8d985-161">Stream Analytics 출력 대상에는 연결 테스트를 위한 **TestConnection** 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="8d985-162">Stream Analytics 변환 만들기</span><span class="sxs-lookup"><span data-stu-id="8d985-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="8d985-163">다음 코드는 쿼리 "입력에서 *선택"를 사용하여 Stream Analytics 변환을 만들고 Stream Analytics 작업에 대한 하나의 스트리밍 단위를 할당하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="8d985-164">스트리밍 단위 조정에 대한 자세한 내용은 [Azure Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="8d985-165">입력 및 출력의 경우와 마찬가지로 변환은 작성된 특정 Stream Analytics 작업과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="8d985-166">Stream Analytics 작업 시작</span><span class="sxs-lookup"><span data-stu-id="8d985-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="8d985-167">Stream Analytics 작업 및 해당 입력, 출력 및 변환을 만든 후, **Start** 메서드를 호출하여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="8d985-168">다음 샘플 코드는 2012년 12월 12일, 12:12:12 UTC로 시작 시간이 설정된 사용자 지정 출력이 있는 Stream Analytics 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="8d985-169">Stream Analytics 작업 중지</span><span class="sxs-lookup"><span data-stu-id="8d985-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="8d985-170">**Stop** 메서드를 호출하여 실행 중인 Stream Analytics 작업을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="8d985-171">Stream Analytics 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="8d985-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="8d985-172">**Delete** 메서드는 입력, 출력 및 변환 작업을 포함한 기본 하위 리소스 및 작업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="8d985-173">지원 받기</span><span class="sxs-lookup"><span data-stu-id="8d985-173">Get support</span></span>
<span data-ttu-id="8d985-174">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d985-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d985-175">Next steps</span></span>
<span data-ttu-id="8d985-176">.NET SDK를 사용하여 분석 작업을 만들고 실행하는 기본을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8d985-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="8d985-177">자세한 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d985-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="8d985-178">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="8d985-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8d985-179">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="8d985-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8d985-180">Azure Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="8d985-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="8d985-181">[Azure Stream Analytics 관리 .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d985-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="8d985-182">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="8d985-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8d985-183">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="8d985-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
