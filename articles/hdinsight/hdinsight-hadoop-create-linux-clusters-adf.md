---
title: "데이터 팩터리-Azure HDInsight를 사용 하는 요청 시 Hadoop 클러스터 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate 주문형 Hadoop 클러스터를 Azure 데이터 팩터리를 사용 하 여 HDInsight에 알아봅니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Azure Data Factory를 사용하여 HDInsight에서 주문형 Hadoop 클러스터 만들기
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Azure Data Factory](../data-factory/data-factory-introduction.md) 는 오케스트레이션 하 고 데이터의 hello 이동 및 변환을 자동화 하는 클라우드 기반 데이터 통합 서비스입니다. HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 분할을 만들 수 있으며 hello 처리가 완료 되 면 hello 클러스터를 삭제. 주문형 HDInsight Hadoop 클러스터를 사용 하 여 hello 혜택은 다음과 같습니다.

- 사용자만 급여 hello 타이머 작업에 대 한 hello 간략 한 구성 가능한 유휴 시간) (더하기 HDInsight Hadoop 클러스터에서 실행 됩니다. HDInsight 클러스터에 대 한 hello 청구는 비례 배분 분당 여부 사용 하 든 합니다. 주문형 HDInsight 연결 된 서비스를 사용 하 여 데이터 팩터리에서 hello 클러스터 요청 시 생성 됩니다. 고 hello 클러스터는 hello 작업이 완료 되 면 자동으로 삭제 됩니다. 따라서 요금만 지불 하기 hello 작업 시간 및 hello 간략 한 유휴 시간 (활성 시간 설정)를 실행 합니다.
- Data Factory 파이프라인을 사용하여 워크플로를 만들 수 있습니다. 예를 들어 hello 파이프라인 toocopy 데이터는 온-프레미스 SQL Server tooan Azure blob 저장소, 주문형 HDInsight Hadoop 클러스터에서 하이브 스크립트와 Pig 스크립트를 실행 하 여 hello 데이터 처리를에서 수도 있습니다. 그런 다음 응용 프로그램 tooconsume BI에 대 한 hello 결과 데이터 tooan Azure SQL 데이터 웨어하우스를 복사 합니다.
- Hello 워크플로 toorun 주기적으로 (시간별, 일별, 주별, 월별, 등)를 예약할 수 있습니다.

Azure Data Factory에서 데이터 팩터리에는 하나 이상의 데이터 파이프라인이 포함될 수 있습니다. 데이터 파이프라인은 하나 이상의 활동을 포함합니다. 두 가지 유형의 활동이 있으며 [데이터 이동 활동](../data-factory/data-factory-data-movement-activities.md) 및 [데이터 변환 활동](../data-factory/data-factory-data-transformation-activities.md)입니다. 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터 이동을 활동 (현재만 복사 작업) toomove 데이터를 사용합니다. 데이터 변환 활동 tootransform/프로세스 데이터를 사용 합니다. HDInsight Hive 활동 데이터 팩터리에서 지원 되는 hello 변환 작업 중 하나입니다. 이 자습서에서는 hello Hive 변환 작업을 사용합니다.

사용자 고유의 HDInsight Hadoop 클러스터 또는 주문형 HDInsight Hadoop 클러스터에 hive 활동 toouse를 구성할 수 있습니다. 이 자습서에서는 hello Hive 작업 hello 데이터 팩터리 파이프라인에서 구성 된 toouse 주문형 HDInsight 클러스터는입니다. 따라서 tooprocess 데이터 조각을 실행 하는 hello 활동을 여기 일이 발생 합니다.

1. HDInsight Hadoop 클러스터 적시에 tooprocess hello 조각에 대 한 자동으로 만들어집니다.  
2. hello 입력된 데이터는 hello 클러스터에 HiveQL 스크립트를 실행 하 여 처리 됩니다.
3. hello HDInsight Hadoop 클러스터 hello 처리가 완료 되 고 hello 클러스터는 시간 (timeToLive 설정) 구성 하는 hello 동안만 유휴 상태 후 삭제 됩니다. 다음 데이터 조각을 hello timeToLive 유휴 시간에 사용 하 여 처리에 사용할 경우 hello 동일한 클러스터 사용 되는 tooprocess hello 조각입니다.  

이 자습서에서는 hello HiveQL 스크립트 hello 하이브 활동과 관련 된 hello 다음 작업을 수행 합니다.

1. 외부 테이블을 참조 hello Azure Blob 저장소에 저장 된 원시 웹 로그 데이터를 만듭니다.
2. 연도 / 월 파티션 hello의 원시 데이터입니다.
3. 저장소 hello hello Azure blob 저장소에서에서 분할 된 데이터입니다.

이 자습서에서는 hello HiveQL 스크립트 hello 하이브 활동과 연결 된 외부 테이블을 참조 hello hello Azure Blob 저장소에에서 저장 된 원시 웹 로그 데이터를 만듭니다. Hello 입력된 파일에 다음 각 월에 대 한 hello 샘플 행은

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

hello HiveQL 스크립트 파티션을 년 및 월 단위로 원시 데이터를 hello 합니다. Hello 이전 입력을 기반으로 세 출력 폴더를 만듭니다. 각 폴더에는 각 월의 항목과 함께 파일이 포함되어 있습니다.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

목록이 추가 tooHive 활동에서 데이터 팩터리 데이터 변환 작업에 대 한 참조 [변환 하 고 Azure 데이터 팩터리를 사용 하 여 분석](../data-factory/data-factory-data-transformation-activities.md)합니다.

> [!NOTE]
> 현재, Azure Data Factory에서 HDInsight 클러스터 버전 3.2 만들기만 할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
이 문서의 지침 hello를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* [Azure 구독](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>저장소 계정 준비
이 시나리오에서 toothree 저장소 계정을 사용할 수 있습니다.

- hello HDInsight 클러스터에 대 한 기본 저장소 계정
- hello 입력된 데이터에 대 한 저장소 계정
- hello에 대 한 저장소 계정 데이터를 출력합니다.

toosimplify hello 자습서에서는 하나의 저장소 계정 tooserve hello 세 가지 목적으로 사용 합니다. 이 섹션에서 제공 하는 hello Azure PowerShell 예제 스크립트는 hello 다음 작업을 수행 합니다.

1. TooAzure에 로그인 합니다.
2. Azure 리소스 그룹 만들기
3. Azure 저장소 계정 만들기
4. Hello 저장소 계정에서 Blob 컨테이너 만들기
5. 다음 두 개의 파일 toohello Blob 컨테이너 hello를 복사 합니다.

   * 입력 데이터 파일: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * HiveQL 스크립트: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     두 파일은 공용 Blob 컨테이너에 저장되어 있습니다.


**tooprepare hello 저장소 파일을 복사할 hello Azure PowerShell을 사용 하 여:**
> [!IMPORTANT]
> Hello Azure 리소스 그룹 및 hello 스크립트에 의해 생성 되는 hello Azure 저장소 계정 이름을 지정 합니다.
> 적어 **리소스 그룹 이름은**, **저장소 계정 이름**, 및 **저장소 계정 키** hello 스크립트에 의해 출력 된 합니다. Hello 다음 섹션에 필요 합니다.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Hello PowerShell 스크립트에서 도움이 필요한 경우 참조 [hello를 사용 하 여 Azure 저장소와 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)합니다. त ु toouse Azure CLI hello 대신 참조 [부록](#appendix) hello Azure CLI 스크립트에 대 한 섹션.

**tooexamine hello 저장소 계정 및 hello 내용**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **리소스 그룹** hello 왼쪽된 창에서.
3. PowerShell 스크립트에서 만든 hello 리소스 그룹 이름이 두 번 클릭 합니다. 나열 된 너무 많은 리소스 그룹이 있는 경우 hello 필터를 사용 합니다.
4. Hello에 **리소스** 타일을 다른 프로젝트와 hello 리소스 그룹을 공유 하지 않는 한 나열 된 리소스가 두 개 있어야 있습니다. 해당 리소스에는 이전에 지정한 hello 이름의 hello 저장소 계정입니다. Hello 저장소 계정 이름을 클릭 합니다.
5. Hello 클릭 **Blob** 타일입니다.
6. Hello 클릭 **adfgetstarted** 컨테이너입니다. **inputdata** 및 **script**라는 두 폴더가 표시됩니다.
7. Hello 폴더를 열고 hello 폴더에 hello 파일을 확인 합니다. hello inputdata 입력된 데이터를 포함 하는 hello input.log 파일 있어서 hello HiveQL 스크립트 파일이 hello 스크립트 폴더에 있습니다.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Resource Manager 템플릿을 사용하여 데이터 팩터리 만들기
Hello 저장소 계정, hello 입력된 데이터 및 hello 준비 HiveQL 스크립트를 준비 toocreate Azure 데이터 팩터리에 됩니다. 데이터 팩터리는 여러 가지 방법으로 만들 수 있습니다. 이 자습서에서는 Azure 포털 hello를 사용 하는 Azure 리소스 관리자 템플릿을 배포 하 여 데이터 팩터리를 만듭니다. 또한 [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) 및 [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)을 사용하여 Resource Manager 템플릿을 배포할 수도 있습니다. 기타 데이터 팩터리 만들기 방법은 [자습서: 첫 번째 데이터 팩터리 빌드](../data-factory/data-factory-build-your-first-pipeline.md)를 참조하세요.

1. Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다. hello 서식 파일은 https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json에 있습니다. Hello 참조 [hello 서식 파일에서 엔터티를 Data Factory](#data-factory-entities-in-the-template) hello 서식 파일에 정의 된 엔터티에 대 한 자세한 내용은 섹션. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. 선택 **기존 항목 사용** hello에 대 한 옵션 **리소스 그룹** 설정과 선택 hello 이름 (PowerShell 스크립트를 사용 하 여) hello 이전 단계에서 만든 hello 리소스 그룹입니다.
3. Hello 데이터 팩토리에 대 한 이름을 입력 하십시오 (**데이터 팩토리 이름이**). 이 이름은 전역적으로 고유해야 합니다.
4. Hello 입력 **저장소 계정 이름** 및 **저장소 계정 키** hello 이전 단계에서 적어 합니다.
5. 선택 **toohello 약관 동의** 읽은 후 위에 언급 된 **약관**합니다.
6. 선택 **Pin toodashboard** 옵션입니다.
6. **구매/만들기**를 클릭합니다. 대시보드를 호출 하는 hello에 타일을 표시 **배포 템플릿 배포**합니다. Hello 될 때까지 기다렸다가 **리소스 그룹** 리소스 그룹에 대 한 블레이드를 엽니다. 이라는 제목으로 사용자 리소스 그룹 이름 tooopen hello 리소스 그룹 블레이드 hello 타일을 클릭할 수도 있습니다.
6. 리소스 그룹 블레이드 hello 아직 열려 있지 않으면 hello 타일 tooopen hello 리소스 그룹을 클릭 합니다. 이제 하나 더 많은 데이터 팩터리 리소스 나열 또한 toohello 저장소 계정 리소스를 표시 해야 합니다.
7. 데이터 팩터리의 hello 이름을 클릭 (hello에 대 한 지정 된 값 **데이터 팩토리 이름이** 매개 변수).
8. Hello Data Factory 블레이드에서 hello 클릭 **다이어그램** 바둑판식으로 배열입니다. hello 다이어그램 입력된 데이터 집합 및는 출력 데이터 집합을 사용 하 여 하나의 동작을 보여 줍니다.

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 다이어그램](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    hello 이름은 hello 리소스 관리자 서식 파일에 정의 됩니다.
9. **AzureBlobOutput**을 두 번 클릭합니다.
10. Hello에 **최근 업데이트 조각**, 한 조각만 표시 되어야 합니다. Hello 상태가 **진행에서**, 너무 변경 될 때까지 기다렸다가**준비**합니다. 에 대 한는 대개 **20 분** toocreate HDInsight 클러스터입니다.

### <a name="check-hello-data-factory-output"></a>Hello 데이터 팩터리 출력 확인

1. 사용 하 여 hello 동일 hello 마지막 세션 toocheck hello 컨테이너에서 hello adfgetstarted 컨테이너의 절차입니다. 없는 두 개의 새 컨테이너 또한 너무**adfgetsarted**:

   * Hello 패턴을 따르는 이름 가진 컨테이너: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`합니다. 이 컨테이너는 hello HDInsight 클러스터에 대 한 hello 기본 컨테이너입니다.
   * adfjobs:이 컨테이너는 hello ADF 작업 로그에 대 한 hello 컨테이너입니다.

     데이터 팩터리 출력이 hello에 저장 됩니다 **afgetstarted** hello 리소스 관리자 서식 파일에서 구성 합니다.
2. **adfgetstarted**를 클릭합니다.
3. **partitioneddata**를 두 번 클릭합니다. 표시는 **연도 2014 =** 폴더 2014 년에 모든 hello 웹 로그 일자 때문에 있습니다.

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 출력](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    드릴 다운 하면 hello 목록, 1 월, 2 월 및 월에 대 한 세 폴더는 표시 됩니다. 각 월에 대한 로그가 있습니다.

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 출력](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Hello 서식 파일에서 데이터 팩터리 엔터티
와 같은 데이터 팩토리에 대 한 최상위 리소스 관리자 템플릿을 hello 표시 되는 모양을 다음과 같습니다.

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>데이터 팩터리 정의
Hello 다음 예제와 같이 hello 리소스 관리자 서식 파일에서 데이터 팩터리를 정의 합니다.  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
hello dataFactoryName은 hello 서식 파일을 배포할 때 지정 하는 hello 데이터 팩터리의 hello 이름입니다. 데이터 팩터리는 현재 hello 미국 동부, 미국 서 부 및 북부 유럽 지역의 에서만 지원 됩니다.

### <a name="defining-entities-within-hello-data-factory"></a>Hello 데이터 팩터리 내에서 엔터티를 정의합니다.
hello 다음과 같은 데이터 팩터리 엔터티 템플릿에 정의 된 hello JSON:

* [Azure 저장소 연결된 서비스](#azure-storage-linked-service)
* [HDInsight 주문형 연결된 서비스](#hdinsight-on-demand-linked-service)
* [Azure Blob 입력 데이터 집합](#azure-blob-input-dataset)
* [Azure Blob 출력 데이터 집합:](#azure-blob-output-dataset)
* [복사 작업을 포함하는 데이터 파이프라인](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
hello Azure 저장소는 Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크를 연결합니다. 이 자습서에서는 hello 동일한 저장소 계정으로 사용 됩니다 hello 기본 HDInsight 저장소 계정, 입력된 데이터 저장 및 출력 데이터 저장소. 따라서 Azure Storage 연결된 서비스 하나만 정의합니다. 연결 된 hello 서비스 정의에 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다. 참조 [Azure 저장소 연결 된 서비스](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
hello **connectionString** 사용 하 여 hello storageAccountName 및 storageAccountKey 매개 변수입니다. Hello 서식 파일을 배포 하는 동안 이러한 매개 변수 값을 지정 합니다.  

#### <a name="hdinsight-on-demand-linked-service"></a>HDInsight 주문형 연결된 서비스
Hello 주문형 HDInsight 연결 되며 서비스 정의 hello Data Factory 서비스 toocreate 런타임 시 HDInsight Hadoop 클러스터에서 사용 되는 구성 매개 변수 값을 지정 합니다. 참조 [계산 연결 된 서비스](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight 주문형 연결 된 서비스 JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 문서입니다.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
포인트 다음 참고 hello:

* hello 데이터 팩터리가 **Linux 기반** HDInsight 클러스터에 있습니다.
* hello HDInsight Hadoop 클러스터를 만든 hello에 동일한 hello 저장소 계정과 지역입니다.
* 공지 hello *timeToLive* 설정 합니다. hello 데이터 팩터리의 hello 클러스터 되 고 유휴 30 분 후 자동으로 hello 클러스터를 삭제 합니다.
* hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**). HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 해야 처리 하지 않으면 기존 라이브 클러스터 toobe 때마다 만드는 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다.

자세한 내용은 [주문형 HDInsight 연결된 서비스](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.

> [!IMPORTANT]
> 많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.

#### <a name="azure-blob-input-dataset"></a>Azure Blob 입력 데이터 집합
Hello 입력된 데이터 집합 정의 있는 blob 컨테이너, 폴더 및 hello 입력된 데이터가 포함 된 파일의 hello 이름을 지정할 수 있습니다. 참조 [Azure Blob 데이터 집합 속성](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

Hello hello JSON 정의에서 특정 설정을 다음 사항을 참고 하십시오.

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Azure Blob 출력 데이터 집합
Hello 출력 데이터 집합 정의 blob 컨테이너 및 hello 출력 데이터를 보유 하는 폴더의 hello 이름을 지정 합니다. 참조 [Azure Blob 데이터 집합 속성](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

hello folderPath hello 출력 데이터를 보유 하는 hello 경로 toohello 폴더를 지정 합니다.

```json
"folderPath": "adfgetstarted/partitioneddata",
```

hello [dataset 가용성](../data-factory/data-factory-create-datasets.md#dataset-availability) 설정을 다음과 같습니다.

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

Azure Data Factory에 출력 데이터 집합 가용성 드라이브 hello 파이프라인입니다. 이 예제에서는 hello 조각이 hello (EndOfInterval) 달의 마지막 날에 월별 생성 됩니다. 자세한 내용은 [데이터 팩터리 예약 및 실행](../data-factory/data-factory-scheduling-and-execution.md)을 참조하세요.

#### <a name="data-pipeline"></a>데이터 파이프라인
주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하여 데이터를 변환하는 파이프라인을 정의합니다. 참조 [파이프라인 JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) JSON 사용 되는 요소 toodefine이이 예제에서 파이프라인에 대 한 설명입니다.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

hello 파이프라인 한 작업, HDInsightHive 활동을 포함합니다. 시작 및 종료 날짜 모두 2016년 1월에 있으므로 한 달에 대한 데이터(조각)만 처리됩니다. 둘 다 *시작* 및 *끝* hello 활동의 없으므로 과거 날짜로 hello Data Factory에서 즉시 hello 월에 대 한 데이터를 처리 합니다. Hello 끝 날짜는 미래의 날짜 이면 hello 데이터 팩터리의 hello 시간이 되 다른 분할 영역을 만듭니다. 자세한 내용은 [데이터 팩터리 예약 및 실행](../data-factory/data-factory-scheduling-and-execution.md)을 참조하세요.

## <a name="clean-up-hello-tutorial"></a>Hello 자습서 정리

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>주문형 HDInsight 클러스터에서 만들어진 hello blob 컨테이너를 삭제 합니다.
주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 toobe 기존 라이브 클러스터 (timeToLive;)이 없는 경우를 처리 해야 때마다 만드는 및 hello 클러스터 hello 처리가 완료 되 면 삭제 됩니다. 각 클러스터에 대 한 Azure Data Factory hello hello 클러스터에 대 한 hello 기본 저장소 계정으로 사용 되는 Azure blob 저장소에서에서 blob 컨테이너를 만듭니다. HDInsight 클러스터를 삭제 하는 경우에 hello 기본 blob 저장소 컨테이너와 연결 된 hello 저장소 계정이 삭제 되지 않습니다. 이 동작은 의도된 것입니다. 많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: `adfyourdatafactoryname-linkedservicename-datetimestamp`합니다.

Hello 삭제 **adfjobs** 및 **adfyourdatafactoryname-linkedservicename-datetimestamp** 폴더입니다. hello adfjobs 컨테이너 Azure Data Factory에서 작업 로그를 포함합니다.

### <a name="delete-hello-resource-group"></a>Hello 리소스 그룹 삭제
[Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 사용된 toodeploy가 관리 하 고 하나의 그룹으로 솔루션을 모니터링 합니다.  리소스 그룹을 삭제 해도 hello 그룹 내의 모든 hello 구성 요소를 삭제 합니다.  

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **리소스 그룹** hello 왼쪽된 창에서.
3. PowerShell 스크립트에서 만든 hello 리소스 그룹 이름을 클릭 합니다. 나열 된 너무 많은 리소스 그룹이 있는 경우 hello 필터를 사용 합니다. Hello 리소스 그룹에는 새 블레이드가 열립니다.
4. Hello에 **리소스** hello 기본 저장소 계정 및 hello 데이터 팩터리 나열 다른 프로젝트와 hello 리소스 그룹을 공유 하지 않는 한 사용할은 타일을 합니다.
5. 클릭 **삭제** hello hello 블레이드 맨 합니다. 이렇게 hello 저장소 계정 및 hello 저장소 계정에 저장 된 hello 데이터를 삭제 합니다.
6. Hello 리소스 그룹 이름 tooconfirm 삭제를 입력 한 다음 클릭 **삭제**합니다.

되지 않도록 toodelete hello 저장소 계정 hello 리소스 그룹을 삭제 하는 경우 hello를 hello 기본 저장소 계정에서 hello 비즈니스 데이터를 분리 하 여 아키텍처를 따르는 것이 좋습니다. 이 경우 hello 비즈니스 데이터로 hello 저장소 계정에 대 한 리소스 그룹에 있고 다른 리소스 그룹 HDInsight 연결 된 서비스 및 hello 데이터 팩토리에 대 한 hello 기본 저장소 계정에 대 한 hello 합니다. Hello 두 번째 리소스 그룹을 삭제 하면 hello 비즈니스 데이터 저장소 계정 영향을 주지 않습니다. toodo 하므로:

* Hello 다음 hello 리소스 관리자 템플릿에 Microsoft.DataFactory/datafactories 리소스와 함께 toohello 최상위 리소스 그룹을 추가 합니다. 저장소 계정을 만듭니다.

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* 새 연결 된 서비스 지점 toohello 새 저장소 계정을 추가 합니다.

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* 추가 dependsOn 및는 additionalLinkedServiceNames 사용 하 여 hello HDInsight 주문형 연결 된 서비스를 구성 합니다.

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 어떻게 toouse Azure Data Factory toocreate 주문형 HDInsight 클러스터 tooprocess 하이브 작업 합니다. 더 많은 tooread:

* [Hadoop 자습서: HDInsight에서 Linux 기반 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)
* [HDInsight 설명서](https://azure.microsoft.com/documentation/services/hdinsight/)
* [데이터 팩터리 설명서](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>부록

### <a name="azure-cli-script"></a>Azure CLI 스크립트
Azure PowerShell toodo hello 자습서를 사용 하는 대신 Azure CLI를 사용할 수 있습니다. 먼저 Azure CLI toouse hello 다음 지침에 따라 Azure CLI를 설치 합니다.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Azure CLI tooprepare hello 저장소를 사용 하 고 hello 파일 복사

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

hello 컨테이너 이름이 *adfgetstarted*합니다. 그대로 유지합니다. 그렇지 않으면 tooupdate hello 리소스 관리자 템플릿이 필요 합니다. 이 CLI 스크립트에서 도움이 필요한 경우 참조 [hello를 사용 하 여 Azure 저장소와 Azure CLI](../storage/common/storage-azure-cli.md)합니다.
