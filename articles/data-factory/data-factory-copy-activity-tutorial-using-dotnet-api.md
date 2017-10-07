---
title: "자습서: .NET API를 사용하여 복사 작업이 있는 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 .NET API를 사용하여 복사 작업이 있는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>자습서: .NET API를 사용하여 복사 작업이 있는 파이프라인 만들기
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

이 문서에서는 설명 어떻게 toouse [.NET API](https://portal.azure.com) toocreate 데이터 팩터리 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인을 사용 합니다. 새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.   

이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다. hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다. 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.

파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요. 

> [!NOTE] 
> Data Factory용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.
> 
> 이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.

## <a name="prerequisites"></a>필수 조건
* 통해 이동 [자습서 개요 및 필수](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget hello 자습서 및 전체 hello 개요 **필수 구성 요소** 단계입니다.
* Visual Studio 2012, 2013 또는 2015
* [Azure .NET SDK](http://azure.microsoft.com/downloads/)
* Azure PowerShell. 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](../powershell-install-configure.md) 컴퓨터에 Azure PowerShell tooinstall 문서입니다. Azure PowerShell toocreate Azure Active Directory 응용 프로그램을 사용 합니다.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
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
4. Hello 다음 추가 **appSetttings** 섹션 toohello **App.config** 파일입니다. 이러한 설정은 hello 도우미 메서드에서 사용 됩니다: **GetAuthorizationHeader**합니다.

    **&lt;응용 프로그램 ID&gt;**, **&lt;암호&gt;**, **&lt;구독 ID&gt;** 및 **&lt;테넌트 ID&gt;**의 값을 고유한 값으로 바꿉니다.

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

5. Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일 (Program.cs).

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
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Hello 값의 대체 **resourceGroupName** hello Azure 리소스 그룹 이름으로 합니다.
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

    데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다. 이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.
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

    데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다. 이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다. Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다. 

    이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.  

    AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
9. 추가 코드를 만드는 다음 hello는 **Azure SQL 연결 된 서비스** toohello **Main** 메서드.

   > [!IMPORTANT]
   > **servername**, **databasename**, **username** 및 **password**를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. 이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
10. 추가 코드를 만드는 다음 hello **입력 및 출력 데이터 집합** toohello **Main** 메서드.

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다. 이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.

    hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

    마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다.

    이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다. 하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다. 이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.    

    이 단계에서는 **OutputDataset**이라는 출력 데이터 집합을 만듭니다. 이 데이터 집합으로 표시 하는 hello Azure SQL 데이터베이스의 tooa SQL 테이블 점은 **AzureSqlLinkedService**합니다.
11. Hello 다음 코드를 추가 **가 만들어지고 활성화 파이프라인** toohello **Main** 메서드. 이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    포인트 다음 참고 hello:
   
    - Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다. Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.
    - Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다. 
    - Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다. 원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.  
   
    현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다. 이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다. hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다. 따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다.
12. 다음 코드 toohello hello 추가 **Main** hello의 데이터 조각 방법 tooget hello 상태 출력 데이터 집합입니다. 이 샘플에서는 조각만 필요합니다.

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

13. 다음 코드 tooget 실행 세부 정보에 대 한 데이터 조각 toohello hello 추가 **Main** 메서드.

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
            }
        );

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

14. Hello hello에서 사용 하는 도우미 메서드를 다음 추가 **Main** 메서드 toohello **프로그램** 클래스입니다.

    > [!NOTE] 
    > 복사한 코드 다음 hello 붙여 넣는 경우 해야 해당 hello 복사한 코드는 동일한 수준으로 hello Main 메서드에 hello에서 합니다.

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

15. 솔루션 탐색기 hello, hello 프로젝트 (DataFactoryAPITestApp) 확장 하 고, 마우스 오른쪽 단추로 클릭 **참조**를 클릭 하 고 **참조 추가**합니다. **System.Configuration** 어셈블리에 대한 확인란을 선택하고 **확인**을 클릭합니다.
16. Hello 콘솔 응용 프로그램을 빌드하십시오. 클릭 **빌드** hello 메뉴에 **솔루션 빌드**합니다.
17. Hello에 파일을 하나 이상 있는지 확인 **adftutorial** Azure blob 저장소의 컨테이너입니다. 그렇지 않은 경우 만들 **Emp.txt** 콘텐츠를 다음 hello로 메모장에서 파일을 toohello adftutorial 컨테이너를 업로드 합니다.

    ```
    John, Doe
    Jane, Doe
    ```
18. 클릭 하 여 hello 샘플을 실행 **디버그** -> **디버깅 시작** hello 메뉴. Hello 표시 되 면 **데이터 조각에 대 한 세부 정보 실행**, 몇 분 및 키를 눌러 **ENTER**합니다.
19. 사용 하 여 hello Azure 포털 tooverify hello 데이터 팩터리에서 **APITutorialFactory** hello 다음 아티팩트를 사용 하 여 만들어집니다.
   * 연결된 서비스: **LinkedService_AzureStorage**
   * 데이터 집합: **InputDataset** 및 **OutputDataset**.
   * 파이프라인: **PipelineBlobSample**
20. Hello에 hello 두 직원 레코드가 만들어졌는지 확인 **emp** hello 표에 Azure SQL 데이터베이스를 지정 합니다.

## <a name="next-steps"></a>다음 단계
Data Factory용 .NET API에 대한 포괄적인 설명서는 [데이터 팩터리 .NET API 참조](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)를 참조하세요.

이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다. hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.

