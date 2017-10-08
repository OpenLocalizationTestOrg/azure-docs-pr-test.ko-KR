---
title: "데이터 변환: 데이터 처리 및 변환 | Microsoft Docs"
description: "자세한 내용은 방법 tootransform 데이터 나 Hadoop, 기계 학습 또는 Azure 데이터 레이크 분석을 사용 하 여 Azure Data Factory에서 데이터를 처리 합니다."
keywords: "데이터 변환, 데이터 처리, 데이터를 변환, 변환 작업"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Azure Data Factory의 데이터 변환
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md)
> * [기계 학습](data-factory-azure-ml-batch-execution-activity.md) 
> * [저장 프로시저](data-factory-stored-proc-activity.md)
> * [데이터 레이크 분석 U-SQL](data-factory-usql-activity.md)
> * [.NET 사용자 지정](data-factory-use-custom-activities.md)

## <a name="overview"></a>개요
이 문서에서는 tootransform צ ְ ײ 예측 및 통찰력에 원시 데이터를 처리 하는 Azure 데이터 팩터리에서 데이터 변환 작업에 설명 합니다. 변환 작업은 Azure HDInsight 클러스터나 Azure Batch와 같은 컴퓨팅 환경에서 실행됩니다. 링크 tooarticles 각 변환 작업에 대 한 자세한 정보를 제공합니다.

데이터 팩터리의 지원 너무 추가할 수 있는 데이터 변환 작업을 수행 하는 hello[파이프라인](data-factory-create-pipelines.md) 중 하나 개별적으로 다른 작업과 체인입니다.

> [!NOTE]
> 단계별 지침이 포함된 연습은 [Hive 변환으로 파이프라인 만들기](data-factory-build-your-first-pipeline.md) 문서를 참조하세요.  
> 
> 

## <a name="hdinsight-hive-activity"></a>HDInsight Hive 작업
데이터 팩터리 파이프라인에서 HDInsight Hive 활동 hello 하이브 쿼리를 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다. 이 작업에 대한 자세한 내용은 [Hive 작업](data-factory-hive-activity.md) 문서를 참조하세요. 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig 작업
hello 데이터 팩터리 파이프라인에서 HDInsight Pig 작업을 직접 Pig 쿼리 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다. 이 작업에 대한 자세한 내용은 [Pig 작업](data-factory-pig-activity.md) 문서를 참조하세요. 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce 작업
데이터 팩터리 파이프라인에서 HDInsight MapReduce 작업 hello MapReduce 프로그램을 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다. 이 작업에 대한 자세한 내용은 [MapReduce 작업](data-factory-map-reduce.md) 문서를 참조하세요.

## <a name="hdinsight-streaming-activity"></a>HDInsight 스트리밍 작업
데이터 팩터리 파이프라인에서 HDInsight 스트리밍 활동 hello Hadoop 스트리밍 프로그램을 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다. 이 작업에 대한 자세한 내용은 [HDInsight 스트리밍 작업](data-factory-hadoop-streaming-activity.md)을 참조하세요.

## <a name="hdinsight-spark-activity"></a>HDInsight Spark 작업
데이터 팩터리 파이프라인에서 HDInsight Spark 활동 hello 고유한 HDInsight 클러스터에서 Spark 프로그램을 실행합니다. 자세한 내용은 [Azure Data Factory에서 Spark 프로그램 호출](data-factory-spark.md) 을 참조하세요. 

## <a name="machine-learning-activities"></a>Machine Learning 작업
웹 predictive analytics에 대해 서비스에 tooeasily 하면 게시 된 Azure 기계 학습을 사용 하는 파이프라인을 생성 하는 azure Data Factory 수 있습니다. Hello를 사용 하 여 [일괄 처리 실행 작업](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) 는 Azure 데이터 팩터리 파이프라인에서 일괄 처리의 hello 데이터에 대 한 기계 학습 웹 서비스 toomake 예측을 호출할 수 있습니다.

시간이 지남에 따라 hello 예측 모델 hello 점수 매기기 실험 toobe 다시 학습 되도록 new를 사용 하 여 필요한 기계 학습의에서 입력 데이터 집합입니다. 재교육를 완료 한 후 웹 서비스 hello와 점수 매기기 tooupdate hello 기계 학습 모델을 다시 학습 되도록 할 수 있습니다. Hello를 사용할 수 있습니다 [업데이트 리소스 작업](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) hello 새로 학습 된 모델 tooupdate hello 웹 서비스입니다.  

이러한 Machine Learning 작업에 대한 자세한 내용은 [Machine Learning 작업 사용](data-factory-azure-ml-batch-execution-activity.md)을 참조하세요. 

## <a name="stored-procedure-activity"></a>저장 프로시저 작업
데이터 팩터리 파이프라인 tooinvoke hello 데이터 저장소를 다음 중 하나에 있는 저장된 프로시저의에서 hello SQL Server 저장 프로시저 활동을 사용할 수 있습니다: Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, 기업 내에 SQL Server 데이터베이스 또는 Azure VM입니다. 자세한 내용은 [저장 프로시저 작업](data-factory-stored-proc-activity.md)을 참조하세요.  

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL 작업
Data Lake Analytics U-SQL 작업은 Azure Data Lake Analytics 클러스터에 대해 U-SQL 스크립트를 실행합니다. 자세한 내용은 [Data Analytics U-SQL 작업](data-factory-usql-activity.md) 문서를 참조하세요. 

## <a name="net-custom-activity"></a>.NET 사용자 지정 작업
데이터 팩터리에서 지원 되지 않는 방식으로 tootransform 데이터를 유지 해야 하는 경우 고유의 데이터 처리 논리와 사용자 지정 활동을 만들 있고 hello 파이프라인에서 hello 활동을 사용 합니다. Hello 사용자 지정.NET 작업 toorun Azure 배치 서비스 또는 Azure HDInsight 클러스터를 사용 하 여 구성할 수 있습니다. 자세한 내용은 [사용자 지정 작업 사용](data-factory-use-custom-activities.md) 문서를 참조하세요. 

만들 수 있습니다는 사용자 지정 활동 toorun R 스크립트에서 HDInsight 클러스터에 설치 된 R을 사용. [Azure Data Factory를 사용하여 R 스크립트 실행](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)을 참조하세요. 

## <a name="compute-environments"></a>컴퓨팅 환경
Hello 계산 환경에 대 한 연결 된 서비스를 만들고 변환 작업을 정의할 때 연결 된 hello 서비스를 사용 하 여 합니다. 데이터 팩터리에서 지원하는 컴퓨팅 환경은 두 가지 유형이 있습니다. 

1. **주문형**: 데이터 팩터리에서 hello 컴퓨팅 환경을 완전히 관리 되는 경우에 합니다. 자동으로 작업은 전송 된 tooprocess 데이터 전에 hello 데이터 팩터리 서비스에서 만든 및 hello 작업이 완료 될 때 제거 됩니다. 구성 하 고 hello 요청 시 계산 환경에서 작업 실행, 클러스터 관리 및 부트스트래핑 동작의 세부적인 설정을 제어할 수 있습니다. 
2. **자체 환경 사용**: 이 경우 사용자 고유의 컴퓨팅 환경(예: HDInsight 클러스터)을 데이터 팩터리에 연결된 서비스로 등록할 수 있습니다. hello 컴퓨팅 환경을 관리 하 고 데이터 팩터리 서비스 hello tooexecute hello 활동 사용 합니다. 

참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) 에 대 한 문서 toolearn 계산 Data Factory에서 지 원하는 서비스입니다. 

## <a name="summary"></a>요약
Azure Data Factory 지원 데이터 변환 활동이 hello 및 hello hello 활동에 대 한 계산 환경입니다. hello 변환 활동 수 추가 toopipelines 하거나 개별적으로 또는 다른 작업과 연결 합니다.

| 데이터 변환 작업 | 컴퓨팅 환경 |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Machine Learning 작업: 배치 실행 및 업데이트 리소스](data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [저장 프로시저](data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL 데이터 웨어하우스 또는 SQL Server |
| [데이터 레이크 분석 U-SQL](data-factory-usql-activity.md) |Azure 데이터 레이크 분석 |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] 또는 Azure Batch |

