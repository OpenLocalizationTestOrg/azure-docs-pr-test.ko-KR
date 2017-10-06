---
title: "aaaBuild 첫 번째 데이터 팩터리 (Azure 포털) | Microsoft Docs"
description: "이 자습서에서는 데이터 팩터리 편집기를 사용 하 여 hello Azure 포털에서에서 샘플 Azure 데이터 팩터리 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>자습서: Azure Portal을 사용하여 첫 번째 Azure Data Factory 빌드
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-build-your-first-pipeline.md)
> * [Azure 포털](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 템플릿](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


이 문서에서는 설명 어떻게 toouse [Azure 포털](https://portal.azure.com/) toocreate 첫 번째 Azure 데이터 팩터리입니다. 다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다. 

이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다. 이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다. hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다. 

> [!NOTE]
> 이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
> 
> 파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
1. 자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.
2. 이 문서는 hello Azure 데이터 팩터리 서비스에 대 한 개념적인 개요를 제공 하지 않습니다. 통과 하는 것이 좋습니다 [소개 tooAzure Data Factory](data-factory-introduction.md) hello 서비스의 문서에 대 한 자세한 개요입니다.  

## <a name="create-data-factory"></a>데이터 팩터리 만들기
데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다. 이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **새로** hello 왼쪽된 메뉴에서 클릭 **데이터 + 분석**, 클릭 하 고 **Data Factory**합니다.

   ![블레이드 만들기](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. Hello에 **새 데이터 팩터리** 블레이드에서 입력 **GetStartedDF** hello 이름에 대 한 합니다.

   ![새 데이터 팩터리 블레이드](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > hello Azure 데이터 팩터리에 hello 이름은 해야 **전역적으로 고유**합니다. Hello 오류가 나타나면: **"GetStartedDF" 데이터 팩터리 이름을 사용할 수 없으면**합니다. Hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameGetStartedDF)을 변경 하 고 다시 만들어 보십시오. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.
   >
   > hello 데이터 팩터리의 hello 이름으로 등록 될 수는 **DNS** hello 미래에 이름을 지정 하 고 따라서 공개적으로 표시 됩니다.
   >
   >
4. 선택 hello **Azure 구독** hello 데이터 팩터리 toobe 만든 원하는 합니다.
5. 기존 **리소스 그룹** 을 선택하거나 리소스 그룹을 만듭니다. Hello 자습서에 대 한 명명 된 리소스 그룹 만들기: **ADFGetStartedRG**합니다.
6. 선택 hello **위치** hello 데이터 팩토리에 대 한 합니다. Hello 데이터 팩터리 서비스에서 지 원하는 영역 으로만 hello 드롭 다운 목록에 표시 됩니다.
7. 선택 **Pin toodashboard**합니다. 
8. 클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.

   > [!IMPORTANT]
   > toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.
   >
   >
7. 표시 상태와 함께 바둑판식으로 배열 하는 hello 다음 hello 대시보드에서: 데이터 팩터리를 배포 합니다.    

   ![데이터 팩터리 만들기 상태](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. 축하합니다. 첫 번째 데이터 팩터리 만들기가 완료되었습니다. 보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.     

    ![데이터 팩터리 블레이드](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Hello 데이터 팩터리에 파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다. 연결 된 서비스 toolink 저장소/계산 tooyour 데이터 저장의 입력 정의 및 연결 된 데이터 저장소의 데이터 집합 toorepresent 입/출력 데이터를 출력 하 고 데이터 다음 이러한 데이터 집합을 사용 하는 작업으로 hello 파이프라인을 만들 먼저 만들어야 합니다.

## <a name="create-linked-services"></a>연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 및 주문형 Azure HDInsight 클러스터 tooyour 데이터 팩터리를 연결합니다. 안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정. hello HDInsight 연결 된 서비스에 사용 되는 toorun hello 파이프라인이 샘플에서의 hello 활동에 지정 된 Hive 스크립트입니다. 식별할 [데이터 저장소](data-factory-data-movement-activities.md)/[계산 서비스](data-factory-compute-linked-services.md) 시나리오에 사용 되 고 해당 서비스 toohello 데이터 팩터리에 연결 된 서비스를 만들어 연결 합니다.  

### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다. 이 자습서를 사용 하 여 hello 스크립트 파일을 toostore 입/출력 데이터와 hello hql로 변환 하는 동일한 Azure 저장소 계정입니다.

1. 클릭 **작성자 및 배포** hello에 **DATA FACTORY** 블레이드 **GetStartedDF**합니다. 데이터 팩터리 편집기 hello를 표시 되어야 합니다.

   ![작성 및 배포 타일](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. **새 데이터 저장소**를 클릭하고 **Azure storage**를 선택합니다.

   ![새 데이터 저장소 - Azure Storage - 메뉴](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. 표시 되어야 hello Azure 저장소를 만들기 위한 JSON 스크립트 hello 편집기에서 서비스를 연결 합니다.

   ![Azure 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. 대체 **계정 이름** hello Azure 저장소 계정 이름으로 및 **계정 키** hello Azure 저장소 계정 액세스 키가 hello 인 합니다. toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.
5. 클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.

    ![배포 단추](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Hello 연결 된 서비스를 배포한 후 성공적으로 hello **Draft 1** 창 사라져야 나타나고 **AzureStorageLinkedService** hello 왼쪽 hello 트리 뷰에서 합니다.

    ![메뉴의 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스 만들기
이 단계에서는 주문형 HDInsight 클러스터 tooyour 데이터 팩터리에 연결합니다. hello HDInsight 클러스터는 자동으로 런타임 시 만들어지고 지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 삭제 합니다.

1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 추가**를 클릭하고 **새 계산**을 클릭하고 **주문형 HDInsight 클러스터**를 선택합니다.

    ![새 계산](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. 복사 및 붙여넣기 다음 코드 조각 toohello hello **Draft 1** 창. hello JSON 코드 조각은 hello 속성 사용 되는 toocreate hello 요청 시 HDInsight 클러스터에 설명 합니다.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

   | 속성 | 설명 |
   |:--- |:--- |
   | ClusterSize |Hello HDInsight 클러스터의 hello 크기를 지정합니다. |
   | TimeToLive | 삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다. |
   | linkedServiceName | HDInsight에서 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다. |

    포인트 다음 참고 hello:

   * hello 데이터 팩터리가 **Linux 기반** JSON hello로 있습니다에 대 한 HDInsight 클러스터입니다. 자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.
   * 주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다. 자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.
   * hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**). HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다. hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.

       많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.

     자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.
3. 클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.

    ![주문형 HDInsight 연결된 서비스 배포](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. 둘 다에 표시 되는지 확인 **AzureStorageLinkedService** 및 **HDInsightOnDemandLinkedService** hello 왼쪽 hello 트리 뷰에서 합니다.

    ![연결된 서비스와 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>데이터 집합 만들기
이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다. 이러한 데이터 집합 참조 toohello **AzureStorageLinkedService** 이 자습서의 앞부분에서 만든 합니다. Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.   

### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택 하 고 **Azure Blob 저장소**합니다.

    ![새 데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. 복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다. 라는 데이터 집합 hello JSON 조각에 만드는 **AzureBlobInput** hello 파이프라인의 활동에 대 한 입력된 데이터를 나타내는입니다. Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **inputdata**합니다.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

   | 속성 | 설명 |
   |:--- |:--- |
   | type |hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다. |
   | linkedServiceName |Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다. |
   | folderPath | Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다. | 
   | fileName |이 속성은 선택 사항입니다. 이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다. 이 자습서에서는 hello **input.log** 처리 됩니다. |
   | type |사용 하도록 hello 로그 파일은 텍스트 형식으로 **TextFormat**합니다. |
   | columnDelimiter |hello 로그 파일의 열으로 구분 됩니다 **쉼표 문자 (`,`)** |
   | frequency/interval |빈도 설정 너무**월** 간격은 및 **1**, 해당 hello를 의미 하는 분할 영역은 매월 입력 합니다. |
   | external | 이 속성은 너무**true** 경우 입력된 데이터 hello이이 파이프라인에서 생성 되지 않습니다. 이 자습서에서는 hello input.log 파일을 만들지이 파이프라인에서 설정 하 여 hello 속성 tootrue 하도록 합니다. |

    이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.
3. 클릭 **배포** hello 명령 모음 toodeploy hello 새로 만든 데이터 집합에 있습니다. Hello 왼쪽의 트리 보기를 hello hello 데이터 집합이 표시 됩니다.

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
이제, hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent hello 출력 데이터를 만듭니다.

1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택 하 고 **Azure Blob 저장소**합니다.  
2. 복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다. 라는 데이터 집합 hello JSON 조각에 만드는 **AzureBlobOutput**, hello hello 하이브 스크립트에 의해 생성 되는 hello 데이터 구조를 지정 하 고 있습니다. Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **partitioneddata**합니다. hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    참조 **hello 입력된 데이터 집합을 만들** 섹션 이러한 속성에 대 한 설명입니다. Hello dataset hello 데이터 팩터리 서비스에서 생성 된 것과 hello 외부 속성에는 출력 데이터 집합 설정 하지 마십시오.
3. 클릭 **배포** hello 명령 모음 toodeploy hello 새로 만든 데이터 집합에 있습니다.
4. 데이터 집합의 hello 성공적으로 생성 되었는지 확인 합니다.

    ![연결된 서비스와 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **HDInsightHive** 작업을 사용하여 첫 번째 파이프라인을 만듭니다. 입력된 조각이 매월 (빈도: 월, 간격: 1), 출력 조각이 매월, 생성 되 고 hello 활동에 대 한 hello 스케줄러 속성 toomonthly도 설정 됩니다. hello 출력 데이터 집합 및 작업 스케줄러 hello에 대 한 hello 설정을 일치 해야 합니다. 현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다. Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다. 다음 JSON hello에 사용 되는 hello 속성 hello 끝이 섹션에 설명 되어 있습니다.

1. Hello에 **데이터 팩터리 편집기**, 클릭 **줄임표 (...) 더 많은 명령이** 클릭 하 고 **새 파이프라인**합니다.

    ![새 파이프라인 단추](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. 복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다.

   > [!IMPORTANT]
   > 대체 **storageaccountname** hello hello JSON에서에서 저장소 계정의 이름으로 합니다.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **AzureStorageLinkedService**), 및  **스크립트** hello 컨테이너에 폴더 **adfgetstarted**합니다.

    hello **정의** 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

    hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다.

    Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.

   > [!NOTE]
   > "파이프라인 JSON"을 참조 [파이프라인 및 활동 Azure Data Factory에](data-factory-create-pipelines.md) hello 예제에 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 합니다.
   >
   >
3. Hello 다음을 확인 합니다.

   1. **input.log** hello에 파일이 **inputdata** hello의 폴더 **adfgetstarted** hello Azure blob 저장소의에서 컨테이너
   2. **partitionweblogs.hql** hello에 파일이 **스크립트** hello의 폴더 **adfgetstarted** hello Azure blob 저장소의에서 컨테이너입니다. Hello에서 단계를 완료 hello prerequisite [자습서 개요](data-factory-build-your-first-pipeline.md) 이러한 파일에 표시 되지 않으면 합니다.
   3. 대체 했는지 확인 **storageaccountname** hello hello에서 저장소 계정의 이름으로 JSON을 파이프라인 합니다.
4. 클릭 **배포** hello 명령 모음 toodeploy hello 파이프라인에 있습니다. Hello 이후 **시작** 및 **끝** 시간이 지난 hello에 설정 된 및 **isPaused** 배포한 후에 즉시 집합 toofalse, hello 파이프라인 (hello 파이프라인의 활동)을 실행 됩니다.
5. Hello 파이프라인 hello 트리 보기에 표시 되는지 확인 합니다.

    ![파이프라인과 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. 축하합니다. 첫 번째 파이프라인 만들기가 완료되었습니다.

## <a name="monitor-pipeline"></a>파이프라인 모니터링
### <a name="monitor-pipeline-using-diagram-view"></a>다이어그램 보기를 사용하여 파이프라인 모니터링
1. 클릭 **X** tooclose 데이터 팩터리 편집기 블레이드를 toonavigate toohello Data Factory 블레이드를 다시 마우스 클릭 **다이어그램**합니다.

    ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. 다이어그램 보기 hello에 hello 파이프라인 및이 자습서에 사용 되는 데이터 집합에 대해 간략하게를 표시 됩니다.

    ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview hello 파이프라인에서 마우스 오른쪽 단추로 클릭 파이프라인 hello에 모든 활동 다이어그램 및 열기 파이프라인을 클릭 합니다.

    ![파이프라인 열기 메뉴](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Hello 파이프라인의 hello HDInsightHive 활동 표시 되는지 확인 합니다.

    ![파이프라인 보기 열기](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate toohello 이전 뷰를 다시 클릭 **Data factory** hello 위쪽 hello 이동 경로 탐색 메뉴에 있습니다.
5. Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobInput**합니다. 해당 hello 조각이에 속하는지 확인 **준비** 상태입니다. 준비 상태가 몇 hello 조각 tooshow 분이 걸릴 수도 있습니다. 잠시을 대기한 후에 발생 하지 않습니다, 경우 hello 오른쪽 컨테이너 (adfgetstarted) 및 폴더 (inputdata)에 배치 입력된 hello 파일 (input.log) 되었는지 확인 합니다.

   ![준비 상태인 입력 조각](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. 클릭 **X** tooclose **AzureBlobInput** 블레이드입니다.
7. Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobOutput**합니다. 현재 처리 중인 해당 hello 조각이 표시 됩니다.

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Hello 조각 참조 처리가 완료 되 면 **준비** 상태입니다.

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > 주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분) 따라서 hello 파이프라인 될 너무 걸릴 **약 30 분** tooprocess hello 조각입니다.
   >
   >

9. Hello 조각화 된 경우 **준비** 상태, hello 확인 **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.  

   ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. 에 대 한 hello 조각 toosee 세부 정보 클릭는 **데이터 조각을** 블레이드입니다.

   ![데이터 조각 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Hello에서 실행할 활동을 클릭 **활동 실행 목록** 안에 (시나리오에서 하이브 활동)을 실행 하는 활동에 대 한 toosee 세부 정보는 **활동 실행 정보** 창.   

   ![작업 실행 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Hello 로그 파일에서 실행 된 hello 하이브 쿼리 및 상태 정보를 볼 수 있습니다. 이러한 로그는 문제를 해결하는 데 유용합니다.
   자세한 내용은 [Azure 포털 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 를 참조하세요.

> [!IMPORTANT]
> 입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다. 따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>앱 모니터링 및 관리를 사용하여 파이프라인 모니터링
모니터를 사용 하 여 & toomonitor 응용 프로그램 파이프라인을 관리할 수도 있습니다. 이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.

1. 클릭 **모니터링 및 관리** 데이터 팩토리에 대 한 hello 홈 페이지에 바둑판식으로 배열 합니다.

    ![타일 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. **응용 프로그램 모니터링 및 관리**가 표시되어야 합니다. 변경 hello **시작 시간** 및 **종료 시간** toomatch 시작 및 종료 시간 프로그램 파이프라인을 하 고 클릭 **적용**합니다.

    ![앱 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Hello에 활동을 선택 **활동 창** toosee 세부 정보를 나열 합니다.

    ![활동 창 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>참고 항목
| 항목 | 설명 |
|:--- |:--- |
| [파이프라인](data-factory-create-pipelines.md) |이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다. |
| [데이터 집합](data-factory-create-datasets.md) |이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다. |
| [예약 및 실행](data-factory-scheduling-and-execution.md) |이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다. |
| [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) |이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다. |
