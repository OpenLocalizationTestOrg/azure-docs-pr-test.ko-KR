---
title: "Azure.NET SDK를 사용 하 여 자신만 데이터 파이프라인 aaaCreate | Microsoft Docs"
description: "Tooprogrammatically를 만들기, 모니터링 및 데이터 팩터리 SDK를 사용 하 여 Azure 데이터 팩터리를 관리 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Azure Data Factory .NET SDK를 사용하여 Azure Data Factory 만들기, 모니터링 및 관리
## <a name="overview"></a>개요
데이터 팩터리 .NET SDK를 사용하여 프로그래밍 방식으로 Azure Data Factory를 만들고, 모니터링하며, 관리할 수 있습니다. 이 문서를 만들고 데이터 팩터리를 모니터링 하는 샘플.NET 콘솔 응용 프로그램 toocreate 참고할 수 있는 연습이 포함 되어 있습니다. 

> [!NOTE]
> 이 문서에서 모든 hello 데이터 팩터리.NET API를 다루지 않습니다. 데이터 팩터리용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요. 

## <a name="prerequisites"></a>필수 조건
* Visual Studio 2012, 2013 또는 2015
* [Azure .NET SDK](http://azure.microsoft.com/downloads/)를 다운로드하여 설치합니다.
* Azure PowerShell. 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 컴퓨터에 Azure PowerShell tooinstall 문서입니다. Azure PowerShell toocreate Azure Active Directory 응용 프로그램을 사용 합니다.

### <a name="create-an-application-in-azure-active-directory"></a>Azure Active Directory에서 응용 프로그램 만들기
Azure Active Directory 응용 프로그램을 만들고 hello 응용 프로그램에 대 한 서비스 사용자를 만들, toohello 할당 **데이터 팩터리 참가자** 역할입니다.

1. **PowerShell**을 시작합니다.
2. Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. 이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. 다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다. 대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > 기록해 두고 **SubscriptionId** 및 **TenantId** hello이이 명령의 출력에서 합니다.

5. 라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 hello PowerShell에서에서 명령을 실행 하 여 합니다.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Hello 리소스 그룹이 이미 있는 경우, 지정 여부 tooupdate 것 (Y) 하거나 (N)로 유지 합니다.

    다른 리소스 그룹을 사용 하는 경우이 자습서의 ADFTutorialResourceGroup 대신 리소스 그룹의 toouse hello 이름이 필요 합니다.
6. Azure Active Directory 응용 프로그램을 만듭니다.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    Hello 다음 오류가 발생 하는 경우 다른 URL을 지정 하 고 hello 명령을 다시 실행 합니다.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Hello AD 서비스 사용자를 만듭니다.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. 서비스 보안 주체 toohello 추가 **데이터 팩터리 참가자** 역할입니다.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Hello 응용 프로그램 ID를 가져옵니다.

    ```PowerShell
    $azureAdApplication 
    ```
    Hello hello 출력에서 응용 프로그램 ID (applicationID) 아래로 note 합니다.

이 단계에서 다음과 같은 4가지 값이 있어야 합니다.

* 테넌트 ID
* 구독 ID
* 응용 프로그램 UI
* 암호 (hello 첫 번째 명령에 지정 됨)

## <a name="walkthrough"></a>연습
Hello 연습 복사 작업을 포함 하는 파이프라인을 사용 하 여 데이터 팩터리를 만듭니다. hello 복사 활동 데이터를 복사 hello에 Azure blob 저장소 tooanother 폴더에 폴더에서 동일한 blob 저장소입니다. 

Azure Data Factory에 hello 데이터 이동을 수행 하는 hello 복사 작업 합니다. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. 참조 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업에 대 한 세부 정보에 대 한 문서입니다.

1. Visual Studio 2012/2013/2015를 사용하여 C# .NET 콘솔 응용 프로그램을 만듭니다.
   1. **Visual Studio** 2012/2013/2015를 실행합니다.
   2. 클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.
   3. **템플릿**을 확장하고 **Visual C#**를 선택합니다. 이 연습에서는 C#을 사용하지만 모든 .NET 언어를 사용할 수 있습니다.
   4. 선택 **콘솔 응용 프로그램** hello hello 오른쪽에 프로젝트 형식 목록에서 합니다.
   5. 입력 **DataFactoryAPITestApp** hello 이름에 대 한 합니다.
   6. 선택 **C:\ADFGetStarted** hello 위치에 대 한 합니다.
   7. 클릭 **확인** toocreate hello 프로젝트.
2. 클릭 **도구**, 너무 가리킨**NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.
3. Hello에 **패키지 관리자 콘솔**, 다음 단계 hello지 않습니다.
   1. 다음 명령 tooinstall Data Factory 패키지 hello를 실행 합니다.`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Hello 명령 tooinstall Azure Active Directory 패키지 (Active Directory API 코드에서 사용 hello) 다음을 실행 합니다.`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Hello 내용 바꾸기 **App.config** 콘텐츠를 다음 hello로 hello 프로젝트 파일에에서: 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. Hello App.Config 파일에 대 한 값을 업데이트  **&lt;응용 프로그램 ID&gt;**,  **&lt;암호&gt;**,  **&lt; 구독 ID&gt;**, 및  **&lt;테 넌 트 ID&gt;**  고유한 값으로.
6. Hello 다음 추가 **를 사용 하 여** 문 toohello **Program.cs** hello 프로젝트 파일에에서 있습니다.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. 인스턴스를 만드는 코드 다음 hello 추가 **DataPipelineManagementClient** 클래스 toohello **Main** 메서드. 이 개체 toocreate을 사용 하 여 데이터 팩터리, 연결된 된 서비스, 입력 및 출력 데이터 집합 및 파이프라인. 또한 런타임에 데이터 집합의 개체 toomonitor 조각을이 사용합니다.

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Hello 값의 대체 **resourceGroupName** hello Azure 리소스 그룹 이름으로 합니다. Hello를 사용 하 여 리소스 그룹을 만들 수 [새로 AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.
   >
   > Hello 데이터 팩터리 () toobe 고유의 이름을 업데이트 합니다. Hello 데이터 팩터리의 이름을 전역적으로 고유 해야 합니다. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.
7. 추가 코드를 만드는 다음 hello는 **데이터 팩터리의** toohello **Main** 메서드.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. 추가 코드를 만드는 다음 hello는 **Azure 저장소 연결 된 서비스** toohello **Main** 메서드.

   > [!IMPORTANT]
   > **storageaccountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. 추가 코드를 만드는 다음 hello **입력 및 출력 데이터 집합** toohello **Main** 메서드.

    hello **FolderPath** hello 입력된 blob 너무 설정 되어**adftutorial /** 여기서 **adftutorial** hello hello 컨테이너 blob 저장소의 이름입니다. 이 컨테이너 Azure blob 저장소에 없는 경우이 이름을 가진 컨테이너 만들기: **adftutorial** 및 텍스트 파일 toohello 컨테이너를 업로드 합니다.

    hello FolderPath hello에 대 한 출력 blob로 설정 되어: **adftutorial/apifactoryoutput {Slice} /** 여기서 **조각** 값인지에 따라 동적으로 계산 된 hello **SliceStart**(날짜-시간 각 조각의 시작 합니다.)

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. Hello 다음 코드를 추가 **가 만들어지고 활성화 파이프라인** toohello **Main** 메서드. 이 파이프라인에는 **BlobSource**를 원본으로 사용하고 **BlobSink**를 싱크로 사용하는 **CopyActivity**가 포함되어 있습니다.

    Azure Data Factory에 hello 데이터 이동을 수행 하는 hello 복사 작업 합니다. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. 참조 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업에 대 한 세부 정보에 대 한 문서입니다.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. 다음 코드 toohello hello 추가 **Main** hello의 데이터 조각 방법 tooget hello 상태 출력 데이터 집합입니다. 이 샘플에서는 한 개의 조각만 필요합니다.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **(선택 사항)**  추가 hello 다음 데이터 조각 toohello에 대 한 실행 tooget 세부 정보를 코드 **Main** 메서드.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. Hello hello에서 사용 하는 도우미 메서드를 다음 추가 **Main** 메서드 toohello **프로그램** 클래스입니다. 이 메서드를 사용 하면 제공할 수 있는 대화 상자를 팝 **사용자 이름** 및 **암호** tooAzure 포털에서 toolog를 사용 합니다.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. Hello 솔루션 탐색기에서에서 프로젝트 hello 확장: **DataFactoryAPITestApp**를 마우스 오른쪽 단추로 클릭 **참조**를 클릭 하 고 **참조 추가**합니다. `System.Configuration` 어셈블리에 대한 확인란을 선택하고 **확인**을 클릭합니다.
15. Hello 콘솔 응용 프로그램을 빌드하십시오. 클릭 **빌드** hello 메뉴에 **솔루션 빌드**합니다.
16. Azure blob 저장소에 hello adftutorial 컨테이너에 파일을 하나 이상 있는지 확인 합니다. 그렇지 않으면 Emp.txt 파일을 메모장에서에서 다음 hello로 콘텐츠 만들고 toohello adftutorial 컨테이너를 업로드 합니다.

    ```
    John, Doe
    Jane, Doe
    ```
17. 클릭 하 여 hello 샘플을 실행 **디버그** -> **디버깅 시작** hello 메뉴. Hello 표시 되 면 **데이터 조각에 대 한 세부 정보 실행**, 몇 분 및 키를 눌러 **ENTER**합니다.
18. 사용 하 여 hello Azure 포털 tooverify hello 데이터 팩터리에서 **APITutorialFactory** hello 다음 아티팩트를 사용 하 여 만들어집니다.
    * 연결된 서비스: **AzureStorageLinkedService**
    * 데이터 집합: **DatasetBlobSource** 및 **DatasetBlobDestination**
    * 파이프라인: **PipelineBlobSample**
19. Hello에 출력 파일이 만들어졌는지 확인 **apifactoryoutput** 폴더 hello에 **adftutorial** 컨테이너입니다.

## <a name="get-a-list-of-failed-data-slices"></a>실패한 데이터 조각 목록 가져오기 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>다음 단계
다음 예제에서는 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는.NET SDK를 사용 하 여 파이프라인 만들기에 대 한 hello를 참조 하십시오. 

- [Blob 저장소 tooSQL 데이터베이스에서에서 파이프라인 toocopy 데이터 만들기](data-factory-copy-activity-tutorial-using-dotnet-api.md)
