---
title: "자습서: Azure PowerShell을 사용 하 여 파이프라인 toomove 데이터 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure PowerShell을 사용하여 복사 작업을 사용하는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>자습서: Azure PowerShell을 사용하여 데이터를 이동하는 Data Factory 파이프라인 만들기
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

이 문서에서는 설명 어떻게 toouse PowerShell toocreate 데이터 팩터리 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인을 사용 합니다. 새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.   

이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다. hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다. 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.

파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.

> [!NOTE]
> 이 문서는 모든 hello 데이터 팩터리 cmdlet을 다루지 않습니다. 이러한 cmdlet에 대한 포괄적인 설명서는 [Data Factory Cmdlet 참조](/powershell/module/azurerm.datafactories)를 참조하세요.
> 
> 이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.

## <a name="prerequisites"></a>필수 조건
- Hello에 나온 필수 조건을 완료 [자습서 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 문서.
- **Azure PowerShell**을 설치합니다. Hello 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](../powershell-install-configure.md)합니다.

## <a name="steps"></a>단계
이 자습서의 일환으로 수행 하는 hello 단계는 다음과 같습니다.

1. Azure **데이터 팩터리**를 만듭니다. 이 단계에서는 ADFTutorialDataFactoryPSH라는 Azure Data Factory를 만듭니다. 
2. 만들 **연결 된 서비스** hello data factory에 있습니다. 이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다. 
    
    AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

    AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.   
3. 입력 및 출력 만들기 **데이터 집합** hello data factory에 있습니다.  
    
    hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

    마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 출력 SQL 테이블의 데이터 집합 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.
4. 만들기는 **파이프라인** hello data factory에 있습니다. 이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.   
    
    hello 복사 활동 hello Azure blob 저장소 tooa hello Azure SQL 데이터베이스의 테이블에 blob에서 데이터를 복사합니다. 모든 지원 되는 원본 tooany 지원 대상에서 파이프라인 toocopy 데이터에서 복사 작업을 사용할 수 있습니다. 지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요. 
5. 모니터 hello 파이프라인입니다. 이 단계에서는 있습니다 **모니터** PowerShell을 사용 하 여 입력 및 출력 데이터 집합의 조각을 hello 합니다.

## <a name="create-a-data-factory"></a>데이터 팩터리를 만듭니다.
> [!IMPORTANT]
> 전체 [hello 자습서에 대 한 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 아직 수행 하지 않은 경우.   

데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다. 이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.

1. **PowerShell**을 시작합니다. 이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다. 닫고 다시 열 경우 toorun hello 명령을 다시 필요 합니다.

    Hello 다음, 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.

    ```PowerShell
    Get-AzureRmSubscription
    ```

    다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다. 대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. 라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 명령을 실행 하 여:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    이라는 hello 리소스 그룹을 사용 하는 것으로 가정이 자습서의 hello 단계 중 일부 **ADFTutorialResourceGroup**합니다. Toouse 필요한 다른 리소스 그룹을 사용 하는 경우이 자습서에서는 ADFTutorialResourceGroup 대신 것입니다.
3. Hello 실행 **새로 AzureRmDataFactory** 라는 데이터 팩터리 cmdlet toocreate **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    이 이름은 이미 사용되었을 수도 있습니다. 따라서 고유 하 게 만드는 hello 데이터 팩터리의 hello 이름 접두사 또는 접미사를 추가 하 여 (예: ADFTutorialDataFactoryPSH05152017) hello 명령을 다시 실행 합니다.  

포인트 다음 참고 hello:

* hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다. Hello 다음 오류가 표시 되 면 hello 이름 (예를 들어 yournameADFTutorialDataFactoryPSH)을 변경 합니다. 이 자습서의 단계를 수행하는 동안 ADFTutorialFactoryPSH 대신 이 이름을 사용합니다. Data Factory 아티팩트에 대한 내용은 [Data Factory - 명명 규칙](data-factory-naming-rules.md)을 참조하세요.

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* toocreate 데이터 팩터리 인스턴스 hello Azure 구독 관리자 또는 참가자 여야 합니다.
* hello hello 데이터 팩터리의 이름입니다 hello 미래에 DNS 이름으로 등록 하 고 있으므로 공개 될 수 있습니다.
* Hello 다음 오류가 나타날 수 있습니다: "**이 구독 microsoft.datafactory가 등록 된 toouse 네임 스페이스가 아닙니다.**" Hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.

  * Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    데이터 팩터리 공급자가 등록 되어 해당 hello hello 명령 tooconfirm 다음을 실행 합니다.

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * 로그인에 사용 하 여 Azure 구독 toohello hello [Azure 포털](https://portal.azure.com)합니다. Tooa Data Factory 블레이드로 이동 하거나 hello Azure 포털에서에서 데이터 팩터리를 만듭니다. 이 동작은 hello 공급자를 자동으로 등록합니다.

## <a name="create-linked-services"></a>연결된 서비스 만들기
데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다. 이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다. Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다. 

이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.  

AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. 이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다. 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Azure 저장소 계정에 대한 연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.

1. 라는 JSON 파일을 만들어 **AzureStorageLinkedService.json** 에 **C:\ADFGetStartedPSH** 폴더 콘텐츠를 다음 hello로: (hello 폴더 만들기 ADFGetStartedPSH 아직 없는 경우.)

    > [!IMPORTANT]
    > 대체 &lt;accountname&gt; 및 &lt;accountkey&gt; 이름과 hello 파일 저장 하기 전에 Azure 저장소 계정의 키입니다. 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. **Azure PowerShell**, toohello 전환 **ADFGetStartedPSH** 폴더입니다.
4. Hello 실행 **새로 AzureRmDataFactoryLinkedService** 연결 된 서비스 cmdlet toocreate hello: **AzureStorageLinkedService**합니다. 이 cmdlet 및 기타 데이터 팩터리 cmdlet이이 자습서에서 사용 하 여 값이 필요 하면 toopass hello에 대 한 **ResourceGroupName** 및 **DataFactoryName** 매개 변수입니다. 또는 리소스 그룹 이름 및 DataFactoryName cmdlet을 실행할 때마다 입력 하지 않고도 hello 새로 AzureRmDataFactory cmdlet에서 반환 하는 hello DataFactory 개체를 전달할 수 있습니다. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    다음은 hello 샘플 출력이입니다.

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    이 연결 된 서비스를 만드는 다른 방법은 toospecify 리소스 그룹 이름 및 hello DataFactory 개체를 지정 하는 대신 데이터 팩터리의 이름입니다.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Azure SQL Database에 대한 연결된 서비스 만들기
이 단계에서는 Azure SQL 데이터베이스 tooyour 데이터 팩터리를 연결할 수 있습니다.

1. 콘텐츠 다음 hello로 AzureSqlLinkedService.json C:\ADFGetStartedPSH 폴더에는 JSON 파일을 만듭니다.

    > [!IMPORTANT]
    > &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; 및 &lt;password&gt;를 Azure SQL Server의 이름, 데이터베이스, 사용자 계정 및 암호로 바꿉니다.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. 다음 명령은 toocreate hello 연결 된 서비스를 실행 합니다.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    다음은 hello 샘플 출력이입니다.

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   확인 **tooAzure 서비스 액세스를 허용** SQL 데이터베이스 서버에 대 한 설정이 켜져 있습니다. tooverify 및 켜십시오, 다음 단계 hello지 않습니다.

    1. Toohello 로그인 [Azure 포털](https://portal.azure.com)
    2. 클릭 **더 많은 서비스 >** 를 클릭 한 hello 왼쪽 **SQL server** hello에 **데이터베이스** 범주입니다.
    3. SQL server hello 목록에서 서버를 선택 합니다.
    4. Hello SQL server 블레이드 클릭 **방화벽 설정 표시** 링크 합니다.
    5. Hello에 **방화벽 설정** 블레이드에서 클릭 **ON** 에 대 한 **tooAzure 서비스 액세스를 허용**합니다.
    6. 클릭 **저장** hello 도구 모음입니다. 

## <a name="create-datasets"></a>데이터 집합 만들기
Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다. 이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.

hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다. 

### <a name="create-an-input-dataset"></a>입력 데이터 집합 만들기
이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다. 하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다. 이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.  

1. 라는 JSON 파일을 만들어 **InputDataset.json** hello에 **C:\ADFGetStartedPSH** 폴더에 콘텐츠를 다음 hello:

    ```json
    {
        "name": "InputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

    | 속성 | 설명 |
    |:--- |:--- |
    | type | hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다. |
    | linkedServiceName | Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다. |
    | folderPath | Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다. 이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다. | 
    | fileName | 이 속성은 선택 사항입니다. 이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다. 이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다. |
    | format -> type |사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다. |
    | columnDelimiter | hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다. |
    | frequency/interval | hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다. 즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다. Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.  |
    | external | 이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다. 이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다. |

    이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.
2. Hello 명령 toocreate hello Data Factory 데이터 집합을 따라를 실행 합니다.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    다음은 hello 샘플 출력이입니다.

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>출력 데이터 집합 만들기
명명 된 출력 데이터 집합을 만들면이 부분 hello 단계 **OutputDataset**합니다. 이 데이터 집합으로 표시 하는 hello Azure SQL 데이터베이스의 tooa SQL 테이블 점은 **AzureSqlLinkedService**합니다. 

1. 라는 JSON 파일을 만들어 **OutputDataset.json** hello에 **C:\ADFGetStartedPSH** 폴더 콘텐츠를 다음 hello로:

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

    | 속성 | 설명 |
    |:--- |:--- |
    | type | hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다. |
    | linkedServiceName | Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다. |
    | tableName | 지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다. | 
    | frequency/interval | hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.  |

    세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다. Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.

    이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.
2. Hello toocreate hello data factory 데이터 명령 집합을 따라를 실행 합니다.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    다음은 hello 샘플 출력이입니다.

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>파이프라인을 만듭니다.
이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.

현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다. 이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다. hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다. 따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다. 


1. 라는 JSON 파일을 만들어 **ADFTutorialPipeline.json** hello에 **C:\ADFGetStartedPSH** 폴더에 콘텐츠를 다음 hello:

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    포인트 다음 참고 hello:
   
    - Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다. Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.
    - Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다. 
    - Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다. 원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.  
     
    Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다. Hello 날짜 부분만 지정 하 고 날짜 시간 hello의 hello 시간 부분을 건너뛸 수 있습니다. 예를 들어 "2016-02-03", 즉 너무 "2016-02-03T00:00:00Z"
     
    start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예를 들어 2016-10-14T16:32:41Z입니다. hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다. 
     
    Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다. toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.
     
    앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.

    파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요. 복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요. BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요. SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.
2. Hello 명령 toocreate hello 데이터 팩터리 테이블을 다음을 실행 합니다.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    다음은 hello 샘플 출력이입니다. 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**축하합니다.** Azure blob 저장소 tooan Azure SQL 데이터베이스의 파이프라인 toocopy 데이터로 Azure 데이터 팩터리에 성공적으로 만들었습니다. 

## <a name="monitor-hello-pipeline"></a>모니터 hello 파이프라인
이 단계를 진행 되는 상황에서 Azure 데이터 팩터리에 Azure PowerShell toomonitor 사용 합니다.

1. 대체 &lt;DataFactoryName&gt; data factory와 실행의 hello 이름의 **Get AzureRmDataFactory**, hello 출력 tooa 변수 $df 할당 합니다.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    예:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    다음 출력 $df toosee hello의 인쇄 hello 내용을 실행 합니다. 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. 실행 **Get AzureRmDataFactorySlice** hello의 모든 분할 영역에 대 한 세부 정보 tooget **OutputDataset**, hello 파이프라인의 hello 출력 데이터 집합은입니다.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   이 설정은 hello 일치 해야 **시작** hello 파이프라인 JSON의 값입니다. 24 조각 표시 되어야 다음 날의 hello AM hello 현재 날짜 too12의 오전 12 시에서 각 시간에 대 한 합니다.

   다음은 hello 출력에서 3 개의 샘플 슬라이스입니다. 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. 실행 **Get AzureRmDataFactoryRun** tooget hello 활동 세부 정보에 대해 실행 되는 **특정** 조각입니다. Hello 이전 명령 toospecify hello hello StartDateTime 매개 변수 값의 hello 출력에서 hello 날짜 및 시간 값을 복사 합니다. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   다음은 hello 샘플 출력이입니다. 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Data Factory cmdlet에 대한 포괄적인 설명서는 [Data Factory cmdlet 참조](/powershell/module/azurerm.datafactories)를 참조하세요.

## <a name="summary"></a>요약
이 자습서에서는 Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 만들었습니다. PowerShell toocreate hello 데이터 팩터리, 연결 된 서비스, 데이터 집합 및 파이프라인을 사용 했습니다. 이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.  

1. Azure **데이터 팩터리**를 만들었습니다.
2. **연결된 서비스**를 만들었습니다.

   a. **Azure 저장소** 서비스 toolink 입력된 데이터를 보유 하는 Azure 저장소 계정을 연결 합니다.     
   b. **Azure SQL** 서비스 toolink hello 출력 데이터를 보유 하는 SQL 데이터베이스를 연결 합니다.
3. 파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합** 을 만들었습니다.
4. 만든는 **파이프라인** 와 **복사 작업**와 **BlobSource** hello 소스로 및 **SqlSink** hello 싱크로 합니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다. hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다. 

