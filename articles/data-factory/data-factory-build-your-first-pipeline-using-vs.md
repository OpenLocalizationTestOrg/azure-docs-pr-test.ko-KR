---
title: "aaaBuild 첫 번째 데이터 팩터리 (Visual Studio) | Microsoft Docs"
description: "이 자습서에서는 Visual Studio를 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>자습서: Visual Studio를 사용하여 데이터 팩터리 만들기
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [개요 및 필수 구성 요소](data-factory-build-your-first-pipeline.md)
> * [Azure 포털](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 템플릿](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

이 자습서에서는 Visual Studio를 사용 하 여 Azure 데이터 팩터리에 toocreate 합니다. Hello Data Factory 프로젝트 템플릿을 사용 하 여 Visual Studio 프로젝트 Data Factory 엔터티 (연결 된 서비스, 데이터 집합 및 파이프라인) 정의 하는 JSON 형식으로 만들고 게시/이러한 엔터티 toohello 클라우드 배포. 

이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다. 이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다. hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다. 

> [!NOTE]
> 이 자습서에서는 Azure Data Factory를 사용하여 데이터를 복사하는 방법을 표시하지 않습니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
> 
> 파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>연습: 데이터 팩터리 엔터티 만들기 및 게시
다음은이 연습의 일부분으로 수행 하는 hello 단계입니다.

1. 2개의 연결된 서비스인 **AzureStorageLinkedService1** 및 **HDInsightOnDemandLinkedService1**을 만듭니다. 
   
    이 자습서에서는 입력 및 출력 데이터에 hello hive 작업에 대 한 hello 동일한 Azure Blob 저장소입니다. 주문형 HDInsight 클러스터 tooprocess 기존 입력된 데이터 tooproduce 출력 데이터를 사용 합니다. hello 주문형 HDInsight 클러스터는 자동으로 생성 Azure 데이터 팩터리에서 hello 입력된 데이터의 처리 준비 toobe 경우 런타임 시. Toolink 데이터를 저장 하거나 hello 데이터 팩터리 서비스 런타임에 toothem 연결할 수 있도록 tooyour 데이터 팩터리를 계산 해야 합니다. 따라서 AzureStorageLinkedService1, hello를 사용 하 여 toohello 데이터 팩터리를 Azure 저장소 계정에 연결 하 고 HDInsightOnDemandLinkedService1 hello를 사용 하 여 주문형 HDInsight 클러스터를 연결 합니다. 게시, hello 데이터 팩터리 toobe 생성에 대 한 hello 이름 또는 기존 데이터 팩토리 지정 합니다.  
2. 두 개의 데이터 집합 만들기: **InputDataset** 및 **OutputDataset**, 있으며 hello Azure blob 저장소에에서 저장 된 hello 입/출력 데이터를 나타냅니다. 
   
    이러한 데이터 집합 정의 hello 이전 단계에서 만든 toohello Azure 저장소 연결 된 서비스를 참조 하십시오. InputDataset hello에 대 한 hello blob 컨테이너 (adfgetstarted)를 지정 하 고 hello hello 입력된 데이터와 함께 blob이 포함 된 폴더 (inptutdata). OutputDataset hello에 대 한 hello blob 컨테이너 (adfgetstarted)를 지정 하 고 hello 출력 데이터를 보유 하는 hello 폴더 (partitioneddata). 구조, 가용성 및 정책과 같은 기타 속성도 지정합니다.
3. **MyFirstPipeline**이라는 파이프라인을 만듭니다. 
  
    이 연습에서는 hello 파이프라인에 활동이 하나만: **HDInsight Hive 활동**합니다. 이 활동 변환 하는 주문형 HDInsight 클러스터에서 하이브 스크립트를 실행 하 여 데이터 tooproduce 출력 데이터를 입력 합니다. hive 작업에 대해 자세히 toolearn 참조 [Hive 작업](data-factory-hive-activity.md) 
4. **DataFactoryUsingVS**라는 데이터 팩터리를 만듭니다. Hello data factory와 모든 데이터 팩터리의 엔터티 (연결 된 서비스, 테이블 및 hello 파이프라인)를 배포 합니다.
5. 를 게시 한 후 Azure 포털 블레이드, 모니터링 및 관리 응용 프로그램 toomonitor hello 파이프라인을 사용 합니다. 
  
### <a name="prerequisites"></a>필수 조건
1. 자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다. Hello를 선택할 수도 있습니다 **개요 및 필수 조건** hello 상위 tooswitch toohello 문서 hello 드롭 다운 목록에서 옵션입니다. Hello 필수 구성 요소를 완료 한 후 뒤로 toothis 문서를 선택 하 여 전환 **Visual Studio** hello 드롭 다운 목록에서 옵션입니다.
2. toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.  
3. Hello 다음이 컴퓨터에 설치 되어 있어야 합니다.
   * Visual Studio 2013 또는 Visual Studio 2015
   * Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다. 너무 이동[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/) 클릭 **VS 2013** 또는 **VS 2015** hello에 **.NET** 섹션.
   * Visual Studio에 대 한 hello 최신 Azure Data Factory 플러그 인을 다운로드: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)합니다. Hello 다음 단계를 수행 하 여 hello 플러그 인을 업데이트할 수도 있습니다: hello 메뉴를 클릭 **도구** -> **확장명 및 업데이트** -> **온라인**  ->  **Visual Studio 갤러리** -> **Visual Studio 용 Microsoft Azure 데이터 팩터리 도구** -> **업데이트**합니다.

이제 Visual Studio toocreate Azure 데이터 팩터리를 사용 하 여 보겠습니다.

### <a name="create-visual-studio-project"></a>Visual Studio 프로젝트 만들기
1. **Visual Studio 2013** 또는 **Visual Studio 2015**를 시작합니다. 클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다. Hello 표시 되어야 **새 프로젝트** 대화 상자.  
2. Hello에 **새 프로젝트** 대화 상자에서 선택 hello **DataFactory** 템플릿과 클릭 **빈 데이터 팩터리 프로젝트**합니다.   

    ![새 프로젝트 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. 입력 한 **이름** hello 프로젝트에 대 한 **위치**, 및 hello에 대 한 이름을 **솔루션**를 클릭 하 고 **확인**합니다.

    ![솔루션 탐색기](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>연결된 서비스 만들기
이 단계에서는 두 가지 연결된 서비스 **Azure Storage** 및 **주문형 HDInsight**를 만듭니다. 

hello Azure 저장소 서비스 링크 Azure 저장소 계정 toohello 데이터 팩터리 hello 연결 정보를 제공 하 여 연결 합니다. 데이터 팩터리 서비스 런타임 시 hello 연결 된 서비스 설정 tooconnect toohello Azure 저장소에서에서 연결 문자열 hello를 사용합니다. 이 저장소 입력을 보유 하 고 hello 파이프라인과 hello에 대 한 출력 데이터 하이브 hello hive 활동에서 사용 하는 스크립트 파일 키를 누릅니다. 

HDInsight 클러스터 hello 주문형 HDInsight 연결 된 서비스와 자동 hello 입력된 데이터가 준비 tooprocessed 경우 런타임 시 생성 됩니다. 지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 hello 클러스터가 삭제 됩니다. 

> [!NOTE]
> 데이터 팩터리 솔루션 게시 하는 hello 시 이름 및 설정을 지정 하 여 데이터 팩터리를 만듭니다.

#### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
1. 마우스 오른쪽 단추로 클릭 **연결 된 서비스** hello 솔루션 탐색기에서 가리키고 너무**추가**를 클릭 하 고 **새 항목**합니다.      
2. Hello에 **새 항목 추가** 대화 상자에서 **Azure 저장소 연결 된 서비스** hello 목록 및 클릭에서 **추가**합니다.
    ![Azure Storage 연결 서비스](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. 대체 `<accountname>` 및 `<accountkey>` Azure 저장소 계정 및 키의 hello 이름의 합니다. toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.
    ![Azure Storage 연결 서비스](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Hello 저장 **AzureStorageLinkedService1.json** 파일입니다.

#### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스 만들기
1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **연결 된 서비스**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. **주문형 HDInsight 연결된 서비스**를 선택하고 **추가**를 클릭합니다.
3. Hello 대체 **JSON** 다음 JSON hello로:

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

    속성 | 설명
    -------- | ----------- 
    ClusterSize | Hello HDInsight Hadoop 클러스터의 hello 크기를 지정합니다.
    TimeToLive | 삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다.
    linkedServiceName | HDInsight Hadoop 클러스터에 의해 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다. 

    > [!IMPORTANT]
    > hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON (linkedServiceName)에 지정 된 hello blob 저장소에 있습니다. HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 경우 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다. hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.
    > 
    > 많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`합니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.

    JSON 속성에 대한 자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)을 참조하세요. 
4. Hello 저장 **HDInsightOnDemandLinkedService1.json** 파일입니다.

### <a name="create-datasets"></a>데이터 집합 만들기
이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다. 이러한 데이터 집합 참조 toohello **AzureStorageLinkedService1** 이 자습서의 앞부분에서 만든 합니다. Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.   

#### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **테이블**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. 선택 **Azure Blob** hello 목록에서 hello 파일의 이름을 변경 hello 너무**InputDataSet.json**를 클릭 하 고 **추가**합니다.
3. Hello 대체 **JSON** 다음 JSON 코드 조각은 hello로 hello 편집기에서:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    이 JSON 코드 조각은 라는 데이터 집합 정의 **AzureBlobInput** hello hive 활동 hello 파이프라인에 대 한 입력된 데이터를 나타내는입니다. Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 `adfgetstarted` 및 라고 하는 hello 폴더 `inputdata`합니다.

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

    속성 | 설명 |
    -------- | ----------- |
    type |hello type 속성이 너무 설정 되어**AzureBlob** 데이터가 Azure Blob 저장소에 있기 때문에 있습니다.
    linkedServiceName | 이전에 만든 AzureStorageLinkedService1 toohello를 참조 합니다.
    fileName |이 속성은 선택 사항입니다. 이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다. 이 경우 hello input.log만 처리 됩니다.
    type | hello 로그 파일은 텍스트 형식으로 TextFormat를 사용 하도록 합니다. |
    columnDelimiter | hello 로그 파일의 열 hello 쉼표 문자로 구분 됩니다 (`,`)
    frequency/interval | frequency tooMonth를 설정 하 고 간격은 1 매월 hello 입력된 조각이 사용할 수 있음을 의미 합니다.
    external | 이 속성 tootrue 경우 hello 활동에 대 한 입력된 데이터 hello hello 파이프라인에서 생성 되지 않습니다. 이 속성은 입력 데이터 집합에서만 지정됩니다. Hello hello 첫 번째 활동의 입력된 데이터 집합, 항상이 속성 설정 tootrue 합니다.
4. Hello 저장 **InputDataset.json** 파일입니다.

#### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
이제, hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent 출력 데이터를 만듭니다.

1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **테이블**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. 선택 **Azure Blob** hello 목록에서 hello 파일의 이름을 변경 hello 너무**OutputDataset.json**를 클릭 하 고 **추가**합니다.
3. Hello 대체 **JSON** 다음 JSON hello로 hello 편집기에서:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    라는 데이터 집합을 정의 하는 hello JSON 코드 조각은 **AzureBlobOutput** 나타내는 hello 파이프라인의 hello hive 활동에 의해 생성 되는 데이터를 출력 합니다. 데이터는 hello hive 작업에 의해 생성 되는 hello 출력 라는 hello blob 컨테이너에 배치 됩니다 지정 `adfgetstarted` 및 라고 하는 hello 폴더 `partitioneddata`합니다. 
    
    hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다. hello 출력 데이터 집합 드라이브 hello 일정 hello 파이프라인의입니다. hello 파이프라인의 시작 및 종료 시간 사이의 매월 실행 됩니다. 

    참조 **hello 입력된 데이터 집합을 만들** 섹션 이러한 속성에 대 한 설명입니다. Hello dataset hello 파이프라인에 의해 생성 된 것과 hello 외부 속성에는 출력 데이터 집합 설정 하지 마십시오.
4. Hello 저장 **OutputDataset.json** 파일입니다.

### <a name="create-pipeline"></a>파이프라인 만들기
만든 hello Azure 저장소 연결 된 서비스 및 입력 및 출력 데이터 집합 지금까지 합니다. 이제 **HDInsightHive** 작업이 포함된 파이프라인을 만듭니다. hello **입력** hello hive 활동 너무 설정 되어**AzureBlobInput** 및 **출력** 너무 설정**AzureBlobOutput**합니다. 입력된 데이터 집합의 조각을 매월 (주파수: 월, 간격: 1), hello 출력 조각이 너무 생성 매월 되 고 있습니다. 

1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **파이프라인**, 너무 가리킨**추가**를 클릭 하 고 **새 항목입니다.**
2. 선택 **Hive 변환 파이프라인** hello 목록 및 클릭에서 **추가**합니다.
3. Hello 대체 **JSON** 다음 코드 조각 hello로:

    > [!IMPORTANT]
    > 대체 `<storageaccountname>` hello 저장소 계정 이름을 사용 합니다.

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > 대체 `<storageaccountname>` hello 저장소 계정 이름을 사용 합니다.

    hello JSON 코드 조각은 단일 활동 (Hive 활동)으로 구성 된 파이프라인을 정의 합니다. 이 활동에서 주문형 HDInsight 클러스터 tooproduce 출력 데이터에서 하이브 스크립트 tooprocess 입력된 데이터를 실행합니다. Hello 파이프라인 JSON의 hello 활동 섹션 유형이 너무 설정 hello 배열에 활동이 하나만 참조**HDInsightHive**합니다. 

    에서는 hello 유형 속성을 특정 tooHDInsight Hive 작업을 Azure 저장소 연결 서비스는 hello hive 스크립트 파일, hello 경로 toohello 스크립트 파일 및 매개 변수 toohello 스크립트 파일을 지정 합니다. 

    hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정 (hello scriptLinkedService로 지정 됨), 및 hello에 저장 된 `script` hello 컨테이너에 폴더 `adfgetstarted`합니다.

    hello `defines` 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`합니다.

    hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다. 생성 된 월별, 따라서 (시작 및 종료 날짜에 동일한 hello month 이므로) 조각을 hello 파이프라인에서 생성 된 후에 hello dataset toobe를 구성 했습니다.

    Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.
4. Hello 저장 **HiveActivity1.json** 파일입니다.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>partitionweblogs.hql 및 input.log 종속성으로 추가
1. 마우스 오른쪽 단추로 클릭 **종속성** hello에 **솔루션 탐색기** 창 너무 가리킨**추가**를 클릭 하 고 **기존 항목**합니다.  
2. Toohello 이동 **C:\ADFGettingStarted** 선택 **partitionweblogs.hql**, **input.log** 파일과 클릭 **추가**합니다. Hello에서 필수 구성 요소 중에이 두 파일을 만든 [자습서 개요](data-factory-build-your-first-pipeline.md)합니다.

Hello 다음 단계에서 hello 솔루션을 게시할 때 hello **partitionweblogs.hql** 파일은 업로드 toohello **스크립트** 폴더 hello에 `adfgetstarted` blob 컨테이너입니다.   

### <a name="publishdeploy-data-factory-entities"></a>데이터 팩터리 엔터티 게시/배포
이 단계에서는 hello Data Factory 엔터티에 (연결 된 서비스, 데이터 집합 및 파이프라인) 프로그램 프로젝트 toohello Azure 데이터 팩터리 서비스에에서 게시합니다. 게시의 hello 프로세스에서 데이터 팩토리에 대 한 hello 이름을 지정할 수 있습니다. 

1. Hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.
2. 표시 되 면 **tooyour Microsoft 계정 로그인** 대화 상자에서 Azure 구독이 있는 hello 계정에 대 한 자격 증명을 입력 하 고 클릭 **로그인**합니다.
3. 대화 상자를 수행 하는 hello를 표시 되어야 합니다.

   ![게시 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. Hello에 **구성 데이터 팩터리의** 페이지에서 다음 단계 hello지 않습니다.

    ![게시 - 새 데이터 팩터리 설정](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. **새 데이터 팩터리 만들기** 옵션을 선택합니다.
   2. 고유한 입력 **이름** hello 데이터 팩토리에 대 한 합니다. 예: **DataFactoryUsingVS09152016** hello 이름은 전역적으로 고유 해야 합니다.
   3. Hello hello에 대 한 올바른 구독이 선택 **구독** 필드입니다. 
        > [!IMPORTANT]
        > 모든 구독을 표시 되지 않으면 관리자 또는 hello 구독 공동 관리자 인 계정을 사용 하 여 로그인을 확인 합니다.
   4. 선택 hello **리소스 그룹** hello 데이터 팩터리 toobe 생성에 대 한 합니다.
   5. 선택 hello **지역** hello 데이터 팩토리에 대 한 합니다.
   6. 클릭 **다음** tooswitch toohello **게시 항목** 페이지. (키를 눌러 **탭** hello 이름 필드 tooif hello 부족 toomove **다음** 단추가 비활성화 됩니다.)

    > [!IMPORTANT]
    > Hello 오류가 나타나면 **"DataFactoryUsingVS" 데이터 팩터리 이름을 사용할 수 없으면** 을 게시할 때는 hello 이름 (예를 들어 yournameDataFactoryUsingVS)을 변경 합니다. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.   
1. Hello에 **게시 항목** 페이지에서 엔터티를 선택 하 고 클릭 하 여 데이터 팩터리를 hello 모든 **다음** tooswitch toohello **요약** 페이지.

    ![항목 페이지 게시](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Hello 요약을 검토 하 고 클릭 **다음** toostart hello 배포 프로세스와 보기 hello **배포 상태**합니다.

    ![요약 페이지](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. Hello에 **배포 상태** 페이지 hello 배포 프로세스의 hello 상태 표시 되어야 합니다. Hello 배포를 완료 한 후 마침을 클릭 합니다.

중요 한 사항 toonote:

- Hello 오류가 나타나면: **이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.
    - Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Azure 구독에서 toohello hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다. 이 동작은 hello 공급자를 자동으로 등록합니다.
- hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.
- toobe 관리자 또는 공동 관리자의 hello Azure 구독 필요 toocreate 데이터 팩터리 인스턴스

### <a name="monitor-pipeline"></a>파이프라인 모니터링
이 단계에서는 hello 데이터 팩터리의 다이어그램 보기를 사용 하 여 hello 파이프라인을 모니터링할 수 있습니다. 

#### <a name="monitor-pipeline-using-diagram-view"></a>다이어그램 보기를 사용하여 파이프라인 모니터링
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/), 다음 단계 hello지 않습니다.
   1. **더 많은 서비스**를 클릭하고 **데이터 팩터리**를 클릭합니다.
       
        ![데이터 팩터리 찾아보기](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. 데이터 팩터리의 선택 hello 이름 (예: **DataFactoryUsingVS09152016**) 데이터 팩터리의 hello 목록에서 합니다.
   
       ![데이터 팩터리 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. 데이터 팩토리에 대 한 hello 홈 페이지에서 클릭 **다이어그램**합니다.

    ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. 다이어그램 보기 hello에 hello 파이프라인 및이 자습서에 사용 되는 데이터 집합에 대해 간략하게를 표시 됩니다.

    ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview hello 파이프라인에서 마우스 오른쪽 단추로 클릭 파이프라인 hello에 모든 활동 다이어그램 및 열기 파이프라인을 클릭 합니다.

    ![파이프라인 열기 메뉴](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Hello 파이프라인의 hello HDInsightHive 활동 표시 되는지 확인 합니다.

    ![파이프라인 보기 열기](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate toohello 이전 뷰를 다시 클릭 **Data factory** hello 위쪽 hello 이동 경로 탐색 메뉴에 있습니다.
6. Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobInput**합니다. 해당 hello 조각이에 속하는지 확인 **준비** 상태입니다. 준비 상태가 몇 hello 조각 tooshow 분이 걸릴 수도 있습니다. Hello 오른쪽 컨테이너에 배치 입력된 hello 파일 (input.log) 되었는지 확인 하면 잠시 후에 발생 하지 않습니다, 하는 경우 (`adfgetstarted`) 및 폴더 (`inputdata`). 만들고, 해당 hello **외부** hello 입력된 데이터 집합에 속성이 너무**true**합니다. 

   ![준비 상태인 입력 조각](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. 클릭 **X** tooclose **AzureBlobInput** 블레이드입니다.
8. Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobOutput**합니다. 현재 처리 중인 해당 hello 조각이 표시 됩니다.

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Hello 조각 참조 처리가 완료 되 면 **준비** 상태입니다.

   > [!IMPORTANT]
   > 주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분) 따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.  
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Hello 조각화 된 경우 **준비** 상태, hello 확인 `partitioneddata` 폴더 hello에 `adfgetstarted` hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.  

    ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. 에 대 한 hello 조각 toosee 세부 정보 클릭는 **데이터 조각을** 블레이드입니다.

    ![데이터 조각 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Hello에서 실행할 활동을 클릭 **활동 실행 목록** 안에 (시나리오에서 하이브 활동)을 실행 하는 활동에 대 한 toosee 세부 정보는 **활동 실행 정보** 창. 
  
    ![작업 실행 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Hello 로그 파일에서 실행 된 hello 하이브 쿼리 및 상태 정보를 볼 수 있습니다. 이러한 로그는 문제를 해결하는 데 유용합니다.  

참조 [모니터링 데이터 집합 및 파이프라인](data-factory-monitor-manage-pipelines.md) 어떻게 toouse hello Azure 포털 toomonitor hello 파이프라인 및 데이터 집합에서에서 만든이 자습서에 대 한 지침은 합니다.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>앱 모니터링 및 관리를 사용하여 파이프라인 모니터링
모니터를 사용 하 여 & toomonitor 응용 프로그램 파이프라인을 관리할 수도 있습니다. 이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.

1. 타일 모니터링 및 관리를 클릭합니다.

    ![타일 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. 응용 프로그램 모니터링 및 관리가 표시되어야 합니다. 변경 hello **시작 시간** 및 **종료 시간** toomatch 시작 (04-01-2016 오전 12시) 시간 및 종료 시간 (2016-04-02 오전 12시) 파이프라인 및 클릭의 **적용**합니다.

    ![앱 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. 활동 창에 대 한 세부 정보 toosee hello에서 선택 **활동 창 목록** toosee 세부 정보가 있습니다.
    ![활동 창 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> 입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다. 따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello 업로드 hello 입력된 파일 (input.log) toohello `inputdata` hello의 폴더 `adfgetstarted` 컨테이너입니다.

### <a name="additional-notes"></a>추가적인 참고 사항
- 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 입력 데이터입니다. 참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원본 및 싱크 hello 복사 작업에서 지 원하는 모든 hello에 대 한 합니다. 참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) hello 목록이 Data Factory에서 지 원하는 계산 서비스에 대 한 합니다.
- 연결 된 서비스 데이터 저장소를 연결 하거나 서비스 tooan Azure 데이터 팩터리를 계산 합니다. 참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원본 및 싱크 hello 복사 작업에서 지 원하는 모든 hello에 대 한 합니다. 참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) hello 목록이 Data Factory에서 지 원하는 계산 서비스에 대 한 및 [변환 활동](data-factory-data-transformation-activities.md) 하에서 실행할 수 있습니다.
- 참조 [에서 데이터 이동 tooAzure /](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello에 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 Azure 저장소 연결 서비스 정의 합니다.
- 주문형 HDInsight 클러스터를 사용하는 대신 고유의 HDInsight 클러스터를 사용할 수 있습니다. 자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.
-  hello 데이터 팩터리가 **Linux 기반** hello JSON 앞에 있는 수에 대 한 HDInsight 클러스터입니다. 자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.
- hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON (linkedServiceName)에 지정 된 hello blob 저장소에 있습니다. HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 경우 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다. hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.
    
    많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`합니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.
- 현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다. Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다. 
- 이 자습서에서는 Azure Data Factory를 사용하여 데이터를 복사하는 방법을 표시하지 않습니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.


## <a name="use-server-explorer-tooview-data-factories"></a>서버 탐색기 tooview 데이터 팩터리를 사용 하 여
1. **Visual Studio**, 클릭 **보기** 메뉴 hello 되 고 클릭 **서버 탐색기**합니다.
2. Hello 서버 탐색기 창에서 확장 **Azure** 확장 **Data Factory**합니다. 표시 되 면 **tooVisual Studio에에서 로그인**, hello 입력 **계정** 연결 된 Azure 구독 및 클릭 **계속**합니다. **암호**를 입력하고 **로그인**을 클릭합니다. Visual Studio에는 구독에서 모든 Azure 데이터 팩토리에 대 한 정보 tooget 하려고 시도합니다. Hello에이 작업의 hello 상태를 확인할 **데이터 팩터리에 작업 목록** 창.

    ![서버 탐색기](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. 데이터 팩터리를 마우스 오른쪽 단추로 클릭 하 고 선택할 수 **데이터 팩터리의 내보내기 tooNew 프로젝트** toocreate 기존 데이터 팩토리를 기반으로 한 Visual Studio 프로젝트입니다.

    ![데이터 팩터리 내보내기](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Visual Studio용 데이터 팩터리 도구 업데이트
Visual Studio 용 Azure Data Factory 도구 tooupdate 단계 hello지 않습니다.

1. 클릭 **도구** hello 메뉴를 선택 **확장명 및 업데이트**합니다.
2. 선택 **업데이트** 에 왼쪽된 창의 hello 선택한 후 **Visual Studio 갤러리**합니다.
3. **Visual Studio용 Azure Data Factory 도구**를 선택하고 **업데이트**를 클릭합니다. 이 항목을 표시 되지 않으면 최신 버전의 hello 도구 hello이 이미 있습니다.

## <a name="use-configuration-files"></a>구성 파일 사용
연결 된 서비스/테이블/파이프라인 각 환경에 대해 다른 방식에 대 한 Visual Studio tooconfigure 속성에서 구성 파일을 사용할 수 있습니다.

다음은 Azure 저장소 연결 서비스에 대 한 JSON 정의 hello를 것이 좋습니다. toospecify **connectionString** accountname 및 accountkey hello (프로덕션/개발/테스트) 환경 toowhich 기준에 대 한 값이 서로 다른 배포 하는 데이터 팩터리 엔터티. 각 환경에 대한 별도의 구성 파일을 사용하여 이 동작을 수행할 수 있습니다.

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

### <a name="add-a-configuration-file"></a>구성 파일 추가
Hello 다음 단계를 수행 하 여 각 환경에 대 한 구성 파일을 추가 합니다.   

1. Visual Studio 솔루션의 hello Data Factory 프로젝트를 마우스 오른쪽 단추로 클릭, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. 선택 **Config** hello hello 왼쪽에 설치 된 템플릿 목록에서 선택 **구성 파일**를 입력 한 **이름** hello 구성에 대 한 파일을 찾아 클릭 **추가**합니다.

    ![구성 파일 추가](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. 형식에 따라 hello에 구성 매개 변수 및 해당 값을 추가 합니다.

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    이 예제에서는 Azure 저장소 연결된 서비스 및 Azure SQL 연결된 서비스의 connectionString 속성을 구성합니다. Hello 구문 이름을 지정 하는 [JsonPath](http://goessner.net/articles/JsonPath/)합니다.   

    JSON에 hello 코드 다음에 나와 있는 값의 배열을 포함 하는 속성:  

    ```json
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
    ```

    다음 구성 파일 (사용 하 여 인덱스가 0부터 시작) hello에 표시 된 대로 속성을 구성 합니다.

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>공백이 포함된 속성 이름
속성 이름에 공백이 있으면, 다음 예제 (데이터베이스 서버 이름) hello와 같이 대괄호를 사용 합니다.

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>구성을 사용하여 솔루션 배포
Azure Data Factory 엔터티에 VS에서 게시 하는 hello 원하는 구성으로 toouse 해당 게시 작업에 대해 지정할 수 있습니다.

구성 파일을 사용 하 여 Azure Data Factory 프로젝트에서 toopublish 엔터티:   

1. 데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시** toosee hello **게시 항목** 대화 상자.
2. 기존 데이터 팩토리를 선택 하거나 hello에 데이터 팩터리 만들기에 대 한 값을 지정할 **구성 데이터 팩터리의** 페이지를 클릭 하 여 **다음**합니다.   
3. Hello에 **게시 항목** 페이지: hello에 대 한 사용 가능한 구성으로 드롭 다운 목록을 보려면 **배포 구성 선택** 필드입니다.

    ![구성 파일 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. 선택 hello **구성 파일** 있는지 toouse 선택한 클릭 **다음**합니다.
5. Hello에 대 한 JSON 파일의 hello 이름 표시 되는지 확인 **요약** 페이지 클릭 하 여 **다음**합니다.
6. 클릭 **마침** hello 배포 작업이 완료 된 후입니다.

를 배포할 때 hello 구성 파일에서 hello 값은 hello 엔터티는 배포 된 tooAzure 데이터 팩터리 서비스 전에 hello JSON 파일의 속성에 대 한 tooset 사용 되는 값입니다.   

## <a name="use-azure-key-vault"></a>Azure Key Vault 사용
권장 및 종종 연결 문자열 toohello 코드 저장소와 같은 보안 정책 toocommit 중요 한 데이터에 대 한 아닙니다. 참조 [ADF 게시 Secure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure 키 자격 증명 모음에 중요 한 정보를 저장 하 고 사용 하 여 데이터 팩터리 엔터티를 게시 하는 동안에 대 한 GitHub toolearn 샘플. Visual Studio 용 확장명 게시 Secure hello hello 비밀 toobe 주요 자격 증명 모음에 저장 된 있으며 참조 toothem만 연결 된 서비스에 지정 된 / 배포 구성. Data Factory 엔터티에 tooAzure를 게시 하는 경우 이러한 참조는 확인 됩니다. 이러한 파일 비밀이 노출 하지 않고 커밋된 toosource 리포지토리 수 있습니다.

## <a name="summary"></a>요약
이 자습서에서는 Azure 데이터 팩터리 tooprocess 데이터 HDInsight hadoop 클러스터에서 하이브 스크립트를 실행 하 여 만들었습니다. 데이터 팩터리 편집기 단계를 수행 하는 hello Azure 포털 toodo hello에 hello을 사용 하는 경우:  

1. Azure **데이터 팩터리**를 만들었습니다.
2. 두 개의 **연결된 서비스**를 만들었습니다.
   1. **Azure 저장소** 서비스 toolink 입/출력 파일 toohello 데이터 팩터리를 포함 하 여 Azure blob 저장소를 연결 합니다.
   2. **Azure HDInsight** 주문형 연결 된 서비스 toolink 주문형 HDInsight Hadoop 클러스터 toohello 데이터 팩터리입니다. Azure 데이터 팩터리를 만들고 HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 생성 출력 데이터 합니다.
3. 두 개의 만든 **데이터 집합**는 hello 파이프라인에서 HDInsight Hive 활동에 대 한 입력 및 출력 데이터에 설명 합니다.
4. **HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.  

## <a name="next-steps"></a>다음 단계
이 문서에서 파이프라인과 주문형 HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다. toouse Azure Blob tooAzure SQL에서 복사 작업 toocopy 데이터를 확인 하려면 어떻게 toosee [자습서: Azure blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.

Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요. 


## <a name="see-also"></a>참고 항목
| 항목 | 설명 |
|:--- |:--- |
| [파이프라인](data-factory-create-pipelines.md) |이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse tooconstruct 시나리오 또는 비즈니스에 대 한 워크플로 데이터 기반으로 합니다. |
| [데이터 집합](data-factory-create-datasets.md) |이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다. |
| [데이터 변환 활동](data-factory-data-transformation-activities.md) |이 문서에서는 Azure Data Factory에서 지원되는 데이터 변환 활동(예: 이 자습서에 사용된 HDInsight Hive 변환)의 목록을 제공합니다. |
| [예약 및 실행](data-factory-scheduling-and-execution.md) |이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다. |
| [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) |이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다. |
