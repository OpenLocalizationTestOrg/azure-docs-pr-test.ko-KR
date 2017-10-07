---
title: "데이터 팩터리 자습서: 첫 번째 데이터 파이프라인 | Microsoft Docs"
description: "이 Azure 데이터 팩터리 자습서 toocreate 및 일정 하이브를 사용 하 여 데이터를 처리 하는 데이터 팩터리 Hadoop 클러스터에서 스크립팅 하는 방법을 보여 줍니다."
services: data-factory
keywords: "Azure 데이터 팩터리 자습서, Hadoop 클러스터, Hadoop Hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>자습서: 빌드 Hadoop 클러스터를 사용 하 여 첫 번째 파이프라인 tootransform 데이터
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-build-your-first-pipeline.md)
> * [Azure 포털](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 템플릿](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

이 자습서에서는 데이터 파이프라인을 사용하여 첫 번째 Azure Data Factory를 빌드합니다. hello 파이프라인은 (Hadoop) Azure HDInsight 클러스터 tooproduce 출력 데이터에서 하이브 스크립트를 실행 하 여 입력된 데이터를 변환 합니다.  

이 문서에서는 개요 및 자습서 hello에 대 한 필수 구성 요소를 제공 합니다. Hello 필수 구성 요소를 완료 한 후 할 수 있는 hello 도구/Sdk를 다음 중 하나를 사용 하 여 hello 자습서: Azure 포털, Visual Studio, PowerShell, REST API 리소스 관리자 템플릿을 합니다. Hello 시작 부분 (또는)에서 링크 hello 드롭 다운 목록에서 다음이 옵션 중 하나를 사용 하 여이 문서 toodo hello 자습서의 hello 끝에 hello 옵션 중 하나를 선택 합니다.    

## <a name="tutorial-overview"></a>자습서 개요
이 자습서의 단계를 수행 하는 hello를 수행할 수 있습니다.

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리는 데이터를 이동 및 변환하는 하나 이상의 데이터 파이프라인을 포함할 수 있습니다. 

    이 자습서에서는 hello data factory에 하나의 파이프라인을 만듭니다. 
2. **파이프라인**을 만듭니다. 파이프라인에는 하나 이상의 활동(예: 복사 활동, HDInsight Hive 활동)이 포함될 수 있습니다. 이 샘플에서는 hello HDInsight Hadoop 클러스터에서 하이브 스크립트를 실행 하는 HDInsight Hive 활동을 사용 합니다. 먼저 hello 스크립트 참조 hello Azure blob 저장소에 저장 된 원시 웹 로그 데이터 표를 만들고 파티션을 년 및 월 단위로 원시 데이터를 hello 다음 합니다.

    이 자습서에서는 hello 파이프라인 Azure HDInsight Hadoop 클러스터에서 하이브 쿼리를 실행 하 여 hello Hive 활동 tootransform 데이터를 사용 합니다. 
3. **연결된 서비스**만들기. 연결 된 서비스 toolink을 데이터 저장소 또는 계산 서비스 toohello 데이터 팩터리를 만듭니다. Azure 저장소와 같은 데이터 저장소 hello 파이프라인의 활동의 입/출력 데이터를 저장합니다. HDInsight Hadoop cluster 클러스터와 같은 계산 서비스는 데이터를 처리/변환합니다.

    이 자습서에는 두 가지 연결된 서비스 **Azure Storage** 및 **Azure HDInsight**를 만듭니다. Azure 저장소 hello hello 입/출력 데이터 toohello 데이터 팩터리를 보유 하는 Azure 저장소 계정 서비스 링크를 연결 합니다. Azure HDInsight 서비스 링크를 사용 하는 tootransform 데이터 toohello 데이터 팩터리 Azure HDInsight 클러스터를 연결 합니다. 
3. 입력 및 출력 **데이터 집합**을 만듭니다. 입력된 데이터 집합 hello 파이프라인의 활동에 대 한 hello 입력을 나타내고 출력 데이터 집합 hello 활동에 대 한 hello 출력을 나타냅니다.

    이 자습서, hello 입력 및 출력에 데이터 집합 입력의 위치를 지정 하 고 출력 데이터에 hello Azure Blob 저장소 키를 누릅니다. hello Azure 저장소 연결 된 서비스를 Azure 저장소 계정 이란 지정 사용 합니다. 입력된 데이터 집합에는 hello 입력된 파일은 출력 데이터 집합 지정 hello 출력 파일을 배치할 위치를 지정 합니다. 


참조 [소개 tooAzure Data Factory](data-factory-introduction.md) Azure Data Factory의 문서에 대 한 자세한 개요입니다.
  
여기에 hello **다이어그램 보기** hello 샘플 데이터 팩터리의이 자습서에서 작성 합니다. **MyFirstPipeline**에는 입력으로 **AzureBlobInput** 데이터 집합을 사용하고 **AzureBlobOutput** 데이터 집합을 출력으로 생성하는 Hive 형식의 한 가지 작업을 포함합니다. 

![데이터 팩터리 자습서에서 다이어그램 보기](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


이 자습서에서는 **inputdata** hello의 폴더 **adfgetstarted** Azure blob 컨테이너 input.log 라는 하나의 파일을 포함 합니다. 이 로그 파일은 2016년 1월, 2월 및 3월 등 세 달에 항목이 있습니다. Hello 입력된 파일에 다음 각 월에 대 한 hello 샘플 행은 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

HDInsight Hive 활동 hello 파이프라인에 의해 hello 파일을 처리 하는 경우 hello 활동 실행 Hive 스크립트 hello HDInsight 클러스터에서 파티션을 년 및 월 단위로 데이터를 입력 합니다. hello 스크립트 각 월의 항목으로 파일을 포함 하는 3 개의 출력 폴더를 만듭니다.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Hello 샘플 선 위에 표시 된에서 hello 먼저 (2016-01-01)으로 작성 된 toohello 000000_0 파일 hello 달에 = 1 폴더입니다. 마찬가지로, hello 두 번째 식 작성 toohello 파일 hello 월 = 2 폴더 및 hello toohello 파일 hello 달에 작성 된 세 번째 = 3 폴더입니다.  

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 다음 필수 구성 요소는 hello가 있어야 합니다.

1. **Azure 구독** - Azure 구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. Hello 참조 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/) 문서 어떻게 무료 평가판 계정을 얻을 수 있습니다.
2. **Azure 저장소** – 범용 표준 Azure 저장소 계정을 사용 하 여이 자습서에서 hello 데이터를 저장 합니다. 범용 표준 Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서. Hello 저장소 계정을 만든 후 응답으로 hello 제공할 **계정 이름** 및 **선택 키**합니다. [저장소 액세스 키 보기, 복사 및 다시 생성](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)을 참조하세요.
3. 다운로드 하 여 hello 하이브 쿼리 파일을 검토 (**hql로 변환**)에 있는: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql)합니다. 이 쿼리는 입력된 데이터 tooproduce 출력 데이터를 변환합니다. 
4. 다운로드 하 여 hello 샘플 입력된 파일을 검토 (**input.log**)에 있는: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Azure Blob Storage에 **adfgetstarted**라는 Blob 컨테이너를 만듭니다. 
6. 업로드 **partitionweblogs.hql** toohello 파일 **스크립트** 폴더 hello에 **adfgetstarted** 컨테이너입니다. [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)와 같은 도구를 사용합니다. 
7. 업로드 **input.log** toohello 파일 **inputdata** 폴더 hello에 **adfgetstarted** 컨테이너입니다. 

Hello 필수 구성 요소를 완료 한 후 hello 도구/Sdk toodo hello 자습서 중 하나를 선택 합니다. 

- [Azure 포털](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Resource Manager 템플릿](data-factory-build-your-first-pipeline-using-arm.md)
- [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Azure Portal 및 Visual Studio는 데이터 팩터리를 빌드하는 GUI 방식을 제공합니다. 반면, PowerShell, Resource Manager 템플릿 및 REST API 옵션은 데이터 팩터리를 빌드하는 스크립팅/프로그래밍 방식을 제공합니다.

> [!NOTE]
> 이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다. 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사 하지 않습니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
> 
> Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요. 





  
