---
title: "데이터 레이크 저장소에 Azure 저장소 Blob 데이터로 aaaCopy | Microsoft Docs"
description: "Azure 저장소 Blob tooData 레이크 스토어에서 AdlCopy 도구 toocopy 데이터를 사용 하 여"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사
> [!div class="op_single_selector"]
> * [DistCp 사용](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy 사용](data-lake-store-copy-data-azure-storage-blob.md)
>
>

명령줄 도구를 제공 하는 azure 데이터 레이크 저장소 [AdlCopy](http://aka.ms/downloadadlcopy), 원본 hello에서 toocopy 데이터:

* Azure 저장소 Blob에서 Data Lake Store로 데이터 레이크 저장소 tooAzure 저장소 blob에서 AdlCopy toocopy 데이터를 사용할 수 없습니다.
* 두 Azure Data Lake Store 계정 간

또한, 두 가지 모드로 hello AdlCopy 도구를 사용할 수 있습니다.

* **독립 실행형**hello 도구 데이터 레이크 저장소 리소스 tooperform hello 작업을 사용 합니다.
* **Data Lake 분석 계정을 사용 하 여**에서 tooyour Data Lake 분석 계정에 할당 하는 hello 단위가 사용 되는 tooperform hello 복사 작업입니다. 예측 가능한 방식으로 tooperform hello 복사 작업을 볼 때이 옵션 toouse 할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 저장소 Blob** 컨테이너
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* **Azure Data Lake 분석 계정 (선택 사항)** -참조 [Azure Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md) 어떻게 toocreate 데이터 레이크 저장소에 대 한 지침은 계정.
* **AdlCopy 도구**. Hello AdlCopy 도구를 설치 [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy)합니다.

## <a name="syntax-of-hello-adlcopy-tool"></a>Hello AdlCopy 도구의 구문
다음 구문 toowork hello AdlCopy 도구로 hello를 사용 하 여

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

hello 구문에서 매개 변수 hello은 다음과 같습니다.

| 옵션 | 설명 |
| --- | --- |
| 원본 |Hello Azure 저장소 blob에 hello 원본 데이터의 hello 위치를 지정합니다. hello 원본은 blob 컨테이너, blob 또는 다른 데이터 레이크 저장소 계정 수 있습니다. |
| Dest |Hello 데이터 레이크 저장소 대상 toocopy를 지정합니다. |
| SourceKey |Hello Azure 저장소 blob 원본에 대 한 hello 저장소 액세스 키를 지정합니다. 이 hello 소스는 blob 컨테이너 또는 blob 하는 경우에 필요 합니다. |
| 계정 |**옵션**. Toouse Azure Data Lake 분석 계정 toorun hello 복사 작업을 원하는 경우이 사용 합니다. Hello /Account 옵션을 사용 하 여 hello 구문에서 Data Lake 분석 계정 지정 하지 않은 경우 AdlCopy 기본 계정 toorun hello 작업을 사용 합니다. 또한이 옵션을 사용 하는 경우 추가 해야 hello 원본 (Azure 저장소 Blob) 및 대상 (Azure 데이터 레이크 저장소) 데이터 원본으로 Data Lake 분석 계정에 대 한 합니다. |
| Units |Hello hello 복사 작업에 사용할 데이터 레이크 분석 단위 수를 지정 합니다. 이 옵션은 hello를 사용 하는 경우 필수 **/계정** toospecify hello Data Lake 분석 계정 옵션입니다. |
| 패턴 |어떤 blob 또는 파일 toocopy 나타내는 regex 패턴을 지정 합니다. AdlCopy는 대/소문자 구분 일치를 사용합니다. 기본 패턴 hello 패턴이 없는 toocopy 모든 항목은 지정 된 경우에 사용 됩니다. 여러 파일 패턴을 지정할 수는 없습니다. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Azure 저장소 blob에서 (독립 실행형)으로 AdlCopy toocopy 데이터 사용
1. 명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.
2. Hello 소스 컨테이너 tooa 데이터 레이크 저장소에서에서 다음 명령을 toocopy hello 특정 blob을 실행 합니다.

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    예:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] 위의 hello 구문 hello Data Lake 저장소 계정에서 hello 파일 toobe 복사한 tooa 폴더를 지정합니다. AdlCopy 도구 hello 지정한 폴더 이름이 존재 하지 않는 경우 폴더를 만듭니다.

    됩니다 증명된 tooenter hello 자격 증명에 대 한 hello Azure 구독이 있는 데이터 레이크 저장소 계정이 필요 합니다. 출력 유사한 toohello 다음을 표시 됩니다.

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. 또한 다음 명령을 hello를 사용 하 여 하나의 컨테이너 toohello Data Lake 저장소 계정에서 모든 hello blob을 복사할 수 있습니다.

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    예:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>성능 고려 사항

Azure Blob 저장소 계정에서 복사 하는 경우 blob 저장소 면 hello에 복사 하는 동안 제한 될 수 있습니다. 이 복사 작업의 hello 성능이 저하 됩니다. Azure Blob 저장소의 hello 제한에 대 한 더 toolearn 참조에서 Azure 저장소 제한 [Azure 구독 및 서비스 제한](../azure-subscription-service-limits.md)합니다.

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>다른 데이터 레이크 저장소 계정에서 독립 실행형) (으로 AdlCopy toocopy 데이터 사용
두 데이터 레이크 저장소 계정 간에 AdlCopy toocopy 데이터를 사용할 수 있습니다.

1. 명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.
2. 데이터 레이크 저장소 계정 tooanother 하나에서 다음 명령 toocopy hello 특정 파일을 실행 합니다.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    예:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > 위의 hello 구문 hello 대상 데이터 레이크 저장소 계정에서 hello 파일 toobe 복사한 tooa 폴더를 지정합니다. AdlCopy 도구 hello 지정한 폴더 이름이 존재 하지 않는 경우 폴더를 만듭니다.
   >
   >

    됩니다 증명된 tooenter hello 자격 증명에 대 한 hello Azure 구독이 있는 데이터 레이크 저장소 계정이 필요 합니다. 출력 유사한 toohello 다음을 표시 됩니다.

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. hello 다음 명령은 모든 파일 복사 hello 대상 데이터 레이크 저장소 계정에에서 hello 원본 데이터 레이크 저장소 계정 tooa 폴더에 있는 특정 폴더에서 합니다.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>성능 고려 사항

AdlCopy를 독립 실행형 도구로 사용할 때는 hello 복사본 공유에서 실행 되, Azure 관리 되는 리소스입니다. 이 환경에서 발생할 수 있습니다 hello 성능 시스템 부하 및 사용 가능한 리소스에 따라 다릅니다. 이 모드는 임시로 작은 양을 전송하는 데 가장 적합합니다. 매개 변수는 독립 실행형 도구로 AdlCopy를 사용 하는 경우 튜닝 toobe가 필요 합니다.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Data Lake 분석 계정) (으로 AdlCopy toocopy 데이터 사용
데이터 레이크 분석을 사용할 수도 있습니다 toorun hello AdlCopy 작업 toocopy 데이터를 Azure 저장소에서에서 blob tooData Lake 저장소 계정입니다. 이 옵션을 hello 데이터 toobe 이동 기가바이트 및 단위를 hello 범위 이며 더 나은 및 예측 가능한 성능 처리량을 원하는 경우에 일반적으로 사용 합니다.

toouse AdlCopy toocopy hello 원본 (Azure 저장소 Blob)는 Azure 저장소 Blob에서 사용 하 여 Data Lake 분석 계정 Data Lake 분석 계정에 대 한 데이터 원본으로 추가 해야 합니다. 추가 데이터 소스 tooyour Data Lake 분석 계정을 추가 하는 방법에 지침은 [관리 Data Lake 분석 계정 데이터 원본](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources)합니다.

> [!NOTE]
> Data Lake 분석 계정을 사용 하 여 hello 소스로 Azure 데이터 레이크 저장소 계정에서 복사 하는 경우에 Data Lake 분석 계정 hello로 tooassociate hello Data Lake 저장소 계정이 설치할 필요가 없습니다. hello 요구 사항 tooassociate hello 소스 저장소 Data Lake 분석 계정 hello로는 hello 소스에는 Azure 저장소 계정은 경우에입니다.
>
>

Hello 명령 toocopy Data Lake 분석 계정을 사용 하 여 Azure 저장소 blob tooa Data Lake 저장소 계정에서 다음을 실행 합니다.

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

예:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

마찬가지로, hello 명령 toocopy Data Lake 분석 계정을 사용 하 여 Azure 저장소 blob tooa Data Lake 저장소 계정에서 다음을 실행 합니다.

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>성능 고려 사항

테라바이트 hello 범위에서 데이터를 복사, AdlCopy 사용자의 Azure Data Lake 분석 계정으로 사용 하 여 더 나은 및 예측 가능성이 더욱 뛰어난 성능을 제공 합니다. 튜닝 해야 하는 hello 매개 변수는 hello 복사 작업에 대 한 Azure 데이터 레이크 분석 단위 toouse hello 수입니다. Hello 단위 수를 늘리면 복사 작업의 hello 성능이 향상 됩니다. 복사 된 각 파일 toobe 최대 단위 하나를 사용할 수 있습니다. 복사 될 파일의 hello 수보다 더 많은 단위를 지정 하는 성능을 증가 되지 않습니다.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>패턴 일치를 사용 하 여 AdlCopy toocopy 데이터 사용
이 섹션에서는 설명 어떻게 toouse AdlCopy toocopy data from a (아래 예에서 사용 하 여 Azure 저장소 Blob) 패턴 일치를 사용 하 여 tooa 대상 데이터 레이크 저장소 계정입니다. 예를 들어 사용할 수 있습니다 hello 단계 toocopy 아래의 모든 파일 hello 원본 blob toohello 대상에서.csv 확장명으로.

1. 명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.
2. 다음 명령은 toocopy hello 모든 파일을 실행 *.csv 확장명으로 hello 소스 컨테이너 tooa 데이터 레이크 저장소에서에서 특정 blob에서:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    예:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>결제
* 청구 되는 독립 실행형으로 hello AdlCopy 도구를 사용 하 여 이동 하기 위한 송신 비용에 대 한 데이터를 hello 원본 Azure 저장소 계정에 없는 경우 데이터 레이크 저장소 hello으로 같은 지역을 hello 합니다.
* 데이터 레이크 분석을 hello AdlCopy 도구를 사용 하는 경우 계정, 표준 [요금이 청구 Data Lake 분석](https://azure.microsoft.com/pricing/details/data-lake-analytics/) 적용 됩니다.

## <a name="considerations-for-using-adlcopy"></a>AdlCopy 사용에 대한 고려 사항
* AdlCopy(버전 1.0.5)는 모두 수천 개가 넘는 파일과 폴더가 있는 원본에서 데이터를 복사하는 작업을 지원합니다. 그러나 크기가 큰 데이터 집합을 복사 하는 문제가 발생 하는 경우 hello 파일/폴더를 여러 하위 폴더에 배포할 수 있고 hello 소스로 hello 경로 toothose 하위 폴더를 대신 사용 합니다.

## <a name="performance-considerations-for-using-adlcopy"></a>AdlCopy 사용에 대한 성능 고려 사항

AdlCopy는 수천 개의 파일 및 폴더가 포함된 데이터의 복사를 지원합니다. 그러나 크기가 큰 데이터 집합을 복사 하는 문제가 발생 하는 경우 더 작은 하위 폴더로 hello 파일/폴더를 배포할 수 있습니다. AdlCopy는 임시 복사본용으로 빌드되었습니다. 사용을 고려해 야 반복적 toocopy 데이터를 보려고 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) hello 복사 작업 중심 전체 관리 기능을 제공 하는 합니다.

## <a name="release-notes"></a>릴리스 정보
* 1.0.13-toohello 데이터를 복사 하는 경우 동일한 Azure 데이터 레이크 저장소 계정에서 여러 adlcopy 명령 각각에 대 한 자격 증명은 더 이상 실행 tooreenter 필요가 없습니다. 이제 Adlcopy가 여러 번 실행할 때 해당 정보를 캐시합니다.

## <a name="next-steps"></a>다음 단계
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
