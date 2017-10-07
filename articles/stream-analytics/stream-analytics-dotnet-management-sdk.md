---
title: "Azure 스트림 분석에 대 한.NET SDK aaaManagement | Microsoft Docs"
description: "Stream Analytics 관리 .NET SDK를 시작합니다. 자세한 내용은 방법 tooset 및 분석 작업을 실행 합니다. 프로젝트, 입력, 출력 및 변환을 만듭니다."
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
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>.NET SDK 관리: 설치 하 고 hello Azure 스트림 분석 API를 사용 하 여.NET에 대 한 분석 작업 실행
tooset 및 실행된 분석 작업을 사용 하 여.NET에 대 한 hello 스트림 분석 API를 사용 하 여 관리.NET SDK hello 방법에 대해 알아봅니다. 프로젝트를 설정하고, 입출력 소스를 만들고, 변환하고, 작업을 시작 및 중지합니다. 분석 작업에 대해 Blob 저장소 또는 이벤트 허브에서 데이터를 스트리밍할 수 있습니다.

Hello 참조 [.NET에 대 한 스트림 분석 API hello에 대 한 참조 설명서 관리](https://msdn.microsoft.com/library/azure/dn889315.aspx)합니다.

Azure Stream Analytics는 스트리밍 데이터 hello 클라우드에 대해 낮은 대기 시간, 고가용성, 확장성, 복잡 한 이벤트 처리를 제공 하는 완전히 관리 되는 서비스. 스트림 분석 작업 tooanalyze 데이터 스트림, 스트리밍를 고객 tooset 있으며 toodrive 실시간 분석 근처에 있습니다.  

> [!NOTE]
> 우리는이 문서에 hello 샘플 코드 Azure 스트림 분석 관리.NET SDK v2.x 버전으로 업데이트. Lagecy (1.x) SDK 버전을 사용 하는 hello를 사용 하 여 샘플 코드에 대 한 참조 하십시오 [스트림 분석에 대 한 관리.NET SDK v1.x hello를 사용 하 여](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1)합니다.

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* Visual Studio 2017 또는 2015를 설치합니다.
* [Azure .NET SDK](https://azure.microsoft.com/downloads/)를 다운로드하여 설치합니다.
* 구독에서 Azure 리소스 그룹을 만듭니다. hello 다음은 샘플 Azure PowerShell 스크립트입니다. Azure PowerShell 정보는 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* 입력된 소스를 설정 하 고 대상 toouse 출력 됩니다. 에 대 한 참조 추가 [추가 입력](stream-analytics-add-inputs.md) 샘플 입력을 tooset 및 [출력 추가](stream-analytics-add-outputs.md) tooset 샘플 출력을 합니다.

## <a name="set-up-a-project"></a>프로젝트 설정
toocreate 분석 작업 프로젝트를 먼저 설정 for.net hello 스트림 분석 API를 사용 합니다.

1. Visual Studio C# .NET 콘솔 응용 프로그램을 만듭니다.
2. 패키지 관리자 콘솔 hello 실행된 hello 다음 tooinstall hello NuGet 패키지를 명령입니다. hello 먼저 하나는 hello Azure 스트림 분석 관리.NET SDK입니다. hello 두 번째 메서드는 Azure 클라이언트 인증에 대 한 합니다.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Hello 다음 추가 **appSettings** 섹션 toohello App.config 파일:
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    **SubscriptionId**와 **ActiveDirectoryTenantId**의 값을 Azure 구독 및 테넌트 ID로 바꿉니다. Hello 다음 Azure PowerShell cmdlet을 실행 하 여 이러한 값을 얻을 수 있습니다.

        Get-AzureAccount

4. Hello 참조 하 여.csproj 파일에서 다음을 추가 합니다.

        <Reference Include="System.Configuration" />

5. Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일 (Program.cs):
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. 인증 도우미 메서드를 추가합니다.

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>스트림 분석 관리 클라이언트 만들기
A **StreamAnalyticsManagementClient** 개체 있습니다 toomanage hello 작업과 hello 작업 같은 구성 요소, 입력, 출력 및 변환 합니다.

Hello의 hello toohello 시작 코드를 다음 추가 **Main** 메서드:

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

hello **resourceGroupName** 변수의 값 hello 생성 하거나 hello 사전 요구 사항 단계에서 선택한 그룹 hello 리소스의 hello 이름과 동일 해야 합니다.

작업 만들기의 tooautomate hello 자격 증명 프레젠테이션 측면 너무 참조[Azure 리소스 관리자와 서비스 사용자를 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)합니다.

hello이 문서의 나머지 단원 들을 가정 hello hello 맨 앞에이 코드는 **Main** 메서드.

## <a name="create-a-stream-analytics-job"></a>Stream Analytics 작업 만들기
hello 다음 코드에서는 사용자가 정의한 hello 리소스 그룹 아래의 스트림 분석 작업 한 입력, 출력 및 변환 toohello 작업을 나중에 추가 합니다.

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

## <a name="create-a-stream-analytics-input-source"></a>Stream Analytics 입력 소스 만들기
hello 다음 코드에서는 만듭니다 스트림 분석 입력된 소스 hello blob 입력된 소스 형식과 CSV serialization을 사용 합니다. toocreate 이벤트 허브 입력된 소스를 사용 하 여 **EventHubStreamInputDataSource** 대신 **BlobStreamInputDataSource**합니다. 마찬가지로, hello 입력 소스의 hello serialization 형식을 사용자 지정할 수 있습니다.

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

입력된 소스는 Blob 저장소 서비스 또는 이벤트 허브는 동 점된 tooa 특정 작업입니다. toouse hello 다른 작업에 대 한 동일한 입력된 소스, hello 메서드를 다시 호출 하 고 다른 작업 이름을 지정 해야 합니다.

## <a name="test-a-stream-analytics-input-source"></a>Stream Analytics 입력 소스 테스트
hello **TestConnection** 메서드 테스트 소스 뿐 아니라 다른 측면 특정 toohello 입력 hello 스트림 분석 작업 수 tooconnect toohello 인지 입력 원본 유형입니다. 예를 들어 hello blob 입력된 소스를 이전 단계에서 만든 hello 메서드는 hello 저장소 계정 이름과 키 쌍 수 사용된 tooconnect toohello 저장소 계정 수으로 해당 hello 지정 된 컨테이너의 존재 확인 확인 됩니다.

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Stream Analytics 출력 대상 만들기
출력 대상으로 만드는 매우 유사한 toocreating 스트림 분석 입력된 소스입니다. 입력된 소스 처럼 출력 대상이 동률된 tooa 특정 작업 됩니다. toouse hello 다른 작업에 대 한 동일한 출력 대상, hello 메서드를 다시 호출 하 고 다른 작업 이름을 지정 해야 합니다.

hello 코드 다음 출력 대상 (Azure SQL 데이터베이스)를 만듭니다. Hello 출력 대상 데이터 형식 및/또는 serialization 형식을 사용자 지정할 수 있습니다.

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

## <a name="test-a-stream-analytics-output-target"></a>Stream Analytics 출력 대상 테스트
스트림 분석 출력 대상 역시 hello **TestConnection** 연결을 테스트 하기 위한 방법입니다.

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Stream Analytics 변환 만들기
hello 다음 코드에서는 스트림 분석 변환 hello 쿼리로 "선택 * 입력에서" hello 스트림 분석 작업에 대 한 tooallocate 하나의 스트리밍 단위를 지정 합니다. 스트리밍 단위 조정에 대한 자세한 내용은 [Azure Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)을 참조하세요.

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

입력 및 출력 마찬가지로 변환은 또한 동률된 toohello 특정 스트림 분석 작업에서 만들어진입니다.

## <a name="start-a-stream-analytics-job"></a>Stream Analytics 작업 시작
스트림 분석 작업 및 미터링, 출력 및 변환을 만든 후 호출 hello 여 hello 작업을 시작할 수 있습니다 **시작** 메서드.

다음 샘플 코드는 hello는 사용자 지정 출력 시작 시간 집합 tooDecember 12, 2012, 12시 12분: 12로 스트림 분석 작업 시작 UTC:

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>Stream Analytics 작업 중지
호출 hello 여 스트림 분석 작업의 실행을 중지할 수 있습니다 **중지** 메서드.

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Stream Analytics 작업 삭제
hello **삭제** 메서드 hello 작업 뿐만 아니라 hello 입력, 출력으로 hello 작업의 변환 등 하위 리소스를 내부에 삭제 됩니다.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>지원 받기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
.NET SDK toocreate를 사용 하 여 hello 기본 사항 학습 되었으며 분석 작업을 실행 합니다. 더 toolearn hello 다음을 참조 합니다.

* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 관리 .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).
* [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
