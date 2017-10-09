---
title: "Azure Data Factory에서 Spark aaaInvoke 프로그램 | Microsoft Docs"
description: "Tooinvoke Spark 프로그램을 사용 하 여 Azure 데이터 팩터리에서 MapReduce Activity hello 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Azure Data Factory 파이프라인에서 Spark 프로그램 호출

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 작업](data-factory-hive-activity.md)
> * [Pig 작업](data-factory-pig-activity.md)
> * [MapReduce 작업](data-factory-map-reduce.md)
> * [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
> * [Spark 작업](data-factory-spark.md)
> * [Machine Learning Batch 실행 작업](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 업데이트 리소스 작업](data-factory-azure-ml-update-resource-activity.md)
> * [저장 프로시저 작업](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 작업](data-factory-usql-activity.md)
> * [.NET 사용자 지정 작업](data-factory-use-custom-activities.md)

## <a name="introduction"></a>소개
Spark 활동을 사용 하면 hello 중 하나인 [데이터 변환 작업](data-factory-data-transformation-activities.md) Azure Data Factory에서 지원 합니다. 이 작업이 실행 지정 hello Azure HDInsight의 Apache Spark 클러스터에서 Spark 프로그램.    

> [!IMPORTANT]
> - Spark 활동은 기본 저장소로 Azure Data Lake Store를 사용하는 HDInsight Spark 클러스터를 지원하지 않습니다.
> - Spark 활동은 사용자 고유의 기존 HDInsight Spark 클러스터만 지원합니다. 주문형 HDInsight 연결된 서비스는 지원하지 않습니다.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>연습: Spark 활동이 포함된 파이프라인 만들기
Hello 일반적인 단계 toocreate Spark 활동으로 데이터 팩터리 파이프라인은 다음과 같습니다.  

1. 데이터 팩터리를 만듭니다.
2. Azure 저장소 연결 서비스 toolink HDInsight Spark 클러스터 toohello 데이터 팩터리와 연결 된 Azure 저장소를 만듭니다.     
2. Azure HDInsight toohello data factory에는 Azure HDInsight 연결 된 서비스 toolink Apache Spark 클러스터를 만듭니다.
3. Toohello Azure 저장소 연결 된 서비스를 참조 하는 데이터 집합을 만듭니다. 현재 생성 중인 출력이 없더라도 작업의 출력 데이터 집합을 지정해야 합니다.  
4. # 2에서 만든 toohello HDInsight 연결 된 서비스를 참조 하는 스파크 작업으로 파이프라인을 만듭니다. hello 활동 출력 데이터 집합으로 hello 이전 단계에서 만든 hello 데이터 집합으로 구성 됩니다. hello 출력 데이터 집합은 어떤 드라이브 hello 일정 (시간별, 일별, 등). 따라서 실제로 hello 활동 출력을 만들지 않고 하는 경우에 hello 출력 데이터 집합을 지정 해야 합니다.

### <a name="prerequisites"></a>필수 조건
1. 만들기는 **범용 Azure 저장소 계정** 지침 hello 연습에 따라: [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다.  
2. 만들기는 **Azure HDInsight의 Apache Spark 클러스터** hello 자습서의 지침에 따라: [Azure HDInsight의 Apache Spark 만드는 클러스터](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)합니다. 이 클러스터와 1 단계에서 만든 hello Azure 저장소 계정을 연결 합니다.  
3. 다운로드 하 여 hello python 스크립트 파일을 검토 **test.py** 에 있는: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py)합니다.  
3.  업로드 **test.py** toohello **pyFiles** 폴더 hello에 **adfspark** Azure Blob 저장소의 컨테이너입니다. 존재 하지 않는 경우 hello 컨테이너 및 hello 폴더를 만듭니다.

### <a name="create-data-factory"></a>데이터 팩터리 만들기
이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **새로** hello 왼쪽된 메뉴에서 클릭 **데이터 + 분석**, 클릭 하 고 **Data Factory**합니다.
3. Hello에 **새 데이터 팩터리** 블레이드에서 입력 **SparkDF** hello 이름에 대 한 합니다.

   > [!IMPORTANT]
   > hello Azure 데이터 팩터리에 hello 이름은 해야 **전역적으로 고유**합니다. Hello 오류가 나타나는 경우: **"SparkDF" 데이터 팩터리 이름을 사용할 수 없으면**합니다. 변경 hello hello 데이터 팩터리의 이름입니다 (예: yournameSparkDFdate, 및 다시 만듭니다. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.   
4. 선택 hello **Azure 구독** hello 데이터 팩터리 toobe 만든 원하는 합니다.
5. 기존 **리소스 그룹**을 선택하거나 Azure 리소스 그룹을 만듭니다.
6. 선택 **Pin toodashboard** 옵션입니다.  
6. 클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.

   > [!IMPORTANT]
   > toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.
7. Hello에 생성 되 고 hello 데이터 팩터리 참조 **대시보드** hello 다음과 같이 Azure 포털의.   
8. 보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다. Hello 데이터 팩터리 페이지를 표시 되지 않으면 hello 대시보드에서 데이터 팩터리에 대 한 hello 타일을 클릭 합니다.

    ![데이터 팩터리 블레이드](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>연결된 서비스 만들기
이 단계에서는 두 개의 연결 된 서비스를 하나의 toolink Spark 클러스터 tooyour 데이터 팩터리를 만들고 다른 toolink tooyour 데이터 팩터리를 Azure 저장소 hello 합니다.  

#### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다. 이 연습 뒷부분에 나오는 단계에서 만든 데이터 집합 toothis 연결 된 서비스를 참조 합니다. hello hello 다음 단계에서 정의 하는 HDInsight 연결 된 서비스는 너무 toothis 연결 된 서비스를 참조 합니다.  

1. 클릭 **작성자 및 배포** hello에 **Data Factory** 블레이드 데이터 팩토리에 대 한 합니다. 데이터 팩터리 편집기 hello를 표시 되어야 합니다.
2. **새 데이터 저장소**를 클릭하고 **Azure storage**를 선택합니다.

   ![새 데이터 저장소 - Azure Storage - 메뉴](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Hello 표시 되어야 **JSON 스크립트** Azure 저장소를 만들기 위한 hello 편집기에서 서비스를 연결 합니다.

   ![Azure 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. 대체 **계정 이름** 및 **계정 키** hello 사용자의 Azure 저장소 계정 이름과 액세스 키를 사용 합니다. toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.
5. toodeploy hello 연결 된 서비스를 클릭 **배포** hello 명령 모음에서 합니다. Hello 연결 된 서비스를 배포한 후 성공적으로 hello **Draft 1** 창 사라져야 나타나고 **AzureStorageLinkedService** hello 왼쪽 hello 트리 뷰에서 합니다.

#### <a name="create-hdinsight-linked-service"></a>HDInsight 연결된 서비스 만들기
이 단계에서는 Azure HDInsight 연결 된 서비스 toolink HDInsight Spark 클러스터 toohello 데이터 팩터리를 만듭니다. hello HDInsight 클러스터는이 샘플의 hello 파이프라인의 hello Spark 활동에 지정 된 사용 되는 toorun hello Spark 프로그램입니다.  

1. 도구 모음에서 **... 더 많은** hello 도구 모음에서 **새 계산**, 클릭 하 고 **HDInsight 클러스터**합니다.

    ![HDInsight 연결된 서비스 만들기](media/data-factory-spark/new-hdinsight-linked-service.png)
2. 복사 및 붙여넣기 다음 코드 조각 toohello hello **Draft 1** 창. Hello JSON 편집기에서 수행 hello 단계를 수행 합니다.
    1. Hello 지정 **URI** hello HDInsight Spark 클러스터입니다. 예: `https://<sparkclustername>.azurehdinsight.net/`
    2. Hello의 hello 이름을 지정 **사용자** 액세스 toohello Spark 클러스터를가지고 있는 사람입니다.
    3. Hello 지정 **암호** 사용자에 대 한 합니다.
    4. Hello 지정 **Azure 저장소 연결 된 서비스** hello HDInsight Spark 클러스터와 연결 된 합니다. 이 예제에서는 **AzureStorageLinkedService**입니다.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Spark 활동은 기본 저장소로 Azure Data Lake Store를 사용하는 HDInsight Spark 클러스터를 지원하지 않습니다.
    > - Spark 활동은 사용자 고유의 기존 HDInsight Spark 클러스터만 지원합니다. 주문형 HDInsight 연결된 서비스는 지원하지 않습니다.

    참조 [HDInsight 연결 된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) hello에 대 한 자세한 내용은 HDInsight 연결 된 서비스입니다.
3.  toodeploy hello 연결 된 서비스를 클릭 **배포** hello 명령 모음에서 합니다.  

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
hello 출력 데이터 집합은 어떤 드라이브 hello 일정 (시간별, 일별, 등). 따라서 hello 활동 실제로 출력을 생성 하지 않는 경우에 hello 파이프라인의 hello spark 활동에 대 한 출력 데이터 집합을 지정 해야 합니다. Hello 활동에 대 한 입력된 데이터 집합을 지정 하는 것은 선택 사항입니다.

1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택 하 고 **Azure Blob 저장소**합니다.  
2. 복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다. 라는 데이터 집합을 정의 하는 hello JSON 코드 조각은 **OutputDataset**합니다. Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfspark** 및 라고 하는 hello 폴더 **pyFiles/출력**합니다. 앞에서 설명한 대로 이 데이터 집합은 더미 데이터 집합입니다. 이 예제의 hello Spark 프로그램 출력을 생성 하지 않습니다. hello **가용성** 섹션 해당 hello 출력 데이터 집합을 매일 생성을 지정 합니다.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello 데이터 집합, 클릭 **배포** hello 명령 모음에서 합니다.


### <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **HDInsightSpark** 활동을 포함하는 파이프라인을 만듭니다. 현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다. Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다. 따라서 이 예제에서는 입력 데이터 집합을 지정하지 않습니다.

1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** 명령 모음 hello 되 고 클릭 **새 파이프라인**합니다.
2. Hello 스크립트를 hello Draft 1 창에 다음 스크립트는 hello로 바꿉니다.

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    포인트 다음 참고 hello:
    - hello **형식** 너무 속성이**HDInsightSpark**합니다.
    - hello **rootPath** 너무 설정**adfspark\\pyFiles** adfspark 란 pyFiles 고 hello Azure Blob 컨테이너는 세밀 하 게 폴더 해당 컨테이너에 있습니다. 이 예제에서는 hello Azure Blob 저장소는 hello 즉 hello Spark 클러스터와 연결 합니다. Hello 파일 tooa 업로드할 수 있습니다 다른 Azure 저장소입니다. 이렇게 하면 Azure 저장소 연결 서비스 toolink 해당 저장소 계정 toohello 데이터 팩터리를 만듭니다. 그런 다음 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **sparkJobLinkedService** 속성입니다. 참조 [Spark 활동 속성](#spark-activity-properties) hello Spark 활동에서 지 원하는 다른 속성 및이 속성에 대 한 세부 정보에 대 한 합니다.  
    - hello **entryFilePath** toohello 설정 **test.py**, hello python 파일인 합니다.
    - hello **getDebugInfo** 너무 속성이**항상**, (성공 또는 실패) 생성 된 hello 로그 파일은 항상 의미 합니다.

        > [!IMPORTANT]
        > 설정 하지 않으면이 속성 너무 권장`Always` 프로덕션 환경에서 문제를 해결 하는 경우가 아니면 합니다.
    - hello **출력** 섹션에는 하나의 출력 데이터 집합에 포함 합니다. Hello spark 프로그램 출력을 생성 하지 않는 경우에 출력 데이터 집합을 지정 해야 합니다. hello 출력 데이터 집합 드라이브 hello에 대 한 일정 hello 파이프라인 (시간별, 일별, 등).  

        Spark 활동에서 지 원하는 hello 속성에 대 한 세부 정보를 참조 하십시오. [활동 속성 멤버](#spark-activity-properties) 섹션.
3. toodeploy hello 파이프라인 클릭 **배포** hello 명령 모음에서 합니다.

### <a name="monitor-pipeline"></a>파이프라인 모니터링
1. 클릭 **X** tooclose 데이터 팩터리 편집기 블레이드와 toonavigate 다시 toohello Data Factory 홈 페이지입니다. 클릭 **모니터 및 관리** toolaunch hello 다른 탭에서 응용 프로그램을 모니터링 합니다.

    ![모니터링 및 관리 타일](media/data-factory-spark/monitor-and-manage-tile.png)
2. 변경 hello **시작 시간** hello 위쪽에 너무 필터링**2/1/2017**를 클릭 하 고 **적용**합니다.
3. 하루가 hello 사이 (2017-02-01)를 시작 및 종료 시간 (2017-02-02) hello 파이프라인의 그대로 활동 창이 하나만 표시 됩니다. 해당 hello 데이터 조각에 속하는지 확인 **준비** 상태입니다.

    ![모니터 hello 파이프라인](media/data-factory-spark/monitor-and-manage-app.png)    
4. 선택 hello **활동 창** hello 활동 실행에 대 한 toosee 세부 정보입니다. 오류가 발생 하는 hello 오른쪽 창에서 항목에 대 한 세부 정보 표시 됩니다.

### <a name="verify-hello-results"></a>Hello 결과 확인

1. https://CLUSTERNAME.azurehdinsight.net/jupyter로 이동하여 HDInsight Spark 클러스터에 대한 **Jupyter 노트북**을 실행합니다. 또한 HDInsight Spark 클러스터에 대한 클러스터 대시보드를 실행한 다음 **Jupyter 노트북**을 실행할 수도 있습니다.
2. 클릭 **새로** -> **PySpark** toostart 새 노트북 합니다.

    ![새 Jupyter 노트북](media/data-factory-spark/jupyter-new-book.png)
3. 실행 hello 다음 명령을 복사/붙여넣기 hello 텍스트 고 키를 눌러 **SHIFT + ENTER** hello hello 두 번째 문이 끝날 때.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Hello 테이블의에서 데이터를 hello hvac 표시 되는지 확인 합니다.  

    ![Jupyter 쿼리 결과](media/data-factory-spark/jupyter-notebook-results.png)

자세한 지침은 [Spark SQL 쿼리 실행](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) 섹션을 참조하세요. 

### <a name="troubleshooting"></a>문제 해결
설정한 이후로 **getDebugInfo** 너무**항상**, 표시는 **로그** hello에 하위 폴더로 **pyFiles** Azure Blob 컨테이너에 폴더입니다. hello 로그 폴더에 hello 로그 파일 추가 세부 정보를 제공합니다. 이 로그 파일은 오류가 발생할 때 특히 유용합니다. 프로덕션 환경에서 tooset 경우가 것 너무**오류**합니다.

추가 문제 해결에 대 한 않습니다 hello 단계를 수행 합니다.


1. 너무 이동`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`합니다.

    ![YARN UI 응용 프로그램](media/data-factory-spark/yarnui-application.png)  
2. 클릭 **로그** hello 중 하나에 대 한 시도 실행 합니다.

    ![응용 프로그램 페이지](media/data-factory-spark/yarn-applications.png)
3. Hello 로그 페이지에 추가 오류 정보가 표시 됩니다.

    ![로그 오류](media/data-factory-spark/yarnui-application-error.png)

다음 섹션 hello Data Factory 엔터티에 toouse Apache Spark 클러스터 및 데이터 팩터리에서 Spark 활동에 대 한 정보를 제공 합니다.

## <a name="spark-activity-properties"></a>Spark 활동 속성
Spark 활동을 포함 하는 파이프라인의 hello 샘플 JSON 정의 다음과 같습니다.    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

hello 다음 표에서 설명 hello JSON 정의에서 사용 되는 hello JSON 속성:

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| name | Hello 파이프라인의 hello 활동의 이름입니다. | 예 |
| 설명 | 어떤 hello 활동을 설명 하는 텍스트는 다음 작업을 수행 하지 않습니다. | 아니요 |
| type | 이 속성은 tooHDInsightSpark 설정 되어야 합니다. | 예 |
| linkedServiceName | 서비스는 hello Spark에서 프로그램 실행 연결 된 하는 hello HDInsight의 이름입니다. | 예 |
| rootPath | hello Azure Blob 컨테이너 및 hello Spark 파일이 있는 폴더입니다. hello 파일 이름은 대/소문자 구분입니다. | 예 |
| entryFilePath | Hello Spark 코드/패키지의 상대 경로 toohello 루트 폴더입니다. | 예 |
| className | 응용 프로그램의 Java/Spark main 클래스 | 아니요 |
| arguments | 명령줄 인수 toohello Spark 프로그램의 목록입니다. | 아니요 |
| proxyUser | hello 사용자 계정 tooimpersonate tooexecute hello Spark 프로그램 | 아니요 |
| sparkConfig | Hello 항목에 나열 된 Spark 구성 속성에 대 한 값을 지정: [Spark 구성-응용 프로그램 속성](https://spark.apache.org/docs/latest/configuration.html#available-properties)합니다. | 아니요 |
| getDebugInfo | Hello Spark 로그 파일에서 복사한 toohello HDInsight 클러스터에서 사용 하는 Azure 저장소를가 하는 경우를 지정 합니다 (또는) sparkJobLinkedService 하 여 지정 합니다. 허용되는 값: None, Always 또는 Failure. 기본값: None. | 아니요 |
| sparkJobLinkedService | hello hello Spark 작업 파일, 종속성 및 로그를 보유 하는 Azure 저장소 연결 된 서비스입니다.  이 속성에 대 한 값을 지정 하지 않으면 HDInsight 클러스터와 연결 된 hello 저장소 사용 됩니다. | 아니요 |

## <a name="folder-structure"></a>폴더 구조
Spark 활동 hello 인라인 스크립트 된 Pig로 지원 하지 않으며 Hive 작업을 수행 합니다. Spark 작업은 Pig/Hive 작업보다 확장성이 뛰어납니다. Spark 작업에 대 한 제공할 수 있습니다 여러 종속성와 같은 패키지 (hello java CLASSPATH에에서 배치 됨), python 파일 (PYTHONPATH hello에 배치 됨) 및 기타 파일 jar.

Hello 다음 hello hello HDInsight 연결 된 서비스에서 참조 하는 Azure Blob 저장소의에서 폴더 구조를 만듭니다. 그런 다음 나타내는 hello 루트 폴더에서 종속 파일 toohello 적절 한 하위 폴더를 업로드 **entryFilePath**합니다. 예를 들어 python 파일 toohello pyFiles 하위 폴더 및 jar 파일 toohello jar의 하위 폴더 hello 루트 폴더를 업로드 합니다. 런타임 시 데이터 팩터리 서비스는 hello Azure Blob 저장소의에서 폴더 구조를 다음 hello가 필요 합니다.     

| Path | 설명 | 필수 | 형식 |
| ---- | ----------- | -------- | ---- |
| 에서도 확인할 수 있습니다. | hello 저장소 연결 된 서비스에서 hello Spark 작업의 hello 루트 경로    | 예 | 폴더 |
| &lt;사용자 정의 &gt; | hello Spark 작업의 toohello 항목 파일을 가리키는 hello 경로 | 예 | 파일 |
| ./jars | 이 폴더 아래에 있는 모든 파일 업로드 되어 hello 클러스터의 hello java 클래스 경로에 저장 합니다. | 아니요 | 폴더 |
| ./pyFiles | 이 폴더 아래에 있는 모든 파일 업로드 되어 hello 클러스터의 PYTHONPATH hello에 저장 합니다. | 아니요 | 폴더 |
| ./files | 이 폴더 아래 모든 파일이 업로드되고 실행기 작업 디렉터리에 배치됨 | 아니요 | 폴더 |
| ./archives | 이 폴더 아래 모든 파일이 압축 해제됨 | 아니요 | 폴더 |
| ./logs | hello hello Spark 클러스터에서 로그를 저장 된 폴더에 있습니다.| 아니요 | 폴더 |

Hello hello HDInsight 연결 된 서비스에서 참조 하는 Azure Blob 저장소에서에서 두 개의 Spark 작업 파일을 포함 하는 저장소에 대 한 예를 들면 다음과 같습니다.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
