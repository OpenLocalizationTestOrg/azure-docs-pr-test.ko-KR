---
title: "프로그래밍 방식으로 Stream Analytics에서 작업 모니터링| Microsoft Docs"
description: "REST API, Azure SDK 또는 PowerShell을 통해 생성된 Stream Analytics 작업을 프로그래밍 방식으로 모니터링하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="5a5de-104">프로그래밍 방식으로 Stream Analytics 작업 모니터 만들기</span><span class="sxs-lookup"><span data-stu-id="5a5de-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="5a5de-105">이 문서에서는 Stream Analytics 작업에 대한 모니터링을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="5a5de-106">REST API, Azure SDK 또는 PowerShell을 통해 생성된 Stream Analytics 작업은 기본적으로 모니터링이 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="5a5de-107">작업의 모니터 페이지로 이동하고 사용 버튼을 클릭하여 Azure Portal에서 수동으로 설정하거나 이 문서의 단계를 수행하여 이 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="5a5de-108">모니터링 데이터는 Stream Analytics 작업에 대해 Azure Portal의 “모니터” 탭에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a5de-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5a5de-109">Prerequisites</span></span>

<span data-ttu-id="5a5de-110">이 프로세스를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="5a5de-111">Visual Studio 2017 또는 2015</span><span class="sxs-lookup"><span data-stu-id="5a5de-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="5a5de-112">[Azure.NET SDK](https://azure.microsoft.com/downloads/) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="5a5de-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="5a5de-113">모니터링 설정이 필요한 기존 Stream Analytics 작업</span><span class="sxs-lookup"><span data-stu-id="5a5de-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="5a5de-114">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5a5de-114">Create a project</span></span>

1. <span data-ttu-id="5a5de-115">Visual Studio C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="5a5de-116">패키지 관리자 콘솔에서 NuGet 패키지를 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="5a5de-117">첫 번째는 Azure Stream Analytics 관리.NET SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="5a5de-118">두 번째는 모니터링을 사용하도록 설정하는 데 사용되는 Azure Monitor SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="5a5de-119">마지막은 인증에 사용되는 Azure Active Directory 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="5a5de-120">다음 appSettings 섹션을 App.config 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-120">Add the following appSettings section to the App.config file.</span></span>
   
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
   <span data-ttu-id="5a5de-121">*SubscriptionId*와 *ActiveDirectoryTenantId*의 값을 Azure 구독 및 테넌트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="5a5de-122">다음 PowerShell cmdlet을 실행하여 이러한 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="5a5de-123">프로젝트의 원본 파일(Program.cs)에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
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
5. <span data-ttu-id="5a5de-124">인증 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="5a5de-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="5a5de-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="5a5de-126">}</span><span class="sxs-lookup"><span data-stu-id="5a5de-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="5a5de-127">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="5a5de-127">Create management clients</span></span>

<span data-ttu-id="5a5de-128">다음 코드는 필수 변수 및 관리 클라이언트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-128">The following code will set up the necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="5a5de-129">기존 Stream Analytics 작업에 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="5a5de-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="5a5de-130">다음 코드는 **기존** Stream Analytics 작업에 모니터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="5a5de-131">코드의 첫 번째 부분은 Stream Analytics 서비스에 대해 GET 요청을 수행하여 특정 Stream Analytics 작업에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="5a5de-132">Stream Analytics 작업에 모니터링을 사용하기 위해 Insights 서비스에 PUT 요청을 보내는 코드의 나머지 부분에서 Put 메서드에 대한 매개 변수로 *Id* 속성(GET 요청에서 검색됨)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="5a5de-133">Azure Portal을 통해 또는 아래 코드를 통해 프로그래밍 방식으로 서로 다른 Stream Analytics 작업에 대한 모니터링을 이전에 설정한 경우, **이전에 모니터링을 활성화했을 때 사용했던 동일한 저장소 계정 이름을 제공하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="5a5de-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="5a5de-134">저장소 계정은 작업 자체에 특정되지 않고 Stream Analytics 작업에서 만든 지역에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="5a5de-135">동일 지역의 모든 Stream Analytics 작업(및 다른 모든 Azure 리소스)은 이 저장소 계정을 공유하여 모니터링 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="5a5de-136">사용자가 다른 저장소 계정을 제공하면, 다른 Stream Analytics 작업 또는 다른 Azure 리소스에 대한 모니터링에 의도하지 않은 부작용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="5a5de-137">다음 코드의 `<YOUR STORAGE ACCOUNT NAME>`을 바꾸는 데 사용한 저장소 계정 이름은 모니터링을 사용할 Stream Analytics 작업과 동일한 구독에 있는 저장소 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a5de-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="5a5de-138">지원 받기</span><span class="sxs-lookup"><span data-stu-id="5a5de-138">Get support</span></span>

<span data-ttu-id="5a5de-139">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a5de-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a5de-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a5de-140">Next steps</span></span>

* [<span data-ttu-id="5a5de-141">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="5a5de-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5a5de-142">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="5a5de-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5a5de-143">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="5a5de-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5a5de-144">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="5a5de-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5a5de-145">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="5a5de-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

