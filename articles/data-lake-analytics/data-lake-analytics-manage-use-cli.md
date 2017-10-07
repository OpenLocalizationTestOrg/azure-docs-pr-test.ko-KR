---
title: "Azure 명령줄 인터페이스를 사용 하 여 Azure Data Lake 분석 aaaManage | Microsoft Docs"
description: "Toomanage Data Lake 분석 계정, 데이터 원본 작업 하는 방법 및 Azure CLI를 사용 하 여 사용자에 알아봅니다"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Azure 명령줄 인터페이스(CLI)를 사용하여 Azure 데이터 레이크 분석 관리
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

어떻게 toomanage Azure Data Lake 분석 계정, 데이터 원본, 사용자 및 사용 하 여 작업 hello Azure CLI에 알아봅니다. 다른 도구를 사용 하 여 toosee 관리 항목을 클릭 하 여 위의 hello 탭 선택 합니다.


**필수 구성 요소**

이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure CLI**. [Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.
  * 다운로드 및 설치 hello **시험판** [Azure CLI 도구](https://github.com/MicrosoftBigData/AzureDataLake/releases) 의 순서로 toocomplete이이 데모입니다.
* **인증**를 사용 하 여 다음 명령을 hello:
  
        azure login
    회사 또는 학교 계정을 사용 하 여 인증에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI에서에서 tooan Azure 구독 연결](../xplat-cli-connect.md)합니다.
* **Toohello Azure Resource Manager 모드로 전환**를 사용 하 여 다음 명령을 hello:
  
        azure config mode arm

**toolist hello 데이터 레이크 저장소 및 데이터 레이크 분석 명령:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>계정 관리
데이터 레이크 분석 작업을 실행하려면 데이터 레이크 분석 계정이 있어야 합니다. Azure HDInsight와 달리 작업을 실행하지 않는 경우 분석 계정에 대해 비용을 지불하지 않습니다.  Hello 시간 작업을 실행 중인 경우에 지불 합니다.  자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.  

### <a name="create-accounts"></a>계정 만들기
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>계정 업데이트
hello 다음 명령을 hello의 속성을 업데이트는 기존 데이터 레이크 분석 계정

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>계정 나열
데이터 레이크 분석 계정을 나열합니다. 

    azure datalake analytics account list

특정 리소스 그룹 내의 데이터 레이크 분석 계정 나열

    azure datalake analytics account list -g "<Azure Resource Group Name>"

특정 데이터 레이크 분석 계정의 세부 정보 가져오기

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>데이터 레이크 분석 계정 삭제
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>계정 데이터 원본 관리
Data Lake 분석에는 현재 데이터 원본 hello를 지원 합니다.

* [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md)
* [Azure 저장소](../storage/common/storage-introduction.md)

분석 계정을 만들 때 Azure 데이터 레이크 저장소 계정 toobe hello 기본 저장소 계정을 지정 해야 합니다. hello 기본 ADL 저장소 계정이 사용 toostore 작업 메타 데이터 및 작업에 대 한 감사 로그 합니다. 분석 계정을 만든 후 데이터 레이크 저장소 계정 및/또는 Azure 저장소 계정을 더 추가할 수 있습니다. 

### <a name="find-hello-default-adl-storage-account"></a>Hello 기본 ADL 저장소 계정 찾기
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

hello 값 속성: datalakeStoreAccount:name 나열 됩니다.

### <a name="add-additional-azure-blob-storage-accounts"></a>Azure Blob 저장소 계정 추가
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Blob 저장소 짧은 이름만 지원됩니다.  FQDN(예: “myblob.blob.core.windows.net”)을 사용하지 마십시오.
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>데이터 레이크 저장소 계정 추가
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d]은 선택적 스위치 tooindicate hello 추가 되는 데이터 레이크 hello 기본 데이터 레이크 계정 인지 합니다. 

### <a name="update-existing-data-source"></a>기존 데이터 원본 업데이트
기존 데이터 레이크 저장소 계정 toobe hello 기본값 tooset:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate 기존 Blob 저장소 계정 키:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>데이터 원본 나열:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![데이터 레이크 분석은 데이터 원본을 나열합니다.](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>데이터 원본 삭제:
toodelete 데이터 레이크 저장소 계정:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete Blob 저장소 계정:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>작업 관리
작업을 만들려면 데이터 레이크 분석 계정이 있어야 합니다.  자세한 내용은 [데이터 레이크 분석 계정 관리](#manage-accounts)를 참조하세요.

### <a name="list-jobs"></a>작업 나열
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![데이터 레이크 분석은 데이터 원본을 나열합니다.](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>작업 세부 정보 가져오기
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>작업 제출
> [!NOTE]
> 작업의 기본 우선 순위 hello은 1000으로 및 hello 기본 수준의 작업에 대 한 병렬 처리는 1입니다.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>작업 취소
Hello 목록 명령 toofind hello 작업 id를 사용 하 고 toocancel hello 작업 취소를 사용 합니다.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>카탈로그 관리
hello U-SQL 카탈로그 이므로 toostructure 사용 되는 데이터와 코드 U-SQL 스크립트에서 공유할 수 있습니다. hello 카탈로그에서 Azure 데이터 레이크 데이터 가능한 최고 성능을 hello 수 있습니다. 자세한 내용은 [U-SQL 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.

### <a name="list-catalog-items"></a>카탈로그 항목 나열
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

hello 유형은 데이터베이스, 스키마, 어셈블리, 외부 데이터 원본, 테이블, 테이블 반환 함수 또는 테이블 통계를 포함합니다.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>ARM 그룹 사용
응용 프로그램은 일반적으로 웹앱, 데이터베이스, 데이터베이스 서버, 저장소 및 타사 서비스 등 많은 구성 요소로 구성됩니다. Azure 리소스 관리자 (ARM) toowork를 hello 리소스 그룹 참조 tooas Azure 리소스 그룹으로 응용 프로그램에 있습니다. 배포 업데이트 하거나 모니터링 단일, 통합 작업에서 응용 프로그램에 대 한 모든 hello 리소스를 삭제할 수 있습니다. 배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다. Hello 전체 그룹에 대 한 hello 겹쳐서 비용을 확인 하 여 조직에 대 한 요금 청구를 확인할 수 있습니다. 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요. 

Data Lake 분석 서비스는 다음과 같은 구성 요소가 hello를 포함할 수 있습니다.

* Azure 데이터 레이크 분석 계정
* 필수 기본 Azure 데이터 레이크 저장소 계정
* 추가 Azure 데이터 레이크 저장소 계정
* 추가 Azure 저장소 계정

하나의 ARM 그룹 toomake에서 이러한 모든 구성이 요소를 만들 수 있습니다에 보다 쉽게 toomanage 합니다.

![Azure 데이터 레이크 분석 계정 및 저장소](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Data Lake 분석 계정 및 hello 종속 저장소 계정에에서 배치 해야 hello 동일한 Azure 데이터 센터입니다.
그러나 hello ARM 그룹 다른 데이터 센터에 위치할 수 있습니다.  

## <a name="see-also"></a>참고 항목
* [Microsoft Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Azure 포털을 사용하여 데이터 레이크 분석 시작](data-lake-analytics-get-started-portal.md)
* [Azure 포털을 사용하여 Azure 데이터 레이크 분석 관리](data-lake-analytics-manage-use-portal.md)
* [Azure 포털을 사용하여 Azure 데이터 레이크 분석 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

