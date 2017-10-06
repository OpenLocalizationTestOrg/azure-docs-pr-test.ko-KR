---
title: "많은 양의 오프 라인 메서드를 사용 하 여 데이터 레이크 저장소로 데이터를 aaaUpload | Microsoft Docs"
description: "사용 하 여 hello Azure 저장소에서 AdlCopy 도구 toocopy 데이터 레이크 저장소 tooData blob"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>데이터 tooData 레이크 저장소의 오프 라인 복사본에 대 한 hello Azure 가져오기/내보내기 서비스를 사용 하 여
이 문서에서는 알아봅니다 toocopy 대규모 데이터 설정 하는 방법 (> 200GB) hello와 같은 오프 라인 복사 방법을 사용 하 여 Azure 데이터 레이크 저장소에 [Azure 가져오기/내보내기 서비스](../storage/common/storage-import-export-service.md)합니다. 특히,이 문서의 예제로 사용 하는 hello 파일은 339,420,860,416 바이트 또는 디스크에 약 319 g B입니다. 이 파일을 319GB.tsv라고 하겠습니다.

Azure 가져오기/내보내기 서비스 hello tootransfer 많은 양의 데이터를 안전 하 게 전달 하드 디스크에서 Blob 저장소 tooAzure 드라이브 tooan Azure 데이터 센터 보다 상세하게 수 있습니다.

## <a name="prerequisites"></a>필수 조건
시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure Storage 계정**
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Hello 데이터 준비
나누기 hello 데이터 파일 toobe hello 가져오기/내보내기 서비스를 사용 하기 전에 전송 **200GB 미만 않은 복사본에** 크기에서입니다. 200GB 보다 큰 파일 hello 가져오기 도구를 작동 하지 않습니다. 이 자습서에서는 각 100GB의 청크로 hello 파일을 분할 합니다. [Cygwin](https://cygwin.com/install.html)을 사용하면 이렇게 수행할 수 있습니다. Cygwin은 Linux 명령을 지원합니다. 이 경우 다음 명령을 hello를 사용 합니다.

    split -b 100m 319GB.tsv

hello split 작업 이름 다음 hello로 파일을 만듭니다.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>데이터와 함께 디스크 준비
Hello 지침에 따라 [hello Azure 가져오기/내보내기 서비스를 사용 하 여](../storage/common/storage-import-export-service.md) (hello 아래 **드라이브를 준비** 섹션) tooprepare 하드 드라이브입니다. 다음은 전체 순서 hello:

1. Hello Azure 가져오기/내보내기 서비스에 사용 되는 hello 요구 사항 toobe 충족 하는 하드 디스크를 조달할 합니다.
2. Azure 저장소 계정이 배송된 toohello Azure 데이터 센터 않아 hello 데이터 복사 될 위치를 식별 합니다.
3. 사용 하 여 hello [Azure 가져오기/내보내기 도구](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), 명령줄 유틸리티입니다. Toouse 도구 hello 하는 방법을 보여 주는 샘플 코드 조각은 다음과 같습니다.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    참조 [hello Azure 가져오기/내보내기 서비스를 사용 하 여](../storage/common/storage-import-export-service.md) 더 많은 샘플 조각에 대 한 합니다.
4. hello 앞의 명령은 저널을 만듭니다는 hello에서 파일 위치를 지정 합니다. 이 저널 파일 toocreate hello에서 가져오기 작업을 사용 하 여 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.

## <a name="create-an-import-job"></a>가져오기 작업 만들기
지침에 hello를 사용 하 여 이제는 가져오기 작업을 만들 수 있습니다 [hello Azure 가져오기/내보내기 서비스를 사용 하 여](../storage/common/storage-import-export-service.md) (hello 아래 **hello 가져오기 작업 만들기** 섹션). 이 가져오기 작업에 대 한 기타 세부 정보 또한 제공할 hello 디스크 드라이브를 준비 하는 동안 만든 hello 저널 파일.

## <a name="physically-ship-hello-disks"></a>Hello 디스크 배달
이제 hello 디스크 tooan Azure 데이터 센터를 물리적으로 제공할 수 있습니다. 여기에 hello 데이터가 hello 가져오기 작업을 만드는 동안 제공한 toohello Azure 저장소 blob 복사 됩니다. 또한 hello 작업을 만드는 동안 정보를 나중에 추적 tooprovide hello를 선택한 경우 이제 다시 할 수 있습니다 tooyour 가져오기 작업 및 update hello 추적 번호입니다.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Azure 저장소 blob tooAzure 데이터 레이크 저장소에서 데이터를 복사 합니다.
Hello의 hello 상태 후 가져오기 작업이 완료 될, hello 데이터를 지정한 hello Azure 저장소 blob에 사용할 수 있는지 여부를 확인할 수 있습니다를 표시 합니다. 다양 한 메서드 toomove hello 데이터로 tooAzure 데이터 레이크 저장소 blob을 유도할 수 있습니다. 모든 데이터를 업로드 하기 위한 사용 가능한 옵션 hello, 참조 [데이터 레이크 저장소로 데이터를 수집 하는 방법](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store)합니다.

이 섹션에서는 제공 hello JSON 정의 데이터를 복사 하기 위한 toocreate Azure 데이터 팩터리 파이프라인을 사용할 수 있습니다. Hello에서 이러한 JSON 정의 사용할 수 있습니다 [Azure 포털](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), 또는 [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md)합니다.

### <a name="source-linked-service-azure-storage-blob"></a>원본에 연결된 서비스(Azure Storage Blob)
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a>대상에 연결된 서비스(Azure Data Lake Store)
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a>입력 데이터 집합
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a>출력 데이터 집합
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a>파이프라인(복사 작업)
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
자세한 내용은 참조 [Azure 저장소에서 데이터에는 Azure 데이터 팩터리를 사용 하 여 tooAzure 데이터 레이크 저장소 blob 이동](../data-factory/data-factory-azure-datalake-connector.md)합니다.

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Azure 데이터 레이크 저장소의 데이터 파일 hello를 다시 생성
319 GB 였으며 중단 것 더 작은 크기의 파일로 hello Azure 가져오기/내보내기 서비스를 사용 하 여 전송할 수 있도록 하는 파일 시작 했습니다.입니다. Hello 데이터는 Azure 데이터 레이크 저장소에 했으므로 hello 파일 tooits 원래 크기를 다시 구성할 수 있습니다. 따라서 Azure PowerShell cmldts toodo 다음 hello를 사용할 수 있습니다.

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a>다음 단계
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
