---
title: "Azure HDInsight의 aaaIntroduction tooSpark | Microsoft Docs"
description: "이 문서는 HDInsight의 Spark 클러스터를 사용할 수 있는 HDInsight 및 hello 다른 시나리오에 소개 tooSpark를 제공 합니다."
keywords: "apache spark, spark 클러스터, 소개 toospark 이란 hdinsight의 spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>HDInsight의 tooSpark 소개

이 문서는 소개 tooSpark HDInsight에 제공합니다. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> 빅 데이터 분석 응용 프로그램의 tooboost hello 성능을 처리에서 메모리를 지 원하는 오픈 소스 병렬 처리 프레임 워크입니다. HDInsight의 Spark 클러스터는 Azure Storage(WASB) 및 Azure Data Lake Store와 호환되므로 Azure에 저장된 기존 데이터를 Spark 클러스터를 통해 쉽게 처리할 수 있습니다.

HDInsight의 Spark 클러스터를 만들면 Spark가 설치되고 구성된 Azure 계산 리소스를 만듭니다. HDInsight의 Spark는 toocreate 클러스터는 약 10 분 걸리는. 처리 하는 hello 데이터 toobe Azure 데이터 레이크 저장소 또는 Azure 저장소에 저장 됩니다. [HDInsight에서 Azure Storage 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.

**HDInsight의 Spark는 toocreate 클러스터**, 참조 [퀵 스타트: Jupyter를 사용 하 여 대화형 쿼리를 실행 하 고 HDInsight의 Spark 클러스터를 만듭니다](hdinsight-apache-spark-jupyter-spark-sql.md)합니다.


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Azure HDInsight의 Apache Spark란?
HDInsight의 Spark 클러스터는 완벽하게 관리되는 Spark 서비스를 제공합니다. HDInsight의 Spark 클러스터를 만드는 이점은 다음과 같습니다.

| 기능 | 설명 |
| --- | --- |
| 손쉬운 Spark 클러스터 만들기 |Hello Azure 포털, Azure PowerShell 또는 hello HDInsight.NET SDK를 사용 하 여 분에 HDInsight의 Spark 클러스터를 새를 만들 수 있습니다. [HDInsight에서 Spark 클러스터 시작](hdinsight-apache-spark-jupyter-spark-sql.md) |
| 사용 편의성 |HDInsight의 Spark 클러스터에는 Jupyter 및 Zeppelin 노트북이 포함되어 있습니다. 대화형 데이터 처리 및 시각화에 사용할 수 있습니다.|
| REST API |HDInsight의 Spark 클러스터 포함 [리비](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), REST API 기반 Spark 작업 서버 tooremotely 전송 및 모니터 작업 합니다. |
| Azure Data Lake 저장소에 대한 지원 | HDInsight의 Spark 클러스터에는 추가 저장소는 물론 (3.5 HDInsight 클러스터)에 주 저장소로 구성 된 toouse Azure 데이터 레이크 저장소 될 수 있습니다. Data Lake 저장소에 대한 자세한 내용은 [Azure Data Lake 저장소 개요](../data-lake-store/data-lake-store-overview.md)를 참조하세요. |
| Azure 서비스와의 통합 |HDInsight의 Spark 클러스터 커넥터 tooAzure 이벤트 허브 함께 제공 됩니다. 고객 또한 너무 hello 이벤트 허브를 사용 하는 스트리밍 응용 프로그램을 빌드할 수[Kafka](http://kafka.apache.org/)를 이미 사용 하지 않는 Spark의 일환으로 합니다. |
| R 서버에 대한 지원 | HDInsight Spark 클러스터 toorun hello 속도 약속 Spark 클러스터와 함께 R 계산 배포에서 R 서버를 설정할 수 있습니다. 자세한 내용은 [HDInsight에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요. |
| 타사 IDE와의 통합 | HDInsight은 IntelliJ 아이디어 등 toocreate를 사용할 수 있으며 응용 프로그램 tooan HDInsight Spark 클러스터를 제출 Eclipse Ide에 대 한 플러그 인을 제공 합니다. 자세한 내용은 [IntelliJ IDEA용 Azure 도구 키트 사용](hdinsight-apache-spark-intellij-tool-plugin.md) 및 [Eclipse용 Azure 도구 키트 사용](hdinsight-apache-spark-eclipse-tool-plugin.md)을 참조하세요.|
| 동시 쿼리 |HDInsight의 Spark 클러스터는 동시 쿼리를 지원합니다. 이렇게 하면 한 사용자 또는 다양 한 사용자의 여러 쿼리를 여러 개의 쿼리 및 응용 프로그램 tooshare hello 같은 클러스터 리소스입니다. |
| SSD에서 캐시 |Ssd toohello 클러스터 노드를 연결 하거나 하나를 선택할 수 toocache 데이터 메모리에 있습니다. 메모리에 캐시 hello 최고의 쿼리 성능을 제공 하지만 비용이 많이 드는; 수 Ssd의 캐싱 hello 필요 toocreate 필요한 toofit hello 전체 데이터 집합을 메모리 크기의 클러스터 없이 쿼리 성능 향상을 위한 훌륭한 옵션을 제공 합니다. |
| BI 도구와의 통합 |HDInsight의 Spark 클러스터는 데이터 분석을 위해 [Power BI](http://www.powerbi.com/) 및 [Tableau](http://www.tableau.com/products/desktop)와 같은 BI 도구용 커넥터를 제공합니다. |
| 미리 로드된 Anaconda 라이브러리 |HDInsight에서 Spark 클러스터는 미리 설치된 Anaconda 라이브러리와 함께 제공됩니다. [Anaconda](http://docs.continuum.io/anaconda/) 는 기계 학습, 데이터 분석, 시각화 등 닫기 too200 라이브러리를 제공 합니다. |
| 확장성 |만드는 동안 클러스터의 노드 수가 hello를 지정할 수, 있지만 toogrow 원하는 또는 hello 클러스터 toomatch 작업 축소 수 있습니다. 모든 HDInsight 클러스터 hello 클러스터의 노드 toochange hello 수를 허용합니다. 또한 Spark 클러스터 모든 hello 데이터는 Azure 저장소 서비스 또는 데이터 레이크 저장소에 저장 되므로 데이터의 손실 없이 삭제할 수 있습니다. |
| 24/7 지원 |HDInsight의 Spark 클러스터는 24/7 엔터프라이즈 수준 지원 및 99.9% 가동 시간 SLA와 함께 제공됩니다. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>HDInsight의 Spark에 대 한 hello 사용 사례는 무엇입니까?
HDInsight의 Spark 클러스터 hello 다음 주요 시나리오를 사용 하도록 설정 합니다.

### <a name="interactive-data-analysis-and-bi"></a>대화형 데이터 분석 및 BI
[자습서 살펴보기](hdinsight-apache-spark-use-bi-tools.md)

HDInsight의 Apache Spark는 Azure Storage 또는 Azure Data Lake Store에 데이터를 저장합니다. 비즈니스 전문가 주요 의사 결정권자 분석 및 해당 데이터에 대해 보고서를 작성 하 고 수 hello 분석 데이터에서 Microsoft Power BI toobuild 대화형 보고서를 사용 합니다. 분석가는 클러스터 저장소의 구조화 되지 않은/반 구조화 된 데이터에서 시작 하 고 전자 필기장을 사용 하 여 hello 데이터에 대 한 스키마를 정의 하 고 Microsoft Power BI를 사용 하 여 데이터 모델을 작성할 수 합니다. 또한 HDInsight의 Spark 클러스터는 데이터 분석자, 비즈니스 전문가 및 주요 의사 결정권자를 위한 이상적인 플랫폼을 만드는 Tableau와 같은 여러 타사 BI 도구를 지원합니다.

### <a name="spark-machine-learning"></a>Spark 기계 학습
[자습서 살펴보기: HVAC 데이터를 사용하여 건물 온도 예측](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[자습서 살펴보기: 음식 검사 결과 예측](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark는 [MLlib](http://spark.apache.org/mllib/), 즉 Spark를 기반으로 하여 빌드되어 HDInsight의 Spark 클러스터에서 사용할 수 있는 기계 학습 라이브러리와 함께 제공됩니다. HDInsight의 Spark 클러스터에는 기계 학습을 위한 다양한 패키지가 포함된 Python 배포인 Anaconda도 있습니다. Jupyter 및 Zeppelin 노트북이 기본 제공되는 지원 기능과 결합하고, 기계 학습 응용 프로그램을 만들기 위한 최고의 환경을 제공합니다.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Spark 스트리밍 및 실시간 데이터 분석
[자습서 살펴보기](hdinsight-apache-spark-eventhub-streaming.md)

HDInsight의 Spark 클러스터는 실시간 분석 솔루션을 빌드하기 위한 풍부한 지원을 제공합니다. Spark 커넥터 tooingest 데이터 Kafka, Flume, Twitter, ZeroMQ, 또는 TCP 소켓 같은 여러 소스에서 이미, HDInsight의 Spark에는 Azure 이벤트 허브에서 데이터를 수집 하는 방법에 대 한 첫 번째 클래스 지원을 추가 합니다. 이벤트 허브는 hello azure 큐 서비스에 가장 많이 사용 합니다. Event Hubs에 대한 즉각적인 지원을 통해 HDInsight의 Spark 클러스터는 실시간 분석 파이프라인을 빌드하기 위한 이상적인 플랫폼이 됩니다.

## <a name="next-steps"></a>Spark 클러스터의 일부로 포함된 구성 요소
HDInsight의 Spark 클러스터에는 다음과 같은 구성 요소가 기본적으로 hello 클러스터에서 사용할 수 있는 hello를 포함 됩니다.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Spark Core, Spark SQL, Spark 스트리밍 API, GraphX 및 MLlib가 포함됩니다.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Jupyter Notebook](https://jupyter.org)
* [Zeppelin Notebook](http://zeppelin-project.org/)

HDInsight의 Spark 클러스터 제공는 [ODBC 드라이버](http://go.microsoft.com/fwlink/?LinkId=616229) Microsoft Power BI 및 Tableau와 같은 BI 도구에서 HDInsight의 연결 tooSpark 클러스터에 대 한 합니다.

## <a name="where-do-i-start"></a>시작 단계
HDInsight의 Spark 클러스터를 만드는 것으로 시작합니다. [빠른 시작: HDInsight Linux에서 Spark 클러스터 만들기 및 Jupyter를 사용하여 대화형 쿼리 실행](hdinsight-apache-spark-jupyter-spark-sql.md).을 참조하세요. 

## <a name="next-steps"></a>다음 단계
### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
* [Azure HDInsight의 Apache Spark에 대해 알려진 문제](hdinsight-apache-spark-known-issues.md)
