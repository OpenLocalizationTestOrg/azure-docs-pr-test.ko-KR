---
title: "스트림 분석에서 작업 aaaProgrammatically 모니터링 | Microsoft Docs"
description: "Tooprogrammatically REST Api, Azure SDK 또는 PowerShell을 통해 만든 스트림 분석 작업을 모니터링 하는 방법에 대해 알아봅니다."
keywords: ".net 모니터, 작업 모니터, 응용 프로그램 모니터링"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>프로그래밍 방식으로 Stream Analytics 작업 모니터 만들기

이 문서에서는 방법을 tooenable 스트림 분석 작업에 대 한 모니터링 합니다. REST API, Azure SDK 또는 PowerShell을 통해 생성된 Stream Analytics 작업은 기본적으로 모니터링이 설정되어 있지 않습니다. 사용할 수 있습니다 수동으로 hello Azure 포털에서에서 toohello 작업 모니터 페이지를 이동 하 여 단추를 사용 hello를 클릭 하 또는 hello이이 문서의 단계를 수행 하 여이 프로세스를 자동화할 수 있습니다. 데이터를 모니터링 하는 hello hello 스트림 분석 작업에 대 한 Azure 포털의 hello 메트릭 영역에 표시 됩니다.

## <a name="prerequisites"></a>필수 조건

이 프로세스를 시작 하기 전에 hello 다음이 있어야 합니다.

* Visual Studio 2017 또는 2015
* [Azure.NET SDK](https://azure.microsoft.com/downloads/) 다운로드 및 설치
* Toohave 모니터링을 사용 하도록 설정 해야 하는 기존 스트림 분석 작업

## <a name="create-a-project"></a>프로젝트 만들기

1. Visual Studio C# .NET 콘솔 응용 프로그램을 만듭니다.
2. 패키지 관리자 콘솔 hello 실행된 hello 다음 tooinstall hello NuGet 패키지를 명령입니다. hello 먼저 하나는 hello Azure 스트림 분석 관리.NET SDK입니다. hello 두 번째 메서드는 사용 되는 Azure 모니터 SDK hello tooenable 모니터링 합니다. hello 마지막 하나인 hello Azure Active Directory 클라이언트 인증을 위해 사용 됩니다.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Hello 다음 appSettings 섹션 toohello App.config 파일을 추가 합니다.
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   *SubscriptionId*와 *ActiveDirectoryTenantId*의 값을 Azure 구독 및 테넌트 ID로 바꿉니다. Hello 다음 PowerShell cmdlet을 실행 하 여 이러한 값을 얻을 수 있습니다.
   
   ```
   Get-AzureAccount
   ```
4. Hello 다음 추가 hello 프로젝트의 문을 toohello 원본 파일 (Program.cs)을 사용 합니다.
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. 인증 도우미 메서드를 추가합니다.
   
     public static string GetAuthorizationHeader()
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     }

## <a name="create-management-clients"></a>관리 클라이언트 만들기

hello 다음 코드에서는 설정 hello 필요한 변수 및 관리 클라이언트 합니다.

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>기존 Stream Analytics 작업에 모니터링 사용

hello 다음 코드에 대 한 모니터링을 사용 하도록 설정 된 **기존** 스트림 분석 작업 합니다. hello 코드의 첫 번째 부분 hello hello hello 특정 스트림 분석 작업에 대 한 스트림 분석 서비스 tooretrieve 정보에 대 한 GET 요청을 수행합니다. Hello를 사용 하 여 *Id* 속성 (hello GET 요청 으로부터 검색 됨) hello Put 메서드 hello에 대 한 매개 변수로 toohello Insights PUT 요청을 전송 하는 hello 코드의 두 번째 절반 서비스 tooenable hello 스트림 분석에 대 한 모니터링 작업입니다.

>[!WARNING]
>이전에 사용 하는 경우 hello 아래 코드를 통해 hello Azure 포털을 통해 또는 프로그래밍 방식으로 다른 스트림 분석 작업에 대 한 모니터링 **hello를 제공 하는 것이 좋습니다 때 사용 하는 동일한 저장소 계정 이름을 있습니다 이전에 모니터링을 사용할 수 있습니다.**
> 
> hello 저장소 계정은 스트림 분석 작업에서 toohello 작업 자체가 명시적으로 만든 연결 된 toohello 영역입니다.
> 
> 모든 스트림 분석 작업 (및 다른 모든 Azure 리소스)는 동일한 지역에이 저장소 계정 toostore 모니터링 데이터를 공유 합니다. 다른 저장소 계정을 제공 하는 경우 다른 스트림 분석 작업 또는 기타 Azure 리소스에 대 한 모니터링을 hello에 의도 하지 않은 결과가 발생할 수 있습니다.
> 
> hello tooreplace를 사용 하는 저장소 계정 이름을 `<YOUR STORAGE ACCOUNT NAME>` hello 코드 다음에 hello에 있는 저장소 계정 이어야 합니다 동일한 구독에 대 한 모니터링 설정 하는 hello 스트림 분석 작업으로 합니다.
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a>지원 받기

추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

