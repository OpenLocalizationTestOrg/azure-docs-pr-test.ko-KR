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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="7f1ea-104">프로그래밍 방식으로 Stream Analytics 작업 모니터 만들기</span><span class="sxs-lookup"><span data-stu-id="7f1ea-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="7f1ea-105">이 문서에서는 방법을 tooenable 스트림 분석 작업에 대 한 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="7f1ea-106">REST API, Azure SDK 또는 PowerShell을 통해 생성된 Stream Analytics 작업은 기본적으로 모니터링이 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="7f1ea-107">사용할 수 있습니다 수동으로 hello Azure 포털에서에서 toohello 작업 모니터 페이지를 이동 하 여 단추를 사용 hello를 클릭 하 또는 hello이이 문서의 단계를 수행 하 여이 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="7f1ea-108">데이터를 모니터링 하는 hello hello 스트림 분석 작업에 대 한 Azure 포털의 hello 메트릭 영역에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f1ea-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f1ea-109">Prerequisites</span></span>

<span data-ttu-id="7f1ea-110">이 프로세스를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="7f1ea-111">Visual Studio 2017 또는 2015</span><span class="sxs-lookup"><span data-stu-id="7f1ea-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="7f1ea-112">[Azure.NET SDK](https://azure.microsoft.com/downloads/) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="7f1ea-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="7f1ea-113">Toohave 모니터링을 사용 하도록 설정 해야 하는 기존 스트림 분석 작업</span><span class="sxs-lookup"><span data-stu-id="7f1ea-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7f1ea-114">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7f1ea-114">Create a project</span></span>

1. <span data-ttu-id="7f1ea-115">Visual Studio C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="7f1ea-116">패키지 관리자 콘솔 hello 실행된 hello 다음 tooinstall hello NuGet 패키지를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="7f1ea-117">hello 먼저 하나는 hello Azure 스트림 분석 관리.NET SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="7f1ea-118">hello 두 번째 메서드는 사용 되는 Azure 모니터 SDK hello tooenable 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="7f1ea-119">hello 마지막 하나인 hello Azure Active Directory 클라이언트 인증을 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="7f1ea-120">Hello 다음 appSettings 섹션 toohello App.config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-120">Add hello following appSettings section toohello App.config file.</span></span>
   
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
   <span data-ttu-id="7f1ea-121">*SubscriptionId*와 *ActiveDirectoryTenantId*의 값을 Azure 구독 및 테넌트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="7f1ea-122">Hello 다음 PowerShell cmdlet을 실행 하 여 이러한 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="7f1ea-123">Hello 다음 추가 hello 프로젝트의 문을 toohello 원본 파일 (Program.cs)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
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
5. <span data-ttu-id="7f1ea-124">인증 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="7f1ea-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="7f1ea-125">public static string GetAuthorizationHeader()</span></span>
   
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
     <span data-ttu-id="7f1ea-126">}</span><span class="sxs-lookup"><span data-stu-id="7f1ea-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="7f1ea-127">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="7f1ea-127">Create management clients</span></span>

<span data-ttu-id="7f1ea-128">hello 다음 코드에서는 설정 hello 필요한 변수 및 관리 클라이언트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-128">hello following code will set up hello necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="7f1ea-129">기존 Stream Analytics 작업에 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="7f1ea-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="7f1ea-130">hello 다음 코드에 대 한 모니터링을 사용 하도록 설정 된 **기존** 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="7f1ea-131">hello 코드의 첫 번째 부분 hello hello hello 특정 스트림 분석 작업에 대 한 스트림 분석 서비스 tooretrieve 정보에 대 한 GET 요청을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="7f1ea-132">Hello를 사용 하 여 *Id* 속성 (hello GET 요청 으로부터 검색 됨) hello Put 메서드 hello에 대 한 매개 변수로 toohello Insights PUT 요청을 전송 하는 hello 코드의 두 번째 절반 서비스 tooenable hello 스트림 분석에 대 한 모니터링 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="7f1ea-133">이전에 사용 하는 경우 hello 아래 코드를 통해 hello Azure 포털을 통해 또는 프로그래밍 방식으로 다른 스트림 분석 작업에 대 한 모니터링 **hello를 제공 하는 것이 좋습니다 때 사용 하는 동일한 저장소 계정 이름을 있습니다 이전에 모니터링을 사용할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="7f1ea-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="7f1ea-134">hello 저장소 계정은 스트림 분석 작업에서 toohello 작업 자체가 명시적으로 만든 연결 된 toohello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="7f1ea-135">모든 스트림 분석 작업 (및 다른 모든 Azure 리소스)는 동일한 지역에이 저장소 계정 toostore 모니터링 데이터를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="7f1ea-136">다른 저장소 계정을 제공 하는 경우 다른 스트림 분석 작업 또는 기타 Azure 리소스에 대 한 모니터링을 hello에 의도 하지 않은 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="7f1ea-137">hello tooreplace를 사용 하는 저장소 계정 이름을 `<YOUR STORAGE ACCOUNT NAME>` hello 코드 다음에 hello에 있는 저장소 계정 이어야 합니다 동일한 구독에 대 한 모니터링 설정 하는 hello 스트림 분석 작업으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="7f1ea-138">지원 받기</span><span class="sxs-lookup"><span data-stu-id="7f1ea-138">Get support</span></span>

<span data-ttu-id="7f1ea-139">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f1ea-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f1ea-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7f1ea-140">Next steps</span></span>

* [<span data-ttu-id="7f1ea-141">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="7f1ea-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7f1ea-142">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="7f1ea-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7f1ea-143">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="7f1ea-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7f1ea-144">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="7f1ea-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7f1ea-145">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="7f1ea-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

