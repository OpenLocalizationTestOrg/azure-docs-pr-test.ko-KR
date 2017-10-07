---
title: "데이터 팩터리-aaaAzure 샘플"
description: "Azure 데이터 팩터리 서비스 hello로 제공 되는 예제에 대 한 세부 정보를 제공 합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure 데이터 팩터리 - 샘플
## <a name="samples-on-github"></a>GitHub의 샘플
hello [GitHub Azure DataFactory 리포지토리](https://github.com/azure/azure-datafactory) Azure Data Factory 서비스와 램프 업 수 있는 몇 가지 예제를 신속 하 게 포함 (또는) hello 스크립트를 수정 하 고 자체 응용 프로그램에서 사용 합니다. hello Samples\JSON 폴더에는 일반적인 시나리오에 대 한 JSON 조각을 포함합니다.

| 샘플 | 설명 |
|:--- |:--- |
| [ADF 연습](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |이 예제는 Azure 데이터 팩터리 tooturn 데이터 tooinsights의 로그 파일에서 사용 하 여 로그 파일을 처리 하기 위한 종단 간 연습을 제공 합니다. <br/><br/>이 연습에서는 hello 데이터 팩터리 파이프라인 샘플 로그, 프로세스 및 참조 데이터를 사용 하 여 로그에서 hello 데이터를 강화 모으고 최근에 실행 된 마케팅 캠페인의 hello tooevaluate hello 유효성 및 데이터를 변환 합니다. |
| [JSON 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |이 예제에서는 일반적인 시나리오에 대한 JSON 예제를 제공합니다. |
| [HTTP 데이터 다운로더 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |이 샘플 전시 다운로드 HTTP 끝점 tooAzure Blob 저장소에서에서 데이터의 사용자 지정.NET 작업을 사용 하 여 합니다. |
| [크로스 AppDomain .Net 작업 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |이 샘플을 사용 하지 않은 사용자 지정.NET 작업 제한 hello ADF 시작 관리자 (예를 들어 WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x 등)에서 사용 하는 tooassembly 버전과 tooauthor가 있습니다. |
| [R 스크립트 실행](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |이 샘플에 사용 되는 tooinvoke RScript.exe 일 수 있는 hello Data Factory 사용자 지정 활동에 포함 됩니다. 이 샘플은 R이 이미 설치되어 있는 사용자 고유(주문형 아님) HDInsight 클러스터에만 작동합니다. |
| [HDInsight Hadoop 클러스터에서 Spark 작업 호출](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |이 샘플은 어떻게 toouse MapReduce 작업 tooinvoke Spark 프로그램. 방금 hello spark 프로그램 하나의 Azure Blob 컨테이너 tooanother에서 데이터를 복사합니다. |
| [Azure 기계 학습 배치 평가 작업을 사용한 Twitter 분석](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |이 예제에서는 어떻게 toouse AzureMLBatchScoringActivity tooinvoke Azure 기계 학습 모델을 보여 줍니다. twitter 감성 분석, 점수 매기기, 예측 등을 수행 합니다. |
| [사용자 지정 작업을 사용한 Twitter 분석](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |이 샘플에서는 사용자 지정.NET 작업 tooinvoke 수행 하는 Azure 기계 학습 모델을 toouse twitter 감성 분석, 등 예측 점수 매기기 방법을 보여 줍니다. |
| [Azure 기계 학습에 대한 매개 변수가 있는 파이프라인](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |hello 예제는 종단 간 C# 코드 toodeploy N 파이프라인 점수 매기기 및 재교육 각각 hello 지역 목록이이 샘플에 포함 되어 있는 parameters.txt 파일에서 제공 되는 위치는 다른 지역 매개 변수를 제공 합니다. |
| [Azure 스트림 분석 작업에 대한 참조 데이터 새로 고침](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |이 샘플에서는 참조 데이터는 일정에 대 한 참조 데이터 및 설치 hello로 toouse Azure 데이터 팩터리 및 Azure 스트림 분석 함께 toorun hello 쿼리 새로 고침 하는 방법을 보여 줍니다. |
| [온-프레미스 Hortonworks Hadoop을 사용한 하이브리드 파이프라인](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |hello 샘플 HDInsight Hadoop 클러스터에 클라우드 기반 마찬가지로 다른 계산 대상을 추가 하는 것 처럼 데이터 팩토리에서 작업을 실행 하기 위한 계산 대상으로 온-프레미스 Hadoop 클러스터를 사용 합니다. |
| [JSON 변환 도구](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |이 도구에서는 버전 이전 too2015-07-01-미리 보기 toolatest 또는 2015-07-01-미리 보기 (기본값)에서 Json tooconvert가 있습니다. |
| [U-SQL 샘플 입력 파일](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |U-SQL 작업에서 사용되는 샘플 파일입니다. |
| [Blob 파일 삭제](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | 이 샘플에서는 C# 파일 hello 파일 복사 된 파일의 일부로 ADF 사용자 지정.net 작업 toodelete hello 원본 Azure Blob 위치에서에서 사용할 수 있습니다.|

## <a name="azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿
GitHub의 Azure 리소스 관리자 템플릿을 데이터 팩토리에 대 한 다음 hello를 찾을 수 있습니다.

| 템플릿 | 설명 |
| --- | --- |
| [Azure Blob 저장소 tooAzure SQL 데이터베이스에서 복사](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Hello 데이터 복사 지정 된 Azure blob 저장소 toohello Azure SQL 데이터베이스는 파이프라인을 사용 하 여 Azure 데이터 팩터리를 만듭니다이 서식 파일을 배포 |
| [Salesforce tooAzure Blob 저장소에서 복사](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |이 서식 파일을 배포 hello 데이터 복사 Salesforce 계정 toohello Azure blob 저장소를 지정 하는 파이프라인이 포함 된 Azure 데이터 팩터리를 만듭니다. |
| [Azure HDInsight 클러스터에서 Hive 스크립트를 실행하여 데이터 변환](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |이 서식 파일을 배포 Azure HDInsight Hadoop 클러스터에서 hello 샘플 하이브 스크립트를 실행 하 여 데이터를 변환 하는 파이프라인이 포함 된 Azure 데이터 팩터리를 만듭니다. |

## <a name="samples-in-azure-portal"></a>Azure Portal의 샘플
Hello를 사용할 수 있습니다 **샘플 파이프라인** tooyour 데이터 팩터리에서 데이터 팩터리 toodeploy 샘플 파이프라인 및 해당 관련된 엔터티 (예: 데이터 집합 및 연결 된 서비스)의 hello 홈 페이지에서 타일입니다.

1. 데이터 팩터리를 만들거나 기존 데이터 팩터리를 엽니다. 참조 [Blob 저장소 tooSQL 데이터 팩터리를 사용 하 여 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계 toocreate 데이터 팩터리에 대 한 합니다.
2. Hello에 **DATA FACTORY** 블레이드 hello 데이터 팩토리에 대 한 클릭 hello **샘플 파이프라인** 바둑판식으로 배열입니다.

    ![샘플 파이프라인 타일](./media/data-factory-samples/SamplePipelinesTile.png)
3. Hello에 **샘플 파이프라인** 블레이드에서 hello 클릭 **샘플** toodeploy 되도록 합니다.

    ![샘플 파이프라인 블레이드](./media/data-factory-samples/SampleTile.png)
4. Hello 샘플에 대 한 구성 설정을 지정 합니다. 예를 들어 Azure Storage 계정 이름 및 계정 키, Azure SQL Server 이름, 데이터베이스, 사용자 ID, 암호 등입니다.

    ![샘플 블레이드](./media/data-factory-samples/SampleBlade.png)
5. Hello 구성 설정을 지정 하 여 완료 한 후 클릭 **만들기** 샘플 파이프라인 및 hello 파이프라인에서 사용 되는 연결 된 서비스/테이블 hello toocreate/배포 합니다.
6. 이전 hello 클릭 hello 샘플 타일에서 배포의 hello 상태를 확인할 **샘플 파이프라인** 블레이드입니다.

    ![배포 상태](./media/data-factory-samples/DeploymentStatus.png)
7. Hello 표시 되 면 **배포 성공** hello 타일 hello 샘플을 닫기 hello 메시지 **샘플 파이프라인** 블레이드입니다.  
8. **DATA FACTORY** 블레이드에 표시 연결 된 서비스, 데이터 집합 및 파이프라인 tooyour 데이터 팩터리 추가 됩니다.  

    ![데이터 팩터리 블레이드](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Visual Studio의 샘플
### <a name="prerequisites"></a>필수 조건
Hello 다음이 컴퓨터에 설치 되어 있어야 합니다.

* Visual Studio 2013 또는 Visual Studio 2015
* Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다. 너무 이동[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/) 클릭 **VS 2013** 또는 **VS 2015** hello에 **.NET** 섹션.
* Visual Studio에 대 한 hello 최신 Azure Data Factory 플러그 인을 다운로드: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)합니다. Visual Studio 2013을 사용 하는 경우 업데이트할 수도 있습니다 hello 플러그 인 hello 다음 단계를 수행 하 여: hello 메뉴를 클릭 **도구** -> **확장명 및 업데이트**  ->  **온라인** -> **Visual Studio 갤러리** -> **Visual Studio 용 Microsoft Azure 데이터 팩터리 도구**  ->  **업데이트**합니다.

### <a name="use-data-factory-templates"></a>데이터 팩터리 템플릿 사용
1. 클릭 **파일** 너무 hello 메뉴를 가리키고**새로**를 클릭 하 고 **프로젝트**합니다.
2. Hello에 **새 프로젝트** 대화 상자에서 다음 단계 hello지 않습니다.

   1. **템플릿** 아래의 **데이터 팩터리**를 선택합니다.
   2. 선택 **데이터 팩터리 템플릿** hello 오른쪽 창에서.
   3. 입력 한 **이름** hello 프로젝트에 대 한 합니다.
   4. 선택 된 **위치** hello 프로젝트에 대 한 합니다.
   5. **확인**을 클릭합니다.

      ![새 프로젝트 대화 상자](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. Hello에 **데이터 팩터리 템플릿** 대화 상자, hello에서 샘플 템플릿을 선택 hello **사용 사례 템플릿** 섹션을 클릭 하 여 **다음**합니다. hello 다음 단계에 관한 hello를 사용 하 여 **고객 프로 파일링** 템플릿. 단계는에 대 한 유사 다른 샘플 hello 합니다.

    ![데이터 팩터리 템플릿 대화 상자](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. Hello에 **데이터 팩터리 구성** 대화 상자에서 클릭 **다음** hello에 **데이터 팩터리의 기본** 페이지.
5. Hello에 **구성 데이터 팩터리의** 페이지에서 다음 단계 hello지 않습니다.
   1. **새 데이터 팩터리 만들기**를 선택합니다. **기존 데이터 팩터리 사용**을 선택할 수도 있습니다.
   2. 입력 한 **이름** hello 데이터 팩토리에 대 한 합니다.
   3. 선택 hello **Azure 구독** 하려는 hello 데이터 팩터리 toobe 생성 합니다.
   4. 선택 hello **리소스 그룹** hello 데이터 팩토리에 대 한 합니다.
   5. 선택 hello **West US**, **미국 동부**, 또는 **유럽 북부** hello에 대 한 **지역**합니다.
   6. **다음**을 누릅니다.
6. Hello에 **데이터 저장소 구성** 페이지에서 기존 지정 **Azure SQL 데이터베이스** 및 **Azure 저장소 계정** (또는) 데이터베이스/저장소 키를 만들고 다음을 클릭 합니다.
7. Hello에 **계산 구성** 페이지 기본값을 선택 하 고 클릭 **다음**합니다.
8. Hello에 **요약** 페이지, 모든 설정을 검토 하 고 클릭 **다음**합니다.
9. Hello에 **배포 상태** 페이지 hello 배포 완료 될 때까지 대기 하 고 클릭 **마침**합니다.
10. Hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.
11. 표시 되 면 **tooyour Microsoft 계정 로그인** 대화 상자에서 Azure 구독이 있는 hello 계정에 대 한 자격 증명을 입력 하 고 클릭 **로그인**합니다.
12. 대화 상자를 수행 하는 hello를 표시 되어야 합니다.

    ![게시 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. Hello에 **구성 데이터 팩터리의** 페이지에서 다음 단계 hello지 않습니다.

    1. **기존 데이터 팩터리 사용** 옵션을 확인합니다.
    2. 선택 hello **데이터 팩터리의** hello 서식 파일을 사용 하는 경우 선택 했습니다.
    3. 클릭 **다음** tooswitch toohello **게시 항목** 페이지. (키를 눌러 **탭** hello 이름 필드 tooif hello 부족 toomove **다음** 단추가 비활성화 됩니다.)
14. Hello에 **게시 항목** 페이지에서 엔터티를 선택 하 고 클릭 하 여 데이터 팩터리를 hello 모든 **다음** tooswitch toohello **요약** 페이지.     
15. Hello 요약을 검토 하 고 클릭 **다음** toostart hello 배포 프로세스와 보기 hello **배포 상태**합니다.
16. Hello에 **배포 상태** 페이지 hello 배포 프로세스의 hello 상태 표시 되어야 합니다. Hello 배포를 완료 한 후 마침을 클릭 합니다.

참조 [빌드 (Visual Studio) 첫 번째 데이터 팩터리](data-factory-build-your-first-pipeline-using-vs.md) Visual Studio tooauthor Data Factory 엔터티를 사용 하 고 tooAzure 가격표를 게시 하는 방법에 대 한 세부 정보에 대 한 합니다.          
