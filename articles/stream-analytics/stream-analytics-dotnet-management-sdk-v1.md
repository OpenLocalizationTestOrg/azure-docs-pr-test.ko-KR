---
title: "Azure 스트림 분석에 대 한.NET SDK v1.x aaaManagement | Microsoft Docs"
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="33248-106">관리.NET SDK v1.x: 설정 및 런타임된 분석 작업을 사용 하 여.NET 용 Azure 스트림 분석 API hello</span><span class="sxs-lookup"><span data-stu-id="33248-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="33248-107">tooset 및 실행된 분석 작업을 사용 하 여.NET에 대 한 hello 스트림 분석 API를 사용 하 여 관리.NET SDK hello 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33248-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="33248-108">프로젝트를 설정하고, 입출력 소스를 만들고, 변환하고, 작업을 시작 및 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="33248-109">분석 작업에 대해 Blob 저장소 또는 이벤트 허브에서 데이터를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33248-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="33248-110">Hello 참조 [.NET에 대 한 스트림 분석 API hello에 대 한 참조 설명서 관리](https://msdn.microsoft.com/library/azure/dn889315.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="33248-111">Azure Stream Analytics는 스트리밍 데이터 hello 클라우드에 대해 낮은 대기 시간, 고가용성, 확장성, 복잡 한 이벤트 처리를 제공 하는 완전히 관리 되는 서비스.</span><span class="sxs-lookup"><span data-stu-id="33248-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="33248-112">스트림 분석 작업 tooanalyze 데이터 스트림, 스트리밍를 고객 tooset 있으며 toodrive 실시간 분석 근처에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33248-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="33248-113">이 문서의 샘플 코드는 Azure Stream Analytics Management .NET SDK의 레거시(1.x) 버전을 여전히 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="33248-114">Hello 최신 SDK 버전을 사용 하 여 샘플 코드를 참조 하세요 [사용 하 여 hello 스트림 분석에 대 한 관리.NET SDK](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33248-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="33248-115">Prerequisites</span></span>
<span data-ttu-id="33248-116">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="33248-117">Visual Studio 2017 또는 2015를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="33248-118">[Azure .NET SDK](https://azure.microsoft.com/downloads/)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="33248-119">구독에서 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33248-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="33248-120">hello 다음은 샘플 Azure PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="33248-121">Azure PowerShell 정보는 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33248-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="33248-122">입력된 소스를 설정 하 고 대상 toouse 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33248-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="33248-123">에 대 한 참조 추가 [추가 입력](stream-analytics-add-inputs.md) 샘플 입력을 tooset 및 [출력 추가](stream-analytics-add-outputs.md) tooset 샘플 출력을 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="33248-124">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="33248-124">Set up a project</span></span>
<span data-ttu-id="33248-125">toocreate 분석 작업 프로젝트를 먼저 설정 for.net hello 스트림 분석 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="33248-126">Visual Studio C# .NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33248-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="33248-127">패키지 관리자 콘솔 hello 실행된 hello 다음 tooinstall hello NuGet 패키지를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="33248-128">hello 먼저 하나는 hello Azure 스트림 분석 관리.NET SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="33248-129">hello 두 번째 메서드는 hello Azure Active Directory 클라이언트 인증을 위해 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="33248-130">Hello 다음 추가 **appSettings** 섹션 toohello App.config 파일:</span><span class="sxs-lookup"><span data-stu-id="33248-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    <span data-ttu-id="33248-131">**SubscriptionId**와 **ActiveDirectoryTenantId**의 값을 Azure 구독 및 테넌트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="33248-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="33248-132">Hello 다음 Azure PowerShell cmdlet을 실행 하 여 이러한 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33248-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="33248-133">Hello 참조 하 여.csproj 파일에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="33248-134">Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일 (Program.cs):</span><span class="sxs-lookup"><span data-stu-id="33248-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="33248-135">인증 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-135">Add an authentication helper method:</span></span>

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="33248-136">스트림 분석 관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="33248-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="33248-137">A **StreamAnalyticsManagementClient** 개체 있습니다 toomanage hello 작업과 hello 작업 같은 구성 요소, 입력, 출력 및 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="33248-138">Hello의 hello toohello 시작 코드를 다음 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="33248-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

<span data-ttu-id="33248-139">hello **resourceGroupName** 변수의 값 hello 생성 하거나 hello 사전 요구 사항 단계에서 선택한 그룹 hello 리소스의 hello 이름과 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="33248-140">작업 만들기의 tooautomate hello 자격 증명 프레젠테이션 측면 너무 참조[Azure 리소스 관리자와 서비스 사용자를 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="33248-141">hello이 문서의 나머지 단원 들을 가정 hello hello 맨 앞에이 코드는 **Main** 메서드.</span><span class="sxs-lookup"><span data-stu-id="33248-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="33248-142">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="33248-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="33248-143">hello 다음 코드에서는 사용자가 정의한 hello 리소스 그룹 아래의 스트림 분석 작업</span><span class="sxs-lookup"><span data-stu-id="33248-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="33248-144">한 입력, 출력 및 변환 toohello 작업을 나중에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-144">You will add an input, output, and transformation toohello job later.</span></span>

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="33248-145">Stream Analytics 입력 소스 만들기</span><span class="sxs-lookup"><span data-stu-id="33248-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="33248-146">hello 다음 코드에서는 만듭니다 스트림 분석 입력된 소스 hello blob 입력된 소스 형식과 CSV serialization을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="33248-147">toocreate 이벤트 허브 입력된 소스를 사용 하 여 **EventHubStreamInputDataSource** 대신 **BlobStreamInputDataSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="33248-148">마찬가지로, hello 입력 소스의 hello serialization 형식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33248-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

<span data-ttu-id="33248-149">입력된 소스는 Blob 저장소 서비스 또는 이벤트 허브는 동 점된 tooa 특정 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="33248-150">toouse hello 다른 작업에 대 한 동일한 입력된 소스, hello 메서드를 다시 호출 하 고 다른 작업 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="33248-151">Stream Analytics 입력 소스 테스트</span><span class="sxs-lookup"><span data-stu-id="33248-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="33248-152">hello **TestConnection** 메서드 테스트 소스 뿐 아니라 다른 측면 특정 toohello 입력 hello 스트림 분석 작업 수 tooconnect toohello 인지 입력 원본 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="33248-153">예를 들어 hello blob 입력된 소스를 이전 단계에서 만든 hello 메서드는 hello 저장소 계정 이름과 키 쌍 수 사용된 tooconnect toohello 저장소 계정 수으로 해당 hello 지정 된 컨테이너의 존재 확인 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33248-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="33248-154">Stream Analytics 출력 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="33248-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="33248-155">출력 대상으로 만드는 매우 유사한 toocreating 스트림 분석 입력된 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="33248-156">입력된 소스 처럼 출력 대상이 동률된 tooa 특정 작업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33248-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="33248-157">toouse hello 다른 작업에 대 한 동일한 출력 대상, hello 메서드를 다시 호출 하 고 다른 작업 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="33248-158">hello 코드 다음 출력 대상 (Azure SQL 데이터베이스)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33248-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="33248-159">Hello 출력 대상 데이터 형식 및/또는 serialization 형식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33248-159">You can customize hello output target's data type and/or serialization type.</span></span>

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="33248-160">Stream Analytics 출력 대상 테스트</span><span class="sxs-lookup"><span data-stu-id="33248-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="33248-161">스트림 분석 출력 대상 역시 hello **TestConnection** 연결을 테스트 하기 위한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="33248-162">Stream Analytics 변환 만들기</span><span class="sxs-lookup"><span data-stu-id="33248-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="33248-163">hello 다음 코드에서는 스트림 분석 변환 hello 쿼리로 "선택 * 입력에서" hello 스트림 분석 작업에 대 한 tooallocate 하나의 스트리밍 단위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="33248-164">스트리밍 단위 조정에 대한 자세한 내용은 [Azure Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33248-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

<span data-ttu-id="33248-165">입력 및 출력 마찬가지로 변환은 또한 동률된 toohello 특정 스트림 분석 작업에서 만들어진입니다.</span><span class="sxs-lookup"><span data-stu-id="33248-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="33248-166">Stream Analytics 작업 시작</span><span class="sxs-lookup"><span data-stu-id="33248-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="33248-167">스트림 분석 작업 및 미터링, 출력 및 변환을 만든 후 호출 hello 여 hello 작업을 시작할 수 있습니다 **시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="33248-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="33248-168">다음 샘플 코드는 hello는 사용자 지정 출력 시작 시간 집합 tooDecember 12, 2012, 12시 12분: 12로 스트림 분석 작업 시작 UTC:</span><span class="sxs-lookup"><span data-stu-id="33248-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="33248-169">Stream Analytics 작업 중지</span><span class="sxs-lookup"><span data-stu-id="33248-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="33248-170">호출 hello 여 스트림 분석 작업의 실행을 중지할 수 있습니다 **중지** 메서드.</span><span class="sxs-lookup"><span data-stu-id="33248-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="33248-171">Stream Analytics 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="33248-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="33248-172">hello **삭제** 메서드 hello 작업 뿐만 아니라 hello 입력, 출력으로 hello 작업의 변환 등 하위 리소스를 내부에 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33248-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="33248-173">지원 받기</span><span class="sxs-lookup"><span data-stu-id="33248-173">Get support</span></span>
<span data-ttu-id="33248-174">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33248-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33248-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33248-175">Next steps</span></span>
<span data-ttu-id="33248-176">.NET SDK toocreate를 사용 하 여 hello 기본 사항 학습 되었으며 분석 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="33248-177">더 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="33248-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="33248-178">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="33248-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="33248-179">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="33248-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="33248-180">Azure Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="33248-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="33248-181">[Azure Stream Analytics 관리 .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="33248-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="33248-182">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="33248-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="33248-183">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="33248-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
