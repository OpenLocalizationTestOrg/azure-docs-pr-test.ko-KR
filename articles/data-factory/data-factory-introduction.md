---
title: "aaaIntroduction tooData 팩터리를 데이터 통합 서비스 | Microsoft Docs"
description: "Azure Data Factory가 무엇인지 알아봅니다. 데이터의 이동과 변환을 조율하고 자동화하는 클라우드 데이터 통합 서비스입니다."
keywords: "데이터 통합, 클라우드 데이터 통합, Azure 데이터 팩터리란"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>소개 tooAzure 데이터 팩터리 
## <a name="what-is-azure-data-factory"></a>Azure 데이터 팩터리란 무엇인가요?
빅 데이터의 hello world에서 어떻게 기존 데이터에에서 사용 될 비즈니스? 온-프레미스 데이터 원본 또는 기타 개별 데이터 원본에서 참조 데이터를 사용 하 여 hello 클라우드에서 생성 가능한 tooenrich 데이터 입니까? 예를 들어, 게임 회사 hello 클라우드에서 게임에서 생성 된 많은 로그를 수집 합니다. 이러한 로그 toogain insights toocustomer 기본 설정, 인구 통계, 사용량 동작에서 원하는 tooanalyze 등 tooidentify 상향 판매 및 교차 판매 기회 새로운 기능 toodrive 비즈니스 성장 강력한 개발 하 고 더 나은 환경을 제공 합니다. toocustomers 합니다. 

tooanalyze hello 회사 이러한 로그는 고객 정보, 게임 정보, 마케팅 캠페인 정보 온-프레미스 데이터 저장소에 있는 같은 toouse hello 참조 데이터를 필요 합니다. 따라서 hello 회사 hello 클라우드 데이터 저장소에서 로그 데이터를 tooingest 및 hello 온-프레미스 데이터 저장소에서 참조 데이터를 원합니다. 그런 다음 hello Hadoop을 사용 하 여 hello 데이터 처리는 클라우드 (Azure HDInsight) 하 고 SQL Server와 같은 Azure SQL 데이터 웨어하우스 또는 온-프레미스 데이터와 같은 클라우드 데이터 웨어하우스로 데이터를 저장 하는 hello 결과 게시 합니다. 브로드캐스트하며이 워크플로 toorun 매주 한 번입니다. 

Hello 회사 toocreate, Hadoop과 같은 기존 계산 서비스를 사용 하 여 온-프레미스와 클라우드 데이터 저장소 모두에서 데이터 및 변환 또는 프로세스 데이터를 수집 하 고 hello 결과 tooan 온-프레미스를 게시할 수 있는 워크플로 수 있는 플랫폼은 필요한 또는 응용 프로그램 tooconsume BI에 대 한 클라우드 데이터 저장소입니다. 

![데이터 팩터리 개요](media/data-factory-introduction/what-is-azure-data-factory.png) 

Azure Data Factory에는 이러한 종류의 시나리오에 대 한 hello 플랫폼입니다. 한 **오케스트레이션 하 고 데이터 변환 및 데이터 이동 자동화에 대 한 hello 클라우드에서 데이터 기반 워크플로 toocreate 수 있는 클라우드 기반 데이터 통합 서비스**합니다. Azure 데이터 팩터리를 사용 하 여 만들 수 있으며 데이터 기반 워크플로 (파이프라인 라고 함), 수 있는 서로 다른 데이터 저장소에서 데이터 수집 프로세스/변환 hello 데이터 Azure HDInsight Hadoop, Spark, Azure 데이터 레이크 등 계산 서비스를 사용 하 여 예약 웹 로그 분석 및 Azure 기계 학습 및 business intelligence (BI) 응용 프로그램 tooconsume에 대 한 Azure SQL 데이터 웨어하우스 등 toodata 데이터를 저장 하는 출력을 게시 합니다.  

기존의 ETL(추출 및 변환 및 로드) 플랫폼이 아닌 EL(추출 및 로드)한 다음 TL(변환 및 로드) 플랫폼이 지지를 얻고 있습니다. 파생 열, 등 데이터를 정렬 하는 행의 수를 계산을 추가 하기 위한 hello 것과 같은 tooperform 변환 되지 않고 hello 변환을 수행 하는 계산 서비스를 사용 하 여 데이터 tootransform/처리 됩니다. 

현재, Azure 데이터 팩터리를 사용 하 고 워크플로 통해 생성 되는 있는 hello 데이터는 **시간 조각화 데이터** (매시간, 매일, 매주 등.). 예를 들어 파이프라인은 하루에 한 번 입력 데이터를 읽고, 데이터를 처리하고 출력 데이터를 생성합니다. 또한 워크플로를 한 번만 실행할 수 있습니다.  
  

## <a name="how-does-it-work"></a>작동 원리 
일반적으로 Azure 데이터 팩터리에서 hello 파이프라인 (데이터 기반 워크플로) hello 세 단계를 수행 합니다.

![Azure Data Factory의 세 단계](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>연결 및 수집
기업에는 다양한 형식의 데이터가 서로 다른 원본에 있습니다. hello 정보 프로덕션 시스템을 작성 하는 첫 번째 단계는 tooconnect tooall hello 필요한 데이터 소스 및 처리, SaaS 서비스와 같은 파일 공유, FTP, 웹 서비스 hello 데이터 필요에 따라 tooa 중앙 위치에 대 한 이동 후속 처리 중입니다.

데이터 팩터리 없이 엔터프라이즈 사용자 지정 데이터 이동을 구성 요소를 만들 하거나 이러한 데이터 원본 및 처리 사용자 지정 서비스 toointegrate를 작성 해야 합니다. 비용이 많이 들고 하드 toointegrate 되 고 이러한 시스템을 유지 관리할 완벽 하 게 관리 되는 서비스를 제공할 수 있는 hello 컨트롤과 hello 엔터프라이즈급 모니터링 및 경고, 종종 부족 합니다.

데이터 팩터리에 온-프레미스에서 데이터 파이프라인 toomove 데이터에 hello 복사 작업을 사용할 수 있으며 클라우드 hello 클라우드 추가 분석을 위해 원본 데이터 저장소 tooa 중앙 집중식 데이터 저장소 키를 누릅니다. 예를 들어 Azure Data Lake 분석 계산 서비스를 사용 하 여 나중에 Azure 데이터 레이크 저장소 및 변환 hello 데이터의 데이터를 수집할 수 있습니다. 또는 Azure HDInsight Hadoop 클러스터를 사용하여 Azure Blob Storage에서 데이터를 수집하고 나중에 변환할 수 있습니다.

### <a name="transform-and-enrich"></a>변환 및 보강
Hello 클라우드에서 중앙 집중식된 데이터 저장소에 있는 데이터를 원하는 hello 수집 된 데이터 toobe 처리 되거나 HDInsight Hadoop, Spark, Data Lake 분석 및 기계 학습 등의 계산 서비스를 사용 하 여 변환 합니다. 신뢰할 수 있는 데이터를 사용 하 여 관리 하 고 제어 된 일정 toofeed 프로덕션 환경에 tooreliably 변환 생성 데이터 사용 하는 것이 좋습니다. 

### <a name="publish"></a>게시 
Tooon 온-프레미스 원본 SQL Server와 같은 hello 클라우드에서 변환 된 데이터를 제공 하거나에 보관 클라우드 사용을 위한 저장소 원본 BI (비즈니스 인텔리전스) 및 분석 도구와 다른 응용 프로그램에서 합니다.

## <a name="key-components"></a>핵심 구성 요소
Azure 구독에는 하나 이상의 Azure Data Factory 인스턴스(또는 데이터 팩터리)가 있을 수 있습니다. Azure Data Factory 단계 toomove 및 변환에 데이터가 있는 데이터 기반 워크플로 작성할 수 있는 tooprovide hello 플랫폼 함께 작동 하는 네 가지 주요 구성 요소가 구성 되어 있습니다. 

### <a name="pipeline"></a>파이프라인
데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인은 활동 그룹입니다. 함께 파이프라인의 hello 활동 작업을 수행 합니다. 예를 들어 파이프라인 Azure blob에서 데이터를 수집 하는 활동 그룹을 포함 하 고는 HDInsight 클러스터 toopartition hello 데이터에서 하이브 쿼리를 실행 수 없습니다. 이 hello 이점은 hello 파이프라인 있습니다 toomanage hello 활동 각각 대신 집합으로 개별적으로입니다. 예를 들어, 배포 및 hello 활동 대신 hello 파이프라인을 독립적으로 예약할 수 있습니다. 

### <a name="activity"></a>작업
파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 활동은 데이터에 대해 작업 tooperform hello를 정의합니다. 예를 들어 하나의 데이터 저장소 tooanother 데이터 저장소에서 복사 작업 toocopy 데이터를 사용할 수 있습니다. 마찬가지로, Azure HDInsight 클러스터 tootransform에서 하이브 쿼리를 실행 하는 하이브 활동을 사용 하 여 또는 데이터를 분석할 수 있습니다. Data Factory는 데이터 이동 활동 및 데이터 변환 활동이라는 두 종류의 활동을 지원합니다.

### <a name="data-movement-activities"></a>데이터 이동 활동
복사 활동 Data Factory에는 원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사합니다. 데이터 팩터리 hello 다음 데이터 저장소를 지원 합니다. 데이터 소스에서 tooany 싱크를 작성할 수 있습니다. 데이터 저장소 toolearn 방법을 클릭 해당 저장소에서 데이터 tooand toocopy 합니다.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 참조하세요.

### <a name="data-transformation-activities"></a>데이터 변환 활동
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

자세한 내용은 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서를 참조하세요.

### <a name="custom-net-activities"></a>사용자 지정 .NET 활동
데이터 저장소에서 복사 작업에 해당 하지 않는 지원, 또는 변환 하는 고유한 논리를 사용 하 여 데이터 만들기/toomove 데이터를 유지 해야 하는 경우는 **사용자 지정.NET 작업**합니다. 사용자 지정 활동을 만들고 사용하는 방법에 대한 자세한 내용은 [Azure Data Factory 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md)을 참조하세요.

### <a name="datasets"></a>데이터 집합
작업은 0개 이상의 데이터 집합을 입력으로 사용하고 하나 이상의 데이터 집합을 출력으로 사용합니다. 데이터 집합 내 단순히 가리키거나 hello에에서 데이터를 toouse 활동 입력 또는 출력으로 참조 하는 hello 데이터 저장소에서 데이터 구조를 나타냅니다. 예를 들어 된 Azure Blob 데이터 집합에서 어떤 hello 파이프라인 hello 데이터 읽어야 하는 hello Azure Blob 저장소에 hello blob 컨테이너 및 폴더를 지정 합니다. 또는 hello 테이블 toowhich hello 출력 데이터가 hello 활동에 의해 기록 되는 Azure SQL 테이블 데이터 집합을 지정 합니다. 

### <a name="linked-services"></a>연결된 서비스
연결 된 서비스 데이터 팩터리의 tooconnect tooexternal 리소스에 대 한 필요한 hello 연결 정보를 정의 하는 연결 문자열 매우 비슷합니다. 이러한 방식으로 생각-hello 연결 toohello 데이터 소스를 정의 하는 연결된 된 서비스 및 데이터 집합 hello hello 데이터 구조를 나타냅니다. 예를 들어 Azure 저장소 연결 된 서비스에는 연결 문자열 tooconnect toohello Azure 저장소 계정을 지정합니다. 고 hello blob 컨테이너 및 hello 폴더 hello 데이터를 포함 하는 Azure Blob 데이터 집합을 지정 합니다.   

연결된 서비스는 데이터 팩터리 내에서 두 가지 용도로 사용됩니다.

* toorepresent는 **데이터 저장소** 등 뿐만 아니라 온-프레미스 SQL Server, Oracle 데이터베이스, 파일 공유 또는 Azure Blob 저장소 계정입니다. Hello 참조 [데이터 이동 작업](#data-movement-activities) 목록은 지원 되는 데이터 저장소 섹션.
* toorepresent는 **계산 리소스** hello는 활동 실행을 호스팅할 수입니다. 예를 들어 hello HDInsightHive 활동 HDInsight Hadoop 클러스터에서 실행 됩니다. 지원되는 컴퓨팅 환경 목록은 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요.

### <a name="relationship-between-data-factory-entities"></a>Data Factory 엔터티 간의 관계
![다이어그램: Data Factory, 클라우드 데이터 통합 서비스 - 주요 개념](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**그림 2.** 데이터 집합, 활동, 파이프라인 및 연결된 서비스 간의 관계

## <a name="supported-regions"></a>지원되는 지역
Hello에서 데이터 팩터리를 만들 수는 현재 **West US**, **미국 동부**, 및 **유럽 북부** 영역입니다. 그러나 데이터 팩터리 데이터 저장소에 액세스할 수 있습니다 및 계산 서비스에서 데이터 저장소 간의 다른 Azure 지역 toomove 데이터 또는 계산 서비스를 사용 하 여 데이터를 처리 합니다.

Azure 데이터 팩터리 자체는 데이터를 저장하지 않습니다. Tooorchestrate 간의 데이터 이동을 데이터 기반 워크플로 만들 수 있습니다 [데이터 저장소를 지원](#data-movement-activities) 및 사용 하 여 데이터의 처리 [계산 서비스](#data-transformation-activities) 온-프레미스 또는 다른 지역 들에 환경입니다. 또한 있습니다 너무[워크플로 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 프로그래밍 방식으로 모두 사용 하 여 및 UI 메커니즘입니다.

데이터 팩터리는에서 사용할 수 있는 경우에 **West US**, **미국 동부**, 및 **유럽 북부** 영역, Data Factory에서 데이터 이동을 hello 전원을 hello 서비스를 사용할 수 [전체적으로](data-factory-data-movement-activities.md#global) 여러 지역에 있습니다. 데이터 저장소는 방화벽 뒤에 있는 경우는 [데이터 관리 게이트웨이](data-factory-move-data-between-onprem-and-cloud.md) 대신 온-프레미스 환경 이동 hello 데이터에 설치 합니다.

예를 들어 Azure HDInsight 클러스터 및 Azure Machine Learning과 같은 계산 환경이 서유럽 지역 외부에서 실행되고 있다고 가정해보겠습니다. 수 및 유럽 북부에 있는 Azure 데이터 팩터리 인스턴스를 사용 하 여 만들고 서 부 유럽에서 하거나 계산 환경에서 tooschedule 작업을 사용 합니다. Data Factory tootrigger hello 작업에 대 한 몇 밀리초 계산 환경에 걸리는 하지만 hello 작업 컴퓨팅 환경에서 실행 하기 위한 hello 시간이 변경 되지 않습니다.

## <a name="get-started-with-creating-a-pipeline"></a>파이프라인 만들기 시작
Azure Data Factory에 이러한 도구 또는 Api toocreate 데이터 파이프라인 중 하나를 사용할 수 있습니다. 

- Azure portal
- Visual Studio
- PowerShell
- .NET API
- REST API
- Azure Resource Manager 템플릿 

toolearn 어떻게 데이터로 toobuild 데이터 팩터리 파이프라인, hello 다음 자습서의에서 단계별 지침을 따르세요.

| 자습서 | 설명 |
| --- | --- |
| [두 클라우드 데이터 저장소 간의 데이터 이동](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |이 자습서에서는 데이터 팩터리 파이프라인 하 만들 **데이터 이동** Blob 저장소 tooSQL 데이터베이스에서 합니다. |
| [Hadoop 클러스터를 사용하여 데이터 변환](data-factory-build-your-first-pipeline.md) |이 자습서에서는 Azure HDInsight(Hadoop) 클러스터에서 Hive 스크립트를 실행하여 **데이터를 처리** 하는 데이터 파이프라인으로 첫 번째 Azure 데이터 팩터리를 구축합니다. |
| [데이터 관리 게이트웨이를 사용하여 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) |이 자습서에서는 데이터 팩터리 빌드할 파이프라인이 있는 **데이터 이동** 에서 **온-프레미스** SQL Server 데이터베이스 tooan Azure blob입니다. Hello 연습의 일부로 설치 하 고 컴퓨터에 hello 데이터 관리 게이트웨이 구성 합니다. |
