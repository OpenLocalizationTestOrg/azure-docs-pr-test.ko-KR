---
title: "aaaGet Azure CLI 2.0을 사용 하 여 Azure Data Lake 분석 시작 | Microsoft Docs"
description: "Toouse hello Azure 명령줄 인터페이스 2.0 toocreate Data Lake 분석 계정 U SQL을 사용 하 여 데이터 레이크 분석 작업 만들기 하 고 hello 작업을 제출 하는 방법을 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Azure CLI 2.0를 사용하여 Azure Data Lake Analytics 시작
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

이 자습서에서는 TSV(탭 분리 값) 파일을 읽고 CSV(쉼표로 구분된 값) 파일로 변환하는 작업을 개발합니다. 다른를 사용 하 여 동일한 자습서 지원 hello 통해 toogo 도구 hello hello 위에 표시이 섹션의 드롭다운 목록을 사용 하 여 합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure CLI 2.0**. [Azure CLI 설치 및 구성](https://docs.microsoft.com/cli/azure/install-azure-cli)을 참조하세요.

## <a name="log-in-tooazure"></a>TooAzure 로그인

toolog tooyour Azure 구독에서:

```
azurecli
az login
```

요청 된 toobrowse tooa URL 하는 인증 코드를 입력 합니다.  한 다음 자격 증명 hello 지침 tooenter를 따릅니다.

로그인 하면 hello 로그인 명령은 구독을 나열 합니다.

특정 구독 toouse:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>데이터 레이크 분석 계정 만들기
모든 작업을 실행하기 전에 Data Lake Analytics 계정이 있어야 합니다. Data Lake 분석 계정 toocreate hello 다음 항목을 지정 해야 합니다.

* **Azure 리소스 그룹**. Azure 리소스 그룹 내에서 Data Lake Analytics 계정을 만들어야 합니다. [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) toowork hello 리소스 그룹으로 응용 프로그램에 있습니다. 배포 지정, 업데이트 또는 단일, 통합 작업에서 응용 프로그램에 대 한 hello 리소스를 모두 삭제 합니다.  

toolist hello 기존 리소스 그룹이 구독에서:

```
az group list
```

새 리소스 그룹 toocreate:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Data Lake Analytics 계정 이름**. Data Lake Analytics 계정마다 이름이 있습니다.
* **위치** - 데이터 레이크 분석 지원 hello Azure 데이터 센터 중 하나를 사용 합니다.
* **기본 Data Lake Store 계정**: 각 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 있습니다.

toolist hello 기존 데이터 레이크 저장소 계정:

```
az dls account list
```

toocreate 새 Data Lake 저장소 계정:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

다음 구문 toocreate Data Lake 분석 계정 hello를 사용 합니다.

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

계정을 만든 후 명령 toolist hello 계정 다음 hello를 사용 하 여 수 있고 계정 세부 정보 표시 됩니다.

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>업로드 데이터 tooData 레이크 저장소
이 자습서에서는 몇 가지 검색 로그를 처리합니다.  로그를 검색 하는 hello 데이터 레이크 저장소 또는 Azure Blob 저장소에 저장할 수 있습니다.

hello Azure 포털 몇 가지 샘플 데이터 파일 toohello 기본 데이터 레이크 저장소 계정을 검색 로그 파일을 포함 하는 복사 하기 위한 사용자 인터페이스를 제공 합니다. 참조 [원본 데이터를 준비](data-lake-analytics-get-started-portal.md) tooupload hello 데이터 toohello 기본 데이터 레이크 저장소 계정입니다.

CLI 2.0에서 다음 명령을 사용 하 여 hello를 사용 하 여 tooupload 파일:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

데이터 레이크 분석은 Azure Blob 저장소에 액세스할 수도 있습니다.  참조 데이터 tooAzure Blob 저장소에 업로드 [hello를 사용 하 여 Azure 저장소와 Azure CLI](../storage/common/storage-azure-cli.md)합니다.

## <a name="submit-data-lake-analytics-jobs"></a>데이터 레이크 분석 작업 제출
hello Data Lake 분석 작업 U-SQL 언어 hello로 작성 됩니다. U SQL에 대해 자세히 toolearn 참조 [U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md) 및 [U-SQL 언어 eence](http://go.microsoft.com/fwlink/?LinkId=691348)합니다.

**데이터 레이크 분석 작업 스크립트 toocreate**

다음 U-SQL 스크립트를 사용 하면 텍스트 파일을 만들고 hello 텍스트 파일 tooyour 워크스테이션을 저장 합니다.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

이 U-SQL 스크립트 hello 원본 파일 사용 하 여 데이터를 읽고 **Extractors.Tsv()**, 다음을 사용 하 여 csv 파일을 만듭니다 **Outputters.Csv()**합니다.

Hello 소스 파일을 다른 위치에 복사 하지 않으면 hello 두 개의 경로 수정 하지 마십시오.  Data Lake 분석 존재 하지 않는 경우 hello 출력 폴더를 만듭니다.

기본 Data Lake 저장소 계정에 저장 된 파일에 대 한 더 간단한 toouse 상대 경로 절대 경로를 사용할 수도 있습니다.  예:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

연결 된 저장소 계정에 절대 경로 tooaccess 파일을 사용 해야 합니다.  hello 연결 된 Azure 저장소 계정에 저장 된 파일에 대 한 구문은 다음과 같습니다.

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> 공용 Blob이 있는 Azure Blob 컨테이너는 지원되지 않습니다.      
> 공용 컨테이너가 있는 Azure Blob 컨테이너는 지원되지 않습니다.      
>

**toosubmit 작업**

다음 구문 toosubmit 작업 hello를 사용 합니다.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

예:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**toolist 작업 및 작업 세부 정보**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**toocancel 작업**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>작업 결과 검색

작업이 완료 되 면 다음 명령을 toolist hello 출력 파일이 hello를 사용 하 여 수 있고 hello 파일을 다운로드 됩니다.

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

예:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>파이프라인 및 되풀이

**파이프라인 및 되풀이에 대한 정보 가져오기**

사용 하 여 hello `az dla job pipeline` toosee hello 파이프라인 정보에는 이전에 작업 제출 명령을 합니다.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

사용 하 여 hello `az dla job recurrence` toosee hello 되풀이 정보가 이전에 제출 된 작업에 대 한 명령입니다.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>다음 단계

* 데이터 레이크 분석 CLI 2.0 참조 문서 toosee hello 참조 [Data Lake 분석](https://docs.microsoft.com/cli/azure/dla)합니다.
* 데이터 레이크 저장소 CLI 2.0 참조 문서 toosee hello 참조 [데이터 레이크 저장소](https://docs.microsoft.com/cli/azure/dls)합니다.
* toosee 복잡 한 쿼리를 참조 [분석 웹 사이트 Azure 데이터 레이크 분석을 사용 하 여 로그](data-lake-analytics-analyze-weblogs.md)합니다.
