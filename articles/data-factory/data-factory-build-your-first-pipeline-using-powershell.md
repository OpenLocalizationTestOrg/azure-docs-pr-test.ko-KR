---
title: "aaaBuild 첫 번째 데이터 팩터리 (PowerShell) | Microsoft Docs"
description: "이 자습서에서는 Azure PowerShell을 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>자습서: Azure PowerShell을 사용하여 첫 번째 Azure Data Factory 빌드
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-build-your-first-pipeline.md)
> * [Azure 포털](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 템플릿](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

이 문서에서는 Azure PowerShell toocreate 첫 번째 Azure 데이터 팩터리를 사용합니다. 다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다.

이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다. 이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다. hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다. 

> [!NOTE]
> 이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다. 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사 하지 않습니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
> 
> 파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
* 자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.
* 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서 tooinstall에 최신 버전의 Azure PowerShell 컴퓨터입니다.
* (선택 사항) 이 문서는 모든 hello 데이터 팩터리 cmdlet을 다루지 않습니다. 데이터 팩터리 cmdlet에 대한 포괄적인 설명서는 [데이터 팩터리 Cmdlet 참조](/powershell/module/azurerm.datafactories) (영문)를 참조하세요.

## <a name="create-data-factory"></a>데이터 팩터리 만들기
이 단계를 사용 하 여 Azure PowerShell toocreate 라는 Azure 데이터 팩터리 **FirstDataFactoryPSH**합니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 입력 데이터입니다. 이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.

1. Azure PowerShell을 시작 하 고 hello 다음 명령을 실행 합니다. 이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다. 닫았다가, 해야 toorun 이러한 명령을 다시.
   * Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * 이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * 다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다. 이 구독은 hello hello Azure 포털에서에서 사용 된 것 처럼 동일한 hello 해야 합니다.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. 라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 명령을 실행 하 여:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    이 자습서의 hello 단계 중 일부 ADFTutorialResourceGroup 라는 hello 리소스 그룹을 사용 하는 것을 가정 합니다. Toouse 필요한 다른 리소스 그룹을 사용 하는 경우이 자습서에서는 ADFTutorialResourceGroup 대신 것입니다.
3. Hello 실행 **새로 AzureRmDataFactory** 라는 데이터 팩터리를 만드는 cmdlet **FirstDataFactoryPSH**합니다.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
포인트 다음 참고 hello:

* Azure Data Factory hello의 hello 이름 전역적으로 고유 해야 합니다. Hello 오류가 나타나면 **"FirstDataFactoryPSH" 데이터 팩터리 이름을 사용할 수 없으면**, hello 이름 (예를 들어 yournameFirstDataFactoryPSH)를 변경 합니다. 이 자습서의 단계를 수행하는 동안 ADFTutorialFactoryPSH 대신 이 이름을 사용합니다. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.
* toocreate 데이터 팩터리 인스턴스 해야 toobe hello Azure 구독 참가자/관리자
* hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.
* Hello 오류가 나타나면: "**이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.

  * Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다. 이 동작은 hello 공급자를 자동으로 등록합니다.

파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다. 연결 된 서비스 toolink 저장소/계산 tooyour 데이터 저장의 입력 정의 및 연결 된 데이터 저장소의 데이터 집합 toorepresent 입/출력 데이터를 출력 하 고 데이터 다음 이러한 데이터 집합을 사용 하는 작업으로 hello 파이프라인을 만들 먼저 만들어야 합니다.

## <a name="create-linked-services"></a>연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 및 주문형 Azure HDInsight 클러스터 tooyour 데이터 팩터리를 연결합니다. 안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정. hello HDInsight 연결 된 서비스에 사용 되는 toorun hello 파이프라인이 샘플에서의 hello 활동에 지정 된 Hive 스크립트입니다. 데이터를 식별 합니다. 저장소/계산 서비스 시나리오에 사용 되 고 해당 서비스 toohello 데이터 팩터리에 연결 된 서비스를 만들어 연결 합니다.

### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다. Hello를 사용 하 여 스크립트 파일을 toostore 입/출력 데이터와 hello hql로 변환 하는 동일한 Azure 저장소 계정입니다.

1. 콘텐츠를 수행 하는 hello로 StorageLinkedService.json hello C:\ADFGetStarted 폴더에는 JSON 파일을 만듭니다. 이미 존재 하지 않는 경우 ADFGetStarted hello 폴더를 만듭니다.

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    대체 **계정 이름** hello Azure 저장소 계정 이름으로 및 **계정 키** hello Azure 저장소 계정 액세스 키가 hello 인 합니다. toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.
2. Azure PowerShell에서 toohello ADFGetStarted 폴더를 전환 합니다.
3. Hello를 사용할 수 있습니다 **새로 AzureRmDataFactoryLinkedService** 연결된 된 서비스를 만드는 cmdlet. 이 cmdlet 및 기타 데이터 팩터리 cmdlet이이 자습서에서 사용 하 여 값이 필요 하면 toopass hello에 대 한 *ResourceGroupName* 및 *DataFactoryName* 매개 변수입니다. 사용할 수 있습니다 **Get AzureRmDataFactory** tooget는 **DataFactory** 개체를 입력 하지 않고도 hello 개체를 전달 *ResourceGroupName* 및  *DataFactoryName* cmdlet을 실행할 때마다 합니다. 실행된 hello 다음 명령은 hello의 tooassign hello 출력 **Get AzureRmDataFactory** cmdlet tooa **$df** 변수입니다.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. 이제 hello 실행 **새로 AzureRmDataFactoryLinkedService** hello를 만드는 cmdlet에 연결 된 **StorageLinkedService** 서비스입니다.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Hello를 실행 하지 않은 경우 **Get AzureRmDataFactory** cmdlet 및 할당 된 hello 출력 toohello **$df** 변수에 값이 있는 toospecify hello에 대 한 *ResourceGroupName*및 *DataFactoryName* 다음과 같이 매개 변수입니다.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Toorun hello 있는 hello 자습서의 hello 가운데에 Azure PowerShell을 닫으면 **Get AzureRmDataFactory** cmdlet 다음에 Azure PowerShell toocomplete hello 자습서를 시작 합니다.

### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스 만들기
이 단계에서는 주문형 HDInsight 클러스터 tooyour 데이터 팩터리에 연결합니다. hello HDInsight 클러스터는 자동으로 런타임 시 만들어지고 지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 삭제 합니다. 주문형 HDInsight 클러스터를 사용하는 대신 고유의 HDInsight 클러스터를 사용할 수 있습니다. 자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.

1. 라는 JSON 파일을 만들어 **HDInsightOnDemandLinkedService**hello에.json **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로 합니다.

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

   | 속성 | 설명 |
   |:--- |:--- |
   | ClusterSize |Hello HDInsight 클러스터의 hello 크기를 지정합니다. |
   | TimeToLive |삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다. |
   | linkedServiceName |HDInsight에서 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다. |

    포인트 다음 참고 hello:

   * hello 데이터 팩터리가 **Linux 기반** JSON hello로 있습니다에 대 한 HDInsight 클러스터입니다. 자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.
   * 주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다. 자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.
   * hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**). HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다. hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.

       많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.

     자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.
2. Hello 실행 **새로 AzureRmDataFactoryLinkedService** hello를 만드는 cmdlet에는 연결 된 서비스 HDInsightOnDemandLinkedService를 호출 합니다.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>데이터 집합 만들기
이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다. 이러한 데이터 집합 참조 toohello **StorageLinkedService** 이 자습서의 앞부분에서 만든 합니다. Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.

### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
1. 라는 JSON 파일을 만들어 **InputTable.json** hello에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    라는 데이터 집합을 정의 하는 hello JSON **AzureBlobInput**을 hello 파이프라인의 활동에 대 한 입력된 데이터를 나타냅니다. Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **inputdata**합니다.

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

   | 속성 | 설명 |
   |:--- |:--- |
   | type |hello type 속성 데이터는 Azure blob 저장소에 있기 때문에 tooAzureBlob 설정 됩니다. |
   | linkedServiceName |이전에 만든 StorageLinkedService toohello를 참조 합니다. |
   | fileName |이 속성은 선택 사항입니다. 이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다. 이 경우 hello input.log만 처리 됩니다. |
   | type |hello 로그 파일은 텍스트 형식으로 TextFormat를 사용 하도록 합니다. |
   | columnDelimiter |hello 로그 파일의 열 hello 쉼표 문자 (,)으로 구분 됩니다. |
   | frequency/interval |frequency tooMonth를 설정 하 고 간격은 1 매월 hello 입력된 조각이 사용할 수 있음을 의미 합니다. |
   | external |이 속성 tootrue 경우 입력된 데이터 hello hello 데이터 팩터리 서비스에서 생성 되지 않습니다. |
2. Hello 다음 Azure PowerShell toocreate hello Data Factory 데이터 집합의 명령을 실행 합니다.

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
이제, hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent hello 출력 데이터를 만듭니다.

1. 라는 JSON 파일을 만들어 **OutputTable.json** hello에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    라는 데이터 집합을 정의 하는 hello JSON **AzureBlobOutput**을 hello 파이프라인의 활동에 대 한 출력 데이터를 나타냅니다. Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **partitioneddata**합니다. hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다.
2. Hello 다음 Azure PowerShell toocreate hello Data Factory 데이터 집합의 명령을 실행 합니다.

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **HDInsightHive** 작업을 사용하여 첫 번째 파이프라인을 만듭니다. 입력된 조각이 매월 (빈도: 월, 간격: 1), 출력 조각이 매월, 생성 되 고 hello 활동에 대 한 hello 스케줄러 속성 toomonthly도 설정 됩니다. hello 출력 데이터 집합 및 작업 스케줄러 hello에 대 한 hello 설정을 일치 해야 합니다. 현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다. Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다. 다음 JSON hello에 사용 되는 hello 속성 hello 끝이 섹션에 설명 되어 있습니다.

1. 콘텐츠 다음 hello로 MyFirstPipelinePSH.json hello C:\ADFGetStarted 폴더에는 JSON 파일을 만듭니다.

   > [!IMPORTANT]
   > 대체 **storageaccountname** hello hello JSON에서에서 저장소 계정의 이름으로 합니다.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    Hello JSON 조각에는 HDInsight 클러스터에서 하이브 tooprocess 데이터를 사용 하는 단일 활동으로 구성 된 파이프라인을 만들게 됩니다.

    hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **StorageLinkedService**), 및 **스크립트**  hello 컨테이너에 폴더 **adfgetstarted**합니다.

    hello **정의** 섹션은 수 있는 사용 되는 toospecify hello 런타임 설정을 toohello 하이브 스크립트 하이브 구성 값으로 전달 (예: ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

    hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다.

    Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.

   > [!NOTE]
   > "파이프라인 JSON"을 참조 [파이프라인 및 활동 Azure Data Factory에](data-factory-create-pipelines.md) hello 예제에 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 합니다.

2. Hello 표시 되는지 확인 **input.log** hello에 대 한 파일 **adfgetstarted/inputdata** hello Azure blob 저장소 및 실행된 hello 명령 toodeploy hello 파이프라인 뒤의 폴더입니다. Hello 이후 **시작** 및 **끝** 시간이 지난 hello에 설정 된 및 **isPaused** 배포한 후에 즉시 집합 toofalse, hello 파이프라인 (hello 파이프라인의 활동)을 실행 됩니다.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. 축하합니다. Azure PowerShell을 사용하여 첫 번째 파이프라인 만들기를 완료하였습니다.

## <a name="monitor-pipeline"></a>파이프라인 모니터링
이 단계를 진행 되는 상황에서 Azure 데이터 팩터리에 Azure PowerShell toomonitor 사용 합니다.

1. 실행 **Get AzureRmDataFactory** hello 출력 tooa 할당 **$df** 변수입니다.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. 실행 **Get AzureRmDataFactorySlice** hello의 모든 분할 영역에 대 한 세부 정보 tooget **EmpSQLTable**, hello 파이프라인의 hello 출력 테이블 변수인 합니다.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    해당 hello StartDateTime 여기에서 지정 하는 hello 동일한 시작 hello 파이프라인 JSON에 지정 된 시간을 확인 합니다. 다음은 hello 샘플 출력이입니다.

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. 실행 **Get AzureRmDataFactoryRun** tooget hello 활동 세부 정보를 특정 조각에 대 한 실행 합니다.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    다음은 hello 샘플 출력이입니다. 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    있습니다 수 계속이 cmdlet을 실행 hello 분할 영역에 표시 될 때까지 **준비** 상태 또는 **실패** 상태입니다. Hello 조각 준비 상태에 있으면 확인 hello **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.  주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.

    ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> 주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분) 따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.
>
> 입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다. 따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.
>
>

## <a name="summary"></a>요약
이 자습서에서는 Azure 데이터 팩터리 tooprocess 데이터 HDInsight hadoop 클러스터에서 하이브 스크립트를 실행 하 여 만들었습니다. 데이터 팩터리 편집기 단계를 수행 하는 hello Azure 포털 toodo hello에 hello을 사용 하는 경우:

1. Azure **데이터 팩터리**를 만들었습니다.
2. 두 개의 **연결된 서비스**를 만들었습니다.
   1. **Azure 저장소** 서비스 toolink 입/출력 파일 toohello 데이터 팩터리를 포함 하 여 Azure blob 저장소를 연결 합니다.
   2. **Azure HDInsight** 주문형 연결 된 서비스 toolink 주문형 HDInsight Hadoop 클러스터 toohello 데이터 팩터리입니다. Azure 데이터 팩터리를 만들고 HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 생성 출력 데이터 합니다.
3. 두 개의 만든 **데이터 집합**는 hello 파이프라인에서 HDInsight Hive 활동에 대 한 입력 및 출력 데이터에 설명 합니다.
4. **HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서 파이프라인과 주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다. toouse Azure Blob tooAzure SQL에서 복사 작업 toocopy 데이터를 확인 하려면 어떻게 toosee [자습서: Azure Blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.

## <a name="see-also"></a>참고 항목
| 항목 | 설명 |
|:--- |:--- |
| [데이터 팩터리 cmdlet 참조](/powershell/module/azurerm.datafactories) |데이터 팩터리 cmdlet에서 포괄적인 설명서를 참조하세요. |
| [파이프라인](data-factory-create-pipelines.md) |이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다. |
| [데이터 집합](data-factory-create-datasets.md) |이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다. |
| [예약 및 실행](data-factory-scheduling-and-execution.md) |이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다. |
| [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) |이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다. |
