---
title: "aaaArchived 릴리스 정보-Azure HDInsight의 Hadoop 구성 요소 | Microsoft Docs"
description: "Azure HDInsight용 Hadoop 구성 요소의 이전 버전에 대한 보관 릴리스 정보입니다."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Azure HDInsight에서 Hadoop 구성 요소에 대한 릴리스 정보(보관)

이 문서에서는 hello에 대 한 정보를 제공 **이전** Azure HDInsight 릴리스 업데이트 합니다. 최신 릴리스에 대한 자세한 내용은 [HDInsight 릴리스 정보](hdinsight-release-notes.md)를 참조하세요.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [HDInsight 버전 관리 문서](hdinsight-component-versioning.md)를 참조하세요.



## <a name="notes-for-08302016-release-of-hdinsight"></a>HDInsight의 2016/08/30 릴리스 정보
Linux 기반 HDInsight 클러스터에 대 한 hello 전체 버전 번호가이 릴리스에서 배포 됩니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 | Ambari 빌드 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

이 릴리스에서 hello 전체 버전 번호는 Windows 기반 HDInsight 클러스터를 배포합니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>2016/08/17 - HDInsight에 대한 R Server 릴리스
* R Server 8.0.5 – 주로 버그 수정 릴리스입니다. Hello 참조 [R Server 릴리스 정보](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) 대 한 자세한 정보.
* AzureML 패키지 hello 가장자리 노드에서- [이 R 패키지](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) 사용 하면 R 모델 toobe 게시 및 소비 되는 Azure ML 웹 서비스입니다.  Hello 참조 ["모델을 운용"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) 섹션 우리의 ["개요의 R 서버에 HDInsight"](hdinsight-hadoop-r-server-overview.md) 아티클에 대 한 자세한 정보.
* Hello의 Linux 종속성 [상위 100 가장 인기 있는 R 패키지](https://github.com/metacran/cranlogs) -이러한 Linux 패키지 종속 파일을 미리 설치 되었습니다.
* R을 추가 하는 경우 옵션 toouse hello CRAN 리포지토리 toohello 데이터 노드를 패키징합니다. 자세한 내용은 [“HDInsight에서 R 서버 시작”](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.
* R 서버 클러스터를 만들 때 프로 비전의 안정성 향상 된 hello 합니다.

## <a name="notes-for-08012016-release-of-hdinsight"></a>HDInsight의 2016/08/01 릴리스 정보
Linux 기반 HDInsight 클러스터에 대 한 hello 전체 버전 번호가이 릴리스에서 배포 됩니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 | Ambari 빌드 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

이 릴리스에서 hello 전체 버전 번호는 Windows 기반 HDInsight 클러스터를 배포합니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Spark, Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 변경 내용 tooHDInsight 3.4 클러스터 |성능 향상을 위해 다음과 같은 하이브 구성에 대 한 hello 기본 값이 변경 되 <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |부여 |모두 |해당 없음 |
| 이 릴리스에서 다음 수정 사항이 포함됨 |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |부여 |모두 |해당 없음 |

## <a name="notes-for-07142016-release-of-hdinsight"></a>HDInsight의 2016/07/14 릴리스 정보
Linux 기반 HDInsight 클러스터에 대 한 hello 전체 버전 번호가이 릴리스에서 배포 됩니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 | Ambari 빌드 |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

이 릴리스에서 hello 전체 버전 번호는 Windows 기반 HDInsight 클러스터를 배포합니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>HDInsight의 2016/07/07 릴리스 정보
Linux 기반 HDInsight 클러스터에 대 한 hello 전체 버전 번호가이 릴리스에서 배포 됩니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

이 릴리스에서 hello 전체 버전 번호는 Windows 기반 HDInsight 클러스터를 배포합니다.

| HDI | HDI 클러스터 버전 | HDP | HDP 빌드 |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Spark, Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| [IntelliJ용 HDInsight 도구](hdinsight-apache-spark-intellij-tool-plugin.md) |이제 HDInsight Spark 클러스터용 IntelliJ IDEA 플러그 인은 IntelliJ용 Azure 도구 키트와 통합됩니다. Azure SDK v2.9.1, 최신 Java Sdk를 지원 하며 hello 독립 실행형 IntelliJ 용 HDInsight 플러그 인에서에서 모든 hello 기능이 포함 됩니다. |도구 |Spark |해당 없음 |
| [Eclipse용 HDInsight 도구](hdinsight-apache-spark-eclipse-tool-plugin.md) |Eclipse용 Azure 도구 키트는 이제 HDInsight Spark 클러스터를 지원합니다. 같은 기능 hello 수 있습니다. <ul><li>IntelliSense에 대한 첫 번째 클래스 작성 지원, 자동 서식, 오류 검사 등을 사용하여 Scala 및 Java로 Spark 응용 프로그램을 쉽게 만들고 쓸 수 있습니다.</li><li>Hello Spark 응용 프로그램을 로컬를 테스트 합니다.</li><li>TooHDInsight Spark 클러스터 작업을 제출 하 고 hello 결과 검색 합니다.</li><li>TooAzure를 로그인 하 고 Azure 구독에 연결 된 모든 hello Spark 클러스터에 액세스 합니다.</li><li>HDInsight Spark 클러스터의 모든 연결 된 hello 저장소 리소스를 이동 합니다.</li></ul> |도구 |Spark |해당 없음 |

이 릴리스부터 Linux 기반 HDInsight 클러스터에 대 한 hello 게스트 OS 패치 정책으로 변경 했습니다. hello hello 새 정책의 ´ ֲ ° toosignificantly 재부팅 hello 횟수를 줄이는 due toopatching 합니다. hello 정책 패치에 새 가상 컴퓨터 (Vm) Linux 클러스터를 모든 월요일 또는 목요일 어떤 특정된 클러스터의 노드에서 불규칙적으로 오전 12 시 UTC에서 시작 합니다. 그러나 지정 된 모든 VM에는 최대 30 일 마다 tooguest OS 패치 인해만 다시 부팅합니다. 또한 새로 만들어진된 클러스터에 대 한 첫 번째 다시 부팅 hello hello 클러스터를 만든 날짜 로부터 30 일 보다 자주 발생 하지 않습니다.

> [!NOTE]
> 이러한 변경 내용은이 릴리스 버전 보다 크거나 같은 클러스터를 만든 toonewly를만 적용 됩니다.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>HDInsight의 2016/06/06 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

| HDP | HDI 버전 | Spark 버전 | Ambari 빌드 번호 | HDP 빌드 번호 |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Spark, Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| HDInsight의 Spark가 일반 공급됨 |이 릴리스의 가용성, 확장성 및 생산성 tooopen 소스 HDInsight의 Apache Spark에 향상 된 기능을 제공합니다. <ul><li>까다로운 엔터프라이즈 워크로드에 적합한 99.9%의 업계 최고 가용성 SLA.</li><li>Azure Data Lake Store를 사용하는 확장 가능한 저장소 계층.</li><li>데이터 탐색 및 개발의 모든 단계를 위한 생산성 도구. 사용자 지정된 Spark 커널이 있는 Jupyter Notebook은 대화형 데이터 탐색을 가능하게 하고, Power BI, Tableau 및 Qlik과 같은 BI 대시보드와 통합되어 빠른 데이터 공유 및 지속적인 보고에 적합하며, IntelliJ 플러그 인은 장기적인 코드 아티팩트 개발 및 디버깅을 위한 신뢰할 수 있는 옵션입니다.</li></ul> |부여 |Spark |해당 없음 |
| IntelliJ용 HDInsight 도구 |HDInsight Spark 클러스터용 IntelliJ IDEA 플러그 인입니다. 같은 기능 hello 수 있습니다.<ul><li>IntelliSense에 대한 첫 번째 클래스 작성 지원, 자동 서식, 오류 검사 등을 사용하여 Scala 및 Java로 Spark 응용 프로그램을 쉽게 만들고 쓸 수 있습니다.</li><li>Hello Spark 응용 프로그램을 로컬를 테스트 합니다.</li><li>TooHDInsight Spark 클러스터 작업을 제출 하 고 hello 결과 검색 합니다.</li><li>TooAzure를 로그인 하 고 Azure 구독에 연결 된 모든 hello Spark 클러스터에 액세스 합니다.</li><li>HDInsight Spark 클러스터의 모든 연결 된 hello 저장소 리소스를 이동 합니다.</li><li>모든 hello 작업 기록 및 작업에 대 한 정보 HDInsight Spark 클러스터를 이동 합니다.</li><li>데스크톱 컴퓨터에서 Spark 작업을 원격으로 디버그할 수 있습니다.</li></ul> |도구 |Spark |해당 없음 |

## <a name="notes-for-05132016-release-of-hdinsight"></a>HDInsight의 2016/05/13 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)
* HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)
* HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Spark, Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| Spark 버전 업데이트 및 기타 버그 수정 |이 릴리스에서 HDInsight 클러스터 too1.6.1에 hello Spark 버전을 업데이트 하며 다른 버그 수정 |부여 |Spark |해당 없음 |

## <a name="notes-for-04112016-release-of-hdinsight"></a>HDInsight의 2016/04/11 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)
* HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 -변경되지 않음)
* HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)
* HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)
* HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| HDI 3.4에 대한 사용자 지정 Metastore 업그레이드 문제 |다른 HDInsight 클러스터의 더 낮은 버전에서 이전에 사용한 사용자 지정 Metastore를 사용 하는 경우 클러스터 생성이 실패할 수 있습니다. 이제 수정 된 tooan 업그레이드 하는 스크립트 오류 때문에 이것이 |클러스터 만들기 |모두 |해당 없음 |
| Livy Crash 복구 |Livy를 통해 제출된 모든 작업에 대한 작업 상태 복원력 제공 |안정성 |Linux에서의 Spark |해당 없음 |
| Jupyter 콘텐츠 HA |Hello 기능 toosave 및 부하 Jupyter 노트북 내용을 tooand hello 클러스터와 연결 된 hello 저장소 계정에서 제공 합니다. 자세한 내용은 [Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요. |노트북 |Linux에서의 Spark |해당 없음 |
| Jupyter 노트북에서 hiveContext 제거 |`%%hive` 매직 대신 `%%sql` 매직을 사용합니다. SqlContext 해당 toohiveContext입니다. 자세한 내용은 [Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md) |노트북 |Linux에서 Spark 클러스터 |해당 없음 |
| 이전 Spark 버전의 사용 중단 |이전 버전 1.3.1 Spark hello 서비스 5/31에서 제거 되었습니다. |부여 |Windows에서 Spark 클러스터 |해당 없음 |

## <a name="notes-for-03292016-release-of-hdinsight"></a>HDInsight의 2016/03/29 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 변경되지 않음)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 변경되지 않음)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 변경되지 않음)
* HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 3.4 버전 추가 및 HDP 버전 업데이트됨 |이 릴리스에서 HDInsight v3.4(HDP 2.4에 기반)을 추가하고 다른 HDP 버전도 업데이트했습니다. HDP 2.4 릴리스 정보는 [여기](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)에서 확인할 수 있고 HDInsight 버전에 대한 자세한 정보는 [여기](hdinsight-component-versioning.md)에서 확인할 수 있습니다. |부여 |모든 Linux 클러스터 |해당 없음 |
| HDInsight 프리미엄 |HDInsight는 현재 표준 및 프리미엄이라는 두 가지 범주로 제공됩니다. HDInsight 프리미엄은 현재 Preview 상태이며 Linux에서 Hadoop 및 Spark 클러스터에서만 사용할 수 있습니다. 자세한 내용은 [여기](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)를 참조하세요. |부여 |Linux에서 Hadoop 및 Spark |해당 없음 |
| Microsoft R 서버 |HDInsight 프리미엄은 Linux의 Hadoop 및 Spark 클러스터에 포함할 수 있는 Microsoft R 서버를 제공합니다. 자세한 내용은 [HDInsight에서 R Server 개요](hdinsight-hadoop-r-server-overview.md)를 참조하세요. |부여 |Linux에서 Hadoop 및 Spark |해당 없음 |
| Spark 1.6.0 |HDInsight 3.4 클러스터에 Spark 1.6.0이 포함됨 |부여 |Linux에서 Spark 클러스터 |해당 없음 |
| Jupyter 노트북 기능 향상 |Spark 클러스터와 함께 사용할 수 있는 Jupyter 노트북은 이제 추가 Spark 커널을 제공합니다. 또한 %%magic의 사용, 자동 시각화 및 Python 시각화 라이브러리(예: (matplotlib)와 통합과 같은 향상된 기능도 포함합니다. 자세한 내용은 [Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요. |부여 |Linux에서 Spark 클러스터 |해당 없음 |

## <a name="notes-for-03222016-release-of-hdinsight"></a>HDInsight의 2016/03/22 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - 변경되지 않음)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - 변경되지 않음)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - 변경되지 않음)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 버전 업데이트됨 |이 릴리스에서는 모든 HDInsight 클러스터에 대해 HDInsight 버전을 업데이트함 |부여 |모두 |해당 없음 |

## <a name="notes-for-03102016-release-of-hdinsight"></a>HDInsight의 2016/03/10 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)
* HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - 변경되지 않음)
* HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)
* HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 버전 업데이트됨 |이 릴리스에서는 모든 HDInsight 클러스터에 대해 HDInsight 버전을 업데이트함 |부여 |모두 |해당 없음 |

## <a name="notes-for-01272016-release-of-hdinsight"></a>HDInsight의 2016/01/27 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)
* HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - 변경되지 않음)
* HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)
* HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 버전 업데이트됨 |이 릴리스에서는 모든 HDInsight 클러스터에 대해 HDInsight 버전을 업데이트함 |부여 |모두 |해당 없음 |

## <a name="notes-for-12022015-release-of-hdinsight"></a>HDInsight의 2015/12/02 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - 변경되지 않음)
* HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - 변경되지 않음)
* HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 3.3 버전 추가 및 HDP 버전 업데이트됨 |이 릴리스에서 HDInsight v3.3(HDP 2.3에 기반)을 추가하고 다른 HDP 버전도 업데이트했습니다. HDP 2.3 릴리스 정보는 [여기](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)에서 확인할 수 있고 HDInsight 버전에 대한 자세한 정보는 [여기](hdinsight-component-versioning.md)에서 확인할 수 있습니다. |부여 |모두 |해당 없음 |

## <a name="notes-for-11302015-release-of-hdinsight"></a>HDInsight의 2015/11/30 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터의 업데이트된 HDInsight 버전 및 HDInsight 3.2 클러스터의 HDP 버전(Windows 및 Linux) |이 릴리스에서 HDInsight 및 HDP 버전이 업데이트됨 |부여 |모두 |해당 없음 |

## <a name="notes-for-10272015-release-of-hdinsight"></a>HDInsight의 2015/10/27 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - 변경되지 않음)
* HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 버전 업데이트됨(Windows 및 Linux) |이 릴리스에서 HDInsight 및 HDP 버전이 업데이트됨 |부여 |모두 |해당 없음 |
| 대문자 클러스터를 사용하여 Windows Spark 클러스터에 대한 Jupyter 수정됨 |클러스터 DNS 이름을 대문자로 지정 했던 Jupyter 노트북 tooan 원본 요청 확인 인해 문제가 있었습니다. hello 수정이 Jupyter의 구성 toolower 사례에 대 한 toochange hello DNS 이름입니다. |부여 |HDInsight Spark(Windows) |해당 없음 |

## <a name="notes-for-10202015-release-of-hdinsight"></a>HDInsight 10/20/2015 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.716.1846990(Windows)    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)
* HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)
* HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 기본 버전 변경 tooHDP HDP 2.2 |HDInsight Windows 클러스터에 대 한 hello 기본 버전이 변경 된 tooHDP 2.2입니다. HDInsight 버전 3.2(HDP 2.2)는 2015년 2월 이후 일반에서 사용할 수 있습니다. 이 변경 내용을 대칭 hello Azure 포털, PowerShell cmdlet 또는 hello SDK 사용 하 여 hello 클러스터를 프로 비전 할 때 명시적 선택 항목이 없는 경우에 hello 기본 클러스터 버전을 이동 합니다. |부여 |모두 |해당 없음 |
| 단일 Virtual Network의 Linux 클러스터에서 여러 HDInsight 배포를 위한 VM 이름 형식 변경 |단일 가상 네트워크에서의 여러 HDInsight Linux 클러스터 배포에 대한 지원이 이 릴리스에 추가되었습니다. 헤드 노드에에서 변경 된 hello 클러스터의 가상 컴퓨터 이름의 hello 형식을 업데이트의 일부로\*, workernode\* 및 zookeepernode\* toohn\*, wn\*, 및 zk\* 각각. 때문에이 주제 toochange 권장된 방식 tootake hello 가상 컴퓨터 이름 형식에 대 한 직접 종속성 않습니다. Hello 로컬 컴퓨터 또는 호스트 및 구성 요소 toohosts의 hello 매핑을 Ambari Api toodetermine hello 목록에서 "호스트 이름-f"를 사용 합니다. 자세한 내용은 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) 및 [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md)에서 확인할 수 있습니다. |부여 |Linux 기반 HDInsight 클러스터 |해당 없음 |
| 구성 변경 내용 |3.1 HDInsight 클러스터에 대 한 구성을 따르고 hello은 이제 사용할 수 있습니다. <ul><li>tez.yarn.ats.enabled 및yarn.log.server.url 구성을 사용할 수 있습니다. 이 통해 응용 프로그램 타임 라인 서버 hello 및 hello 로그 서버 toobe 수 tooserve 로그 아웃 합니다.</li></ul>3.2 HDInsight 클러스터에 대 한 구성을 따르고 hello 수정 되었습니다. <ul><li>mapreduce.fileoutputcommitter.algorithm.version too2를 설정 되었습니다. 이 hello V2 버전의 hello FileOutputCommitter 사용할 수 있습니다.</li></ul> |부여 |모두 |해당 없음 |

## <a name="notes-for-09092015-release-of-hdinsight"></a>HDInsight의 2015/09/09 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.675.1768697(HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.675.1768697(HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.675.1768697(HDP 2.1.15.0-2334 - 변경되지 않음)
* HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - 변경되지 않음)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 버전 업데이트됨 |이 릴리스에서 HDInsight 버전이 업데이트됨 |부여 |모두 |해당 없음 |

## <a name="notes-for-07312015-release-of-hdinsight"></a>HDInsight의 2015/07/31 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.640.1695824(HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.640.1695824(HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.640.1695824(HDP 2.1.15.0-2334 - 변경되지 않음)
* HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - 변경되지 않음)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| Spark 클러스터 노드 다시 이미징 워크플로 수정 |일으킨 Spark toonot 이미지로 다시 설치 후 복구 하는 클러스터 노드에 있는 버그를 수정 |부여 |Spark |해당 없음 |

## <a name="notes-for-07312015-release-of-hdinsight"></a>HDInsight의 2015/07/31 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.635.1684502(HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.635.1684502(HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.635.1684502(HDP 2.1.15.0-2334 - 변경되지 않음)
* HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - 변경되지 않음)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| 모든 HDInsight 클러스터에 대해 HDInsight 버전 업데이트됨 |이 릴리스에서 HDInsight 버전이 업데이트됨 |부여 |모두 |해당 없음 |

## <a name="notes-for-07072015-release-of-hdinsight"></a>HDInsight의 2015/07/07 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - 변경되지 않음)
* HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

| 제목 | 설명 | 영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK) | 클러스터 유형(예: Hadoop, HBase 또는 Storm) | JIRA(적용 가능한 경우) |
| --- | --- | --- | --- | --- |
| HDInsight 3.2 클러스터에 대한 업데이트된 HDP 버전 |이 릴리스에서는 HDInsight 3.2가 HDP 2.2.6.1-0012를 배포함 |부여 |모두 |해당 없음 |

## <a name="notes-for-06262015-release-of-hdinsight"></a>HDInsight의 2015/06/26 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - 변경되지 않음)
* HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>HDInsight 3.2 클러스터에 대한 업데이트된 HDP 버전</td>
<td>이 릴리스에서는 HDInsight 3.2가 HDP 2.2.6.1을 배포함</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>HDInsight의 2015/06/18 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)
* HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>열린 추가 HTTPS 포트</td>
<td>hello 클라우드 서비스에는 이제 hello 클러스터 예를 들어 5 포트 8001 too8005를 열립니다. https://<clustername>.azurehdinsight.net:8001/). 동일한 toothese Url은 사용 하 여 인증 된 요청 hello 포트 443으로 기본 인증 암호 메커니즘입니다. 이러한 포트는 toohello hello 활성 헤드 노드에 동일한 포트를 바인딩합니다. 스크립트 동작 hello 헤드 노드 및 경로 toooutside hello 클러스터에서 이러한 포트에서 사용 되는 toomake 고객 서비스 수신 될 수 있습니다.</td>
<td>클라우드 서비스</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HDInsight 3.2에 대한 일시적인 MapReduce shuffle 문제</td>
<td>대형 클러스터의 Map Reduce Shuffle에서 드문 일시적인 경합 상태에 대한 수정으로 간혹 작업이 실패할 수 있습니다. 자세한 내용은 <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a>을 참조하세요.</td>
<td>Hadoop 코어</td>
<td>모두</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>HDInsight 3.2에 대 한 Azure Java SDK 2.2 tooLatest 이동</td>
<td>Toolatest 버전의 Azure SDK for Java hello WASB 드라이버에서 사용 하는 hello 이동 합니다. hello 최신 SDK 몇 가지 수정 있고 hello에 대 한 hello 릴리스 정보 동일 https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt에서 사용할 수 있습니다.</td>
<td>Hadoop 코어</td>
<td>모두</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>3.1 HDInsight 클러스터에 대 한 2.1.15 tooHDP 이동</td>
<td>Hortonworks hello 릴리스의 릴리스 정보는 사용할 수 있는 <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">여기</a>합니다.</td>
<td>HDP</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>HDInsight의 2015/06/04 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - 변경되지 않음)
* HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>스톰 클러스터에 대한 502 잘못된 게이트웨이 오류에 대한 수정</td>
<td>이 릴리스에서 hello 작업 전송 API를 발생 시킨 hello 웹 사이트 toobe 아래로 다시 부팅 한 후에 영향을 미치는 버그를 수정 합니다.</td>
<td>부여</td>
<td>Storm</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>HDInsight의 2015/06/01 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - 변경되지 않음)
* HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - 변경되지 않음)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>다양한 버그 수정</td>
<td>이 릴리스의 버그를 수정 관련 toocluster 프로 비전 합니다.</td>
<td>부여</td>
<td>모든 클러스터 형식</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>HDInsight의 2015/05/27 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)
* 다른 클러스터 버전 및 SDK은 이 릴리스의 일부분으로 배포되지 않습니다.

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>HDP 2.2 업데이트</td>
<td>이 버전의 HDInsight 3.2 HDP 2.2.6, 포함 되며 몇 가지 중요 한 버그 수정 tooHDInsight 옵니다. hello 전체 릴리스 정보는에서 사용할 수 있는 <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 릴리스 정보</a>합니다.</td>
<td>HDP</td>
<td>모든 클러스터 형식</td>
<td>해당 없음</td>
</tr>
<tr>
<td>TooDefault Yarn 컨테이너 메모리 구성 변경</td>
<td>이 업데이트에 (yarn.nodemanager.resource.memory mb 및 yarn.scheduler.maximum 할당 100mb) hello 기본 사용 가능한 메모리 tooYARN 컨테이너 노드 관리자가 시작, too5632MB 증가 됩니다. 이전에이 감소 too4608MB 했지만 다양 한 작업 실행에 따라, 새 값 hello 제공 해야 더 나은 안정성과 성능을 toomost 작업, 따라서 더 나은 기본값입니다. 일반적으로 중요 한 종속성이 메모리 구성에 있으면이 설정 명시적으로 hello 클러스터를 만드는 동안 합니다.</td>
<td>HDP</td>
<td>모든 클러스터 형식</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HBase 및 스톰 클러스터에 대한 기본 구성 패리티</td>
<td>이 업데이트 복원 Hbase 클러스터와 Storm 클러스터 toouse hello Hadoop 클러스터의 YARN configs 같은 값입니다. 모든 클러스터 형식에서 패리티에 대해 수행됩니다.</td>
<td>HDP</td>
<td>HBase, Storm</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>HDInsight의 2015/05/20 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)
* HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>SCP.NET 이벤트 허브 지원</td>
<td>HDInsight 스톰에 대 한 업데이트 hello 클러스터 패키지에 새 기능 tooSCP.NET 상태로 전환합니다. 이제 보다 쉽게 toouse EventHubSpout 또는 Java Spouts 하는 토폴로지 작성기에 대 한 Api 액세스 toonew를 준비 되었습니다. Hello 계약 업데이트 되었습니다. 프로그램 SCP.NET 클라이언트 SDK toowork 새 클러스터로 업데이트 해야 합니다. Hello에 대 한 자세한 내용은 새로운 Api, 사용법 및 릴리스 정보 (버그 수정 포함) toohello hello SCP.NET NuGet 패키지에에서 포함 된 추가 정보를 참조 하십시오.</td>
<td>VS 도구</td>
<td>Storm HDInsight 3.2 클러스터</td>
<td>해당 없음</td>
</tr>
<tr>
<td>JDBC 드라이버 업데이트</td>
<td>업데이트 된 hello 드라이버 toohello SQL Server sqljdbc_4.1.5605.100에서 버전을 지원 합니다.</td>
<td>메타 저장소</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>HDInsight의 2015/04/27 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - 변경되지 않음)
* HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)
* SDK            1.5.8

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>DLL 종속성 수정</td>
<td>단위 테스트 프레임워크에 대한 HDInsight 종속성을 제거합니다.</td>
<td>SDK)</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>경합 상태에 대한 버그 수정</td>
<td>클러스터는 PUT에 대 한 대기 요청 hello 상태를 폴링하기 전에 수락 toobe 이제 요청 만들기</td>
<td>SDK)</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>HDInsight의 2015/04/14 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 변경되지 않음)
* HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)
* SDK            1.5.6

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>Tez 버그 수정</td>
<td>Apache TEZ 2214 및 TEZ 1923에 대한 수정 프로그램이 이 릴리스의 HDI 3.2에 포함되어 있습니다. 에 대 한 특정 하이브 쿼리 Tez tooshuffle 상당한 양의 데이터를 요구 필요 합니다.
</td>
<td>HDP</td>
<td>Hadoop은</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>HDInsight의 2015/04/06 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - 변경되지 않음)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - 변경되지 않음)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - 변경되지 않음)
* HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)
* SDK            1.5.6

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>HDInsight .NET SDK 1.5.6</td>
<td>Linux에서 HDInsight를 tooremove 일부 내부 클래스를 업데이트합니다.</td>
<td>SDK)</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>Avro Library 1.5.6</td>
<td><b>GetAllKnownTypes</b> 메서드에 대한 <b>KnownTypeAttribute</b>가 추가되었습니다. GetAllKnownTypes 메서드에 대해 형식이 null인 경우의 NullReferenceException이 수정되었습니다.</td>
<td>SDK)</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>버그 수정</td>
<td>다양 한 버그 수정 toohello 서비스</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>HDInsight의 2015/04/01 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)
* HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)
* HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)
* HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)
* SDK            1.5.5

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>기능 tooenable/사용 안 함 원격 데스크톱 자격 증명.NET SDK를 통해 Windows 클러스터에서</td>
<td>Windows 클러스터에서 RDP 자격 증명을 사용하도록/사용하지 않도록 설정하는 기능을 프로그래밍 방식으로 지원합니다.</td>
<td>SDK)</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>기능 tooenable 원격 데스크톱 자격 증명에 클러스터 되 고 프로 비전 된 동안</td>
<td>Hello 클러스터를 만드는 중으로 원격 데스크톱 자격 증명을 사용 하기 위한 프로그래밍 방식의 지원 합니다. 다음 원격 데스크톱을 사용 하도록 설정 하 고 프로 비전 하는 첫 번째 hello 클러스터 hello 2 단계 프로세스를 제거 합니다.</td>
<td>SDK)</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>업그레이드 된 Python too2.7.8</td>
<td>HDInsight 버전 2.1, 3.0, 3.1 및 3.2에 대 한 몇 가지 중요 한 보안을 포함 하는 HDInsight 클러스터 tooPython 2.7.8에서 업그레이드 된 Python 수정</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>YARN 구성 변경</td>
<td>변경 된 YARN 구성 yarn.resourcemanager.max-완료-응용 프로그램 HDInsight 버전 3.1 및 3.2에 대 한 모든 클러스터 유형에 too1000 합니다. 이 값만 hello 목록이 hello YARN UI에서에서 완성 된 응용 프로그램을 제어합니다. 실행 된 응용 프로그램에 대 한 tooget 정보 이전 toohello 목록이 toohello 기록 서버를 직접 이동할 수 있습니다 hello UI에 표시 된 응용 프로그램을 제출 합니다.</td>
<td>YARN</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HBase 클러스터의 노드 크기 조정</td>
<td>이제 HBase 클러스터에서 HDInsight 버전 3.1 및 3.2에 대한 노드 크기를 조정(확장 및 축소)할 수 있습니다.</td>
<td>부여</td>
<td>HBase</td>
<td>해당 없음</td>
</tr>
<tr>
<td>JDBC 업그레이드</td>
<td>JDBC SQL 드라이버는 HDInsight 버전 3.2에 대 한 업그레이드 tooversion sqljdbc_4.0.2206.100입니다. 이 버전에는 중요한 보안 향상 기능이 포함되어 있습니다.</td>
<td>HDP</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>JVM 구성 업데이트</td>
<td>업데이트 된 JVM 구성 networkaddress.cache.ttl too300 초 hello 기본값인-1에서 HDInsight 버전 3.1 및 3.2에 대 한 합니다. 이 구성 값 hello 캐싱 hello 이름 서비스에서 성공적인 이름 조회에 대 한 정책을 제어 합니다. 이 버그 수정 관련 toogrowing 및 HBase 클러스터를 축소 합니다.</td>
<td>부여</td>
<td>HBase</td>
<td>해당 없음</td>
</tr>
<tr>
<td>저장소 SDK 2.0에 tooAzure 업그레이드</td>
<td>HDInsight 버전 3.2는 업그레이드 된 toouse hello hello Java 용 Azure 저장소 SDK의 최신 버전입니다. 이 현재 0.6.0 hello 버전에 비해 몇 가지 중요 한 버그 수정 포함합니다.</td>
<td>HDP</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>업그레이드 된 tooApache WASB 소스 코드</td>
<td>HDInsight 버전 3.2 사용 하 여 hello hello WASB Apache Hadoop의 드라이버를 파일 시스템에 대 한 최신 코드 이제 합니다. 이러한 변경으로 인해 hello WASB 드라이버는 이제 별도 jar로 패키지 됩니다. 패키징 변경 순수 하 게 이므로 hello WASB 드라이버의 모든 변경 내용을 toobehavior 포함 되어 있지 않습니다. hello이 JAR 파일의 이름이 hadoop-azure-2.6.0.jar 합니다.</td>
<td>HDP</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HDInsight 3.2에서 Jar 파일 이름 업데이트</td>
<td>이 업데이트 tooHDInsight 버전 3.2 몇 가지 버그 수정이 포함 하 고 몇 가지 내부 jar HDP의 일부로 패키지를 업그레이드 합니다. 이러한 JAR filesare 내부 toohello HDP 패키지 및 사용자 지정 응용 프로그램에서 직접 사용 되지 않습니다. 응용 프로그램 내부 HDP 단지 업그레이드 toohello는 사용자 지정 응용 프로그램 해제 되지 않도록 있도록 hello Jar의 고유 버전을 패키지 해야 합니다.</td>
<td>HDP</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>HDInsight의 2015/03/03 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - 변경되지 않음)
* HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 -  변경되지 않음)
* HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - 변경되지 않음)
* HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - 변경되지 않음)
* SDK            1.5.0                (변경되지 않음)

이 릴리스에서 업데이트 이후에 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>안정성 향상</td>
<td>Hello 서비스 tooscale hello 증가 한 부하를 존중 toocluster 만드는 강력해졌습니다 허용 하는 수정 프로그램이 만들었습니다.</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>HDInsight의 2015/02/18 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - 변경되지 않음)
* HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 -  변경되지 않음)
* HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - 변경되지 않음)
* HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)
* SDK            1.5.0

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>HDInsight 3.2 클러스터</td>
<td>Hadoop 2.6/HDP2.2는 HDInsight 3.2 클러스터에서 사용할 수 있습니다. 주요 업데이트 tooall hello 오픈 소스 구성 요소를 포함합니다. 자세한 내용은 HDInsight의 새로운 기능 및 <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">HDP 2.2.0.0 릴리스 정보</a>를 참조하세요.</td>
<td>오픈 소스 소프트웨어</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>Linux에서의 HDInsight(미리 보기)</td>
<td>Ubuntu Linux에서 실행되는 클러스터를 배포할 수 있습니다. 자세한 내용은 Linux에서 HDInsight 시작을 참조하세요.</td>
<td>부여</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>Storm 일반 공급</td>
<td>Apache Storm 클러스터가 일반 공급됩니다. 자세한 내용은 HDInsight에서 Storm 사용 시작을 참조하세요.</td>
<td>부여</td>
<td>Storm</td>
<td>해당 없음</td>
</tr>
<tr>
<td>가상 컴퓨터 크기</td>
<td>더 다양한 가상 컴퓨터 유형 및 크기에서 Azure HDInsight를 사용할 수 있습니다. HDInsight; 같은 일반적인 목적 용으로 작성 된 A2 tooA7 크기를 활용할 수 있습니다. 관련 기능을 Ssd (반도체 드라이브)와 60% 빠른 프로세서; D 시리즈 노드 고 InfiniBand 있는 A8 및 A9 크기 빠른 네트워킹에 대 한 지원 합니다.</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>클러스터 크기 조정</td>
<td>Toodelete 필요 없이 hello 실행 중인 HDInsight 클러스터에 대 한 데이터 노드 수를 변경 하거나 다시 만들 수 있습니다. 현재, Hadoop 쿼리 및 Apache Storm 클러스터 형식만 이러한 기능을가지고 있지만 곧 Apache HBase 클러스터 유형 toofollow에 대 한 지원은. 자세한 내용은 Ambari를 사용하여 HDInsight 관리를 참조하세요.</td>
<td>부여</td>
<td>Hadoop, Storm</td>
<td>해당 없음</td>
</tr>
<tr>
<td>Visual Studio 도구</td>
<td>또한 toocomplete tooling Apache Storm, Visual Studio에서 Apache Hive에 대 한 tooling hello에 대 한 업데이트 된 tooinclude 문 완성, 로컬 유효성 검사 및 디버깅 지원 개선된 되었습니다. 자세한 내용은 Visual Studio용 HDInsight Hadoop 도구 시작을 참조하세요.</td>
<td>도구</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<td>Azure Cosmos DB용 Hadoop 커넥터</td>
<td>Azure Cosmos DB용 Hadoop 커넥터를 사용하면 여러 Azure Cosmos DB 컬렉션 또는 데이터베이스 계정에 걸쳐 저장된 스키마 없는 JSON 문서에 대해 복잡한 집계, 분석 및 조작을 수행할 수 있습니다. 자세한 내용 및 자습서는 Azure Cosmos DB 및 HDInsight를 사용하여 Hadoop 작업 실행을 참조하세요.</td>
<td>부여</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>버그 수정</td>
<td>HDInsight 서비스에 대한 여러 가지 사소한 버그가 수정되었습니다. 고객이 수행해야 하는 동작 변경은 없습니다.</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>HDInsight의 2015/02/06 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - 변경되지 않음)
* HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 -  변경되지 않음)
* HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)
* SDK            N/A

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>버그 수정</td>
<td>HDInsight 서비스에 대한 여러 가지 사소한 버그가 수정되었습니다. 고객이 수행해야 하는 동작 변경은 없습니다.</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HDP 2.1 유지 관리 업데이트</td>
<td>HDInsight 3.1은 업데이트 된 toodeploy HDP 2.1.10.0입니다. 자세한 내용은 <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">HDP-2.1.10 릴리스 정보</a>를 참조하세요. </td>
<td>오픈 소스 소프트웨어</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HDP 이진 업데이트</td>
<td>HBase의 JAR 파일 중 일부의 파일 이름이 업데이트되었습니다. 이러한 JAR 파일 않아야 고객 한지 hello 이러한 JAR 파일 이름에 종속 되므로 HBase에서 내부적으로 사용 됩니다. 내용은 다음과 같습니다.
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>오픈 소스 소프트웨어</td>
<td>HBase</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>HDInsight의 2015/1/29 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - 변경되지 않음)
* HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 -  변경되지 않음)
* HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 -  변경되지 않음)
* SDK            N/A

이 릴리스에서 업데이트 이후에 hello를 포함 되어 있습니다.

<table border="1">

<tr>
<th>제목</th>
<th>설명</th>
<th>영향을 받는 영역(예: 서비스, 구성 요소 또는 SDK)</p></th>
<th>클러스터 유형(예: Hadoop, HBase 또는 Storm)</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>버그 수정</td>
<td>기능이 Azure 업그레이드 하는 동안 hello HDInsight 클러스터의 hello 안정성을 개선 하는 몇 가지 중요 한 버그 수정 되었습니다.</td>
<td>부여</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>HDInsight의 2015/1/5 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호:

* HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - 변경되지 않음)
* HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - 변경되지 않음)
* HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - 변경되지 않음)

이 릴리스에서 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">

<tr>
<th>제목</th>
<th>설명</th>
<th>구성 요소</th>
<th>클러스터 유형</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>Twitter 추세 분석 및 Mahout 기반 동영상 권장 사항 샘플</td>
<td><p>이 릴리스에서 hello HDInsight 쿼리 콘솔에는 두 개의 추가 샘플에 있습니다.</p>

<p><b>Twitter 추세 분석</b><br>
Twitter와 같은 사이트에서 제공하는 공개 API는 대중적인 추세를 분석하고 이해하는 데 유용한 데이터 원본입니다. 이 자습서에서는 어떻게 toouse 하이브 tooget hello 특정 단어를 포함 하는 대부분 트 윗을 보낼 Twitter 사용자 목록에 알아봅니다. </p>

<p><b>Mahout 동영상 권장 사항</b><br>
Apache Mahout는 Apache Hadoop 기계 학습 라이브러리입니다. Mahout에는 필터링, 분류 및 클러스터링과 같은 데이터 처리를 위한 알고리즘이 포함됩니다. 이 자습서에서는 친구에 알아보았습니다 동영상에 따라 권장 엔진 toogenerate 영화 권장 합니다.</p></td>
<td>쿼리 콘솔</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>하이브 구성에 대 한 toodefault 값 변경: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>이 크기 구성 변환 tooautomatically 지도 조인을 적용 됩니다. hello 값 너무 커서 메모리에 변환 된 toohash 지도 일 수 있는 테이블의 hello 크기의 합계를 hello를 나타냅니다. 이전 릴리스에서이 값은 MB too128 10MB의 기본값 hello에서에서 증가 합니다. 그러나 128MB의 새 값 hello 작업 toofail 일으켰던 메모리 due toolack 합니다. 이 릴리스에서 되돌립니다 hello 기본값 too10 MB를 백업 합니다. 고객이 선택할 수 toooverride이 값이 클러스터를 만드는 동안 해당 쿼리 및 테이블 크기를 지정 합니다. 이 설정에 대 한 자세한 내용은 방법과 toooverride, 참조 <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">최적화 자동 조인 변환</a> Hortonworks 설명서에 있습니다. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>HDInsight의 2014/12/23 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호는:

* HDInsight     2.1.10.420.1246783    (HDP 버전 변경되지 않음)
* HDInsight     3.0.6.420.1246783    (HDP 버전 변경되지 않음)
* HDInsight     3.1.1.420.1246783    (HDP 버전 변경되지 않음)

이 릴리스에서 업데이트 이후에 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>구성 요소</th>
<th>클러스터 유형</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>Tooexcessive 부하 인해 일시적인 클러스터 만들기 실패</td>
<td><p>클러스터를 만드는 동안 HDP 패키지를 다운로드 하기 위한 향상 된 알고리즘에는 보다 강력한 처리할을 tooexcessive 부하 인해 발생 한 실패 수 있습니다.</p></td>
<td>부여</td>
<td>Hadoop, Hbase, Storm</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>HDInsight의 2014/12/18 릴리스 정보
이 릴리스에서 구성 요소 업데이트 이후에 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>구성 요소</th>
<th>클러스터 유형</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">클러스터 사용자 지정 일반 공급</a></td>
<td><p>사용자 지정 기능을 제공 hello 드립니다 toocustomize hello Apache Hadoop 에코 시스템에서 사용할 수 있는 프로젝트와 함께 Azure HDInsight 클러스터입니다. 이 새로운 기능을 실험 하 고 HDInsight Hadoop 프로젝트 tooAzure 배포할 수 있습니다. Hello를 통해이 작업이 가능 **스크립트 동작** 사용자 지정 스크립트를 사용 하 여 임의 방식 Hadoop 클러스터를 수정할 수 있는 기능을 합니다. 이 사용자 지정 방식은 Hadoop, HBase, Storm을 비롯한 모든 HDInsight 유형에서 사용할 수 있습니다. 이 기능은 toodemonstrate hello 기능, 인기 있는 hello 프로세스 tooinstall hello 문서화 우리 <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, 및 <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> 모듈입니다. 이 릴리스에서 또한 추가 toospecify 고객에 대 한 hello 기능 hello Azure 포털을 통해 자신의 사용자 지정 스크립트 동작, 지침 및 toobuild 사용자 지정 도우미 메서드를 사용 하 여 작업을 스크립팅 하는 방법에 대 한 모범 사례를 제공 하 고 있는 방법에 대 한 지침을 제공 tootest hello 스크립트 동작입니다. </p></td>
<td>기능 일반 공급</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>HDInsight의 2014/12/05 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호는:

* HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)
* HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)
* HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)
* HDInsight SDK 해당 없음

이 릴리스에서 구성 요소 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr>
<th>제목</th>
<th>설명</th>
<th>구성 요소</th>
<th>클러스터 유형</th>
<th>JIRA(적용 가능한 경우)</th>
</tr>
<tr>
<td>버그 수정: 하이브 DDL에서 많은 수의 파티션 tooa 테이블을 추가 하는 동안 일시적인 오류 </td>
<td><p>테이블 파티션 tooa Hive 테이블의 경우 hello 하이브 metastore 데이터베이스와 함께 일시적인 연결 오류가 발생 하는, DDL 하이브 hello 실패할 수 있습니다. 이 오류가 발생 하면 문이 isseen hello 하이브 오류 로그에 다음 hello: </p><p>"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0. 이 의미일 수 불균형된 호출 tooopenTransaction/commitTransaction 된다고) "</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE-482(내부 JIRA이므로 외부에서 인용할 수 없습니다. 여기에 참조용으로 기록되었습니다.)</td>
</tr>
<tr>
<td>버그 수정: hello HDInsight 쿼리 콘솔에서에서 가끔 나타나는 중지</td>
<td>이 경우 hello 다음 문은에서 볼 수 있습니다 hello WebHCat 시작 관리자 작업에 대 한 hello WebHCat 로그: <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): 기록 파일 {wasb url toohello 기록 파일을 (를) 로드할 수 없습니다 "</p></td>
<td>WebHCat</td>
<td>Hadoop은</td>
<td>HIVE-482(내부 JIRA이므로 외부에서 인용할 수 없습니다. 여기에 참조용으로 기록되었습니다.)</td>
</tr>
<tr>
<td>버그 수정: Hbase 쿼리 대기 시간의 간헐적 급증</td>
<td>이 경우 사용자가 Hbase 쿼리의 hello 대기 시간에 3 초는 가끔 발생 하 여 급증으로 바뀝니다. </td>
<td>HDInsight 클러스터 게이트웨이</td>
<td>HBase</td>
<td>해당 없음</td>
</tr>
<tr>
<td>HDP JAR 파일 이름 변경</td>
<td>HDI 클러스터 버전 3.0, 몇 가지 변경 toohello 내부 JAR 파일 HDP 하 여 설치 되어 있습니다. jetty-6.1.26.jar은 jetty-6.1.26.hwx.jar로 대체되었습니다. jetty-util-6.1.26.jar은 jetty-util-6.1.26.hwx.jar로 대체되었습니다. 이러한 변경 내용은 tooHadoop, Mahout, WebHCat 및 Oozie 프로젝트를 적용 합니다.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>HDInsight의 2014/11/21 릴리스 정보
이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호는:

* HDInsight 2.1.9.382.1169709(2014/11/14에서 변경 없음)
* HDInsight 3.0.5.382.1169709(2014/11/14에서 변경 없음)
* HDInsight 3.1.1.382.1169709(2014/11/14에서 변경 없음)
* HDInsight SDK 1.4.0

이 릴리스에서 구성 요소 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr><th>제목</th><th>설명</th><th>구성 요소</th><th>클러스터 유형</th><th>JIRA(적용 가능한 경우)</th></tr>
<tr>
<td>응용 프로그램 로그 액세스</td>
<td>기능 tooprogrammatically 클러스터에서 실행 되는 응용 프로그램 및 toodownload 관련 응용 프로그램 또는 컨테이너 로그 toohelp 디버그 문제가 있는 응용 프로그램을 열거 합니다.</td>
<td>SDK)</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>IHdInsightClient.DeleteCluster 기능 toospecify 지역 이름 </td>
<td>Azure HDInsight SDK hello hello 기능 toospecify 영역 이름을 제공 사용 하는 경우 **DeleteCluster**합니다. 이렇게 하면 서로 다른 지역에 동일한 이름 가진 두 개의 리소스를 보유 한 없습니다 toodelete 되 고 고객에 게 차단을 해제 둘 중 하나입니다.</td>
<td>SDK)</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>hello **ClusterDetails** 반환 개체는 **DeploymentID** hello 클러스터에 대 한 고유 식별자를 나타내는 필드입니다. Hello로 toobe 클러스터를 만드는 전체에서 고유 시도 동일 보장할 수는 이름입니다.</td>
<td>SDK)</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>HDInsight의 2014/11/14 릴리스 정보

이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호는:

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

이 릴리스의 새로운 기능, 구성 요소 업데이트 및 버그 수정 다음 hello를 포함 합니다.

<table border="1">
<tr><th>제목</th><th>설명</th><th>구성 요소</th><th>클러스터 유형</th><th>JIRA(적용 가능한 경우)</th></tr>
<tr>
<td>스크립트 작업(미리 보기):</td>
<td>임의 방식 사용자 지정 스크립트를 사용 하 여 Hadoop 수정할 수 있도록 하는 hello 클러스터 사용자 지정 기능의 미리 보기를 클러스터링 합니다. 이 기능을 사용자가 연결한 선택한 hello Apache Hadoop 생태계 tooAzure HDInsight 클러스터에서 사용할 수 있는 프로젝트를 배포 합니다. 이 사용자 지정 기능은 Hadoop, HBase, Storm을 비롯한 모든 HDInsight 유형에서 사용할 수 있습니다.</td>
<td>새로운 기능</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>Azure 웹 사이트 및 저장소 로그 분석을 위해 미리 빌드된 작업</td>
<td>hello HDInsight 쿼리 콘솔에는 데이터에 대해 또는 예제 데이터에서 작동 하는 솔루션을 지 원하는 시작 갤러리를 있습니다.
<p>**사용자의 데이터를 기반으로 작동하는 솔루션**:<br>
일부 hello 가장 일반적인 데이터 분석 시나리오 tooprovide 사용자 고유의 솔루션을 만들기 위한 시작 지점에 대 한 작업 만들었습니다. Hello 작업 toosee 작동 방식으로 데이터를 사용할 수 있습니다. 다음 준비 되 면 배운 toocreate 솔루션은 hello 미리 작성 된 작업 다음에 모델링을 사용 합니다.</p>
<p>**샘플 데이터를 기반으로 작동하는 솔루션**:<br>
자세한 방법을 몇 가지 기본 시나리오 (예: 웹 로그 및 센서 데이터를 분석)를 통해 탐색 하 여 HDInsight와 toowork 합니다. 배웁니다 어떻게 toouse HDInsight tooanalyze 이러한 데이터 및 기타 응용 프로그램 및 서비스 toothis 데이터를 연결 하는 방법입니다. 이 방법의 hello 전원의 예제를 제공 tooMicrosoft Excel 연결 하 여 데이터를 시각화 합니다.</p></td>
<td>쿼리 콘솔</td>
<td>Hadoop은</td>
<td>해당 없음</td>
</tr>
<tr>
<td>Templeton의 메모리 누수 수정</td>
<td>장기간 실행되는 클러스터가 있거나 1초에 수백 개의 작업 요청을 전송하는 고객에게 영향을 미친 Templeton의 메모리 누수가 해결되었습니다. hello Templeton 5xx 오류 및 hello 해결 방법으로 매니페스트 문제 was toorestart hello 서비스입니다. hello 해결 방법은 더 이상 필요 합니다.</td>
<td>Templeton</td>
<td>모두</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> toodemonstrate hello 새로운 기능을 사용할 수 있는 클러스터 사용자 지정 스크립트 동작 tooinstall Spark 및 R 모듈을 사용 하 여 클러스터에 hello 절차 문서화 되었습니다. 자세한 내용은 다음을 참조하세요.

* [HDInsight 클러스터에 Spark 1.0 설치 및 사용](hdinsight-hadoop-spark-install.md)
* [HDInsight Hadoop 클러스터에 R 설치 및 사용](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>HDInsight의 2014/11/07 릴리스 정보

이 릴리스를 사용 하 여 배포 하는 HDInsight 클러스터에 대 한 hello 전체 버전 번호는:

* HDInsight 2.1    2.1.9.374.1153876
* HDInsight 3.0    3.0.5.374.1153876
* HDInsight 3.1    3.1.1.374.1153876

이 릴리스에서 구성 요소 업데이트를 수행 하는 hello를 포함 되어 있습니다.

<table border="1">
<tr><th>제목</th><th>설명</th><th>구성 요소</th><th>클러스터 유형</th><th>JIRA(적용 가능한 경우)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>이 릴리스는 HDP(Hortonworks Data Platform) 2.1.7에 기반을 둡니다. 자세한 내용은 <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">HDP 2.1.7 릴리스 정보</a>를 참조하세요.</td>
<td>HDP</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
<tr>
<td>YARN Timeline Server</td>
<td>hello YARN 타임 라인 서버 (라고도 일반 응용 프로그램 기록 서버 hello) 기본적으로 설정 되었습니다. 시간 표시 막대 서버 hello 완성 된 응용 프로그램 (예: 응용 프로그램 ID, 응용 프로그램 이름, 응용 프로그램 상태, 응용 프로그램 제출 시간 및 완료 시간 응용 프로그램)에 대 한 일반 정보를 제공합니다.

Hello http://headnodehost:8188 URI에 액세스 하 여 또는 hello YARN 명령을 실행 하 여 헤드 노드 hello에서에서이 응용 프로그램 정보를 검색할 수 있습니다: yarn 응용 프로그램--appStates 목록 모든 합니다.

이 정보는 REST API를 통해 https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/에서 원격으로 검색할 수도 있습니다.

자세한 내용은 <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>를 참조하세요.</td>
<td>서비스, YARN</td>
<td>Hadoop, HBase</td>
<td>해당 없음</td>
</tr>
<tr>
<td>클러스터 배포 ID</td>
<td>SDK 버전 1.3.3.1.5426.29232부터 사용자는 각 클러스터에 대해 HDInsight에서 발급된 고유 ID에 액세스할 수 있습니다. 이 수 있도록 고객 toofigure 클러스터에서 DNS 이름을 다시 사용 하는 경우의 고유 인스턴스를 만들거나 시나리오를 삭제 합니다.</td>
<td>SDK)</td>
<td>모두</td>
<td>해당 없음</td>
</tr>
</table>

> [!NOTE]
> 이 릴리스에서 hello 포털에서 표시 또는 Windows PowerShell 또는 hello SDK로 반환 되 고 hello 전체 버전 번호를 방해 하는 hello 버그가 수정 되었습니다.

## <a name="notes-for-10152014-release"></a>2014/10/15 릴리스 정보

이 핫픽스 릴리스 Templeton Templeton의 hello 작업량이 많은 사용자의 영향을에서 메모리 누수를 해결 합니다. 경우에 따라 Templeton 과도 하 게 실행 사용자 것 hello 요청은 충분 한 메모리 toorun 없기 때문에 오류 코드를 500으로 표시 되는 오류를 표시 됩니다. 이 문제에 대 한 hello 해결 toorestart hello Templeton 서비스 했습니다. 이 문제가 해결되었습니다.

## <a name="notes-for-1072014-release"></a>2014/10/7 릴리스 정보

* Ambari를 사용 하는 경우 끝점, "을 (를) https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname" hello *host_name* 반환 필드 만 hello 호스트 이름 대신 hello 노드의 정규화 된 도메인 이름 (FQDN)을 hello 합니다. 예를 들어 반환 하는 대신 "**headnode0**", hello FQDN을 얻게"**headnode0. { ClusterDNS}.azurehdinsight.net**"입니다. 이 변경 내용을 하나의 가상 네트워크에 여러 클러스터 유형 (예: HBase 및 Hadoop)를 배포할 수 있는 필수 toofacilitate 시나리오 했습니다. 예를 들어 Hadoop의 백 엔드 플랫폼으로 HBase를 사용하는 등의 경우 이 변경이 적용됩니다.

* Hello HDInsight 클러스터의 기본 배포 hello에 대 한 새 메모리 설정을 제공 합니다. 배포 중인 CPU 코어 수가 hello에 대 한 hello 지침 이전 기본 메모리 설정을 적절 하 게 차지 하지 않습니다. 이러한 새 메모리 설정은 Hortonworks 권장 사항에 따라 향상된 기본값을 제공합니다. toochange 이러한 클러스터 구성을 변경 하는 방법에 대 한 toohello SDK 참조 설명서를 참조 하십시오. 다음 표에 hello에 hello 기본값: 4 개 CPU 코어 (8 컨테이너) HDInsight 클러스터에서 사용 되는 hello 새 메모리 설정은 항목별로 됩니다. (hello 사용 되는 값 toothis 이전 릴리스도 제공 됩니다 parenthetically.)

<table border="1">
<tr><th>구성 요소</th><th>메모리 할당</th></tr>
<tr><td> yarn.scheduler.minimum-allocation</td><td>768MB(이전에는 512MB)</td></tr>
<tr><td> yarn.scheduler.maximum-allocation</td><td>6144MB(변경되지 않음)</td></tr>
<tr><td>yarn.nodemanager.resource.memory</td><td>6144MB(변경되지 않음)</td></tr>
<tr><td>mapreduce.map.memory</td><td>768MB(이전에는 512MB)</td></tr>
<tr><td>mapreduce.map.java.opts</td><td>opts=-Xmx512m(이전에는 -Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.memory</td><td>1536MB(이전에는 1024MB)</td></tr>
<tr><td>mapreduce.reduce.java.opts</td><td>opts=-Xmx1024m(이전에는 -Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.am.resource</td><td>768MB(이전에는 1024MB)</td></tr>
<tr><td>yarn.app.mapreduce.am.command</td><td>opts=-Xmx512m(이전에는 -Xmx819m)</td></tr>
<tr><td>mapreduce.task.io.sort</td><td>256MB(이전에는 200MB)</td></tr>
<tr><td>tez.am.resource.memory</td><td>1536MB(변경되지 않음)</td></tr>
</table>

YARN 및 MapReduce hello HDInsight에서 사용 되는 Hortonworks Data Platform에서 사용 하는 hello 메모리 구성 설정에 대 한 자세한 내용은 참조 [HDP 메모리 구성 설정 확인](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html)합니다. Hortonworks는 toocalculate 적절 한 메모리 설정을 도구를도 제공 합니다.

Azure PowerShell hello 및 hello HDInsight SDK 오류 메시지 관련 항목: "*HTTP 서비스 액세스에 대해 구성 되지 않은*":

* 이 오류는 알려진 [호환성 문제가](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) hello 버전의 hello HDInsight SDK 또는 Azure PowerShell 및 hello 버전 hello 클러스터의 tooa 차이 인해 발생할 수 있는 합니다. 8/15 또는 그 이후에 만든 클러스터는 가상 네트워크에 대한 새로운 프로비전 기능을 지원합니다. 하지만이 기능은 이전 버전의 hello HDInsight SDK 또는 Azure PowerShell에서 올바르게 해석 되지 않습니다. hello 결과 일부 작업 전송 작업에 실패 합니다. HDInsight SDK Api 또는 Azure PowerShell cmdlet을 사용 하는 경우 (**사용 AzureRmHDInsightCluster** 또는 **Invoke AzureRmHDInsightHiveJob**) toosubmit 작업, 해당 작업이 hello 오류 메시지와 함께 실패할 수 있습니다 " *클러스터 <clustername> HTTP 서비스 액세스에 대해 구성 되지 않았습니다*. " (작업에 따라 hello)를 발생할 수 있습니다 다른 오류 메시지와 같은 또는 "*toocluster 연결할 수 없습니다.*"입니다.
* Hello 최신 버전의 hello HDInsight SDK 및 Azure PowerShell에서 이러한 호환성 문제를 해결 합니다. 업데이트 하는 것이 좋습니다 HDInsight SDK tooversion 1.3.1.6 또는 이후 및 Azure PowerShell 도구 tooversion 0.8.8 hello 이상. 액세스 toohello 얻을 수 있습니다에서 최신 HDInsight SDK [덩어리](http://nuget.codeplex.com/wikipage?title=Getting%20Started) hello에 Azure PowerShell 도구 및 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>HDInsight 3.1의 2014/9/12 릴리스 정보
* 이 릴리스는 HDP(Hortonworks Data Platform) 2.1.5에 기반을 둡니다. 이 릴리스에서 수정 된 hello 버그의 목록에 대 한 참조 hello [이 릴리스에서 수정](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) hello Hortonworks 사이트에서 페이지.
* Hello Pig 라이브러리 폴더에 "avro mapred 1.7.4.jar" hello 파일이 변경 되어 너무 "avro-mapred-1.7.4-hadoop2.jar." 이 파일의 내용을 hello 줄 바꿈하지 않는 있는 사소한 버그 수정 포함 되어 있습니다. 고객 tooavoid 중단 된 파일을 파일의 이름을 바꾸는 경우 JAR hello의 hello 이름에 직접 종속성을 구성 하지 않는 것이 좋습니다.

## <a name="notes-for-8212014-release"></a>2014/8/21 릴리스 정보
* 같은 작업 too1 GB Templeton 컨트롤러에 대 한 hello 기본 메모리 제한을 설정 하는 WebHCat 구성이 (하이브-7155) hello를 추가 됩니다. (이전 hello 기본값은 512MB입니다.)

     templeton.mapper.memory.mb (=1024)

  * 이 변경 사항은 해결 hello 다음 특정 하이브 쿼리 toolower 메모리 제한 때문에 오류가 발생 했습니다: "컨테이너는 실제 메모리도 넘어 실행 중" 합니다.
  * toorevert toohello 이전 기본값, Azure PowerShell을 통해이 구성 값 too512 hello 다음 명령을 사용 하 여 클러스터를 만들 때 설정할 수 있습니다.

      Add-AzureHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* hello 사육 역할의 hello 호스트 이름을 너무 변경*사육*합니다. Hello 클러스터 내에서 이름 확인을 미치면 하지만 외부 REST Api 영향을 주지 않습니다. 구성 요소가 있으면 해당 사용 하 여 hello *zookeepernode* 호스트 이름 tooupdate 해야 해당 toouse 새 이름입니다. hello 사육 노드 3 개 hello에 대 한 새 이름은 다음과 같습니다.

  * zookeeper0
  * zookeeper1
  * zookeeper2
* HBase 버전 지원 매트릭스가 업데이트됩니다. 프로덕션 HBase 워크로드에는 HDInsight 버전 3.1(HBase 버전 0.98)만 지원됩니다. 미리 보기에 사용 가능한 버전 3.0은 앞으로 지원되지 않습니다.

## <a name="notes-about-clusters-created-prior-too8152014"></a>클러스터에 대 한 참고 사항 만든 이전 too8/15/2014
Azure PowerShell 또는 HDInsight SDK 오류 메시지를 "클러스터 <clustername> HTTP 서비스 액세스에 대해 구성 되지 않았습니다" (있거나 hello 작업에 따라 다른 오류 메시지와 같은: "toocluster 연결할 수 없음") tooa 버전 차이 때문에 발견할 수 Azure PowerShell 또는 hello HDInsight SDK와 클러스터 간에 8/15 또는 그 이후에 만든 클러스터는 가상 네트워크에 대한 새로운 프로비전 기능을 지원합니다. 이 기능은 이전 버전의 Azure PowerShell hello 또는 hello HDInsight SDK로 인해 작업 제출 작업의 오류가 발생 하 여 올바르게 해석 되지 않습니다. HDInsight SDK Api 또는 Azure PowerShell cmdlet (예: 사용 AzureRmHDInsightCluster 또는 Invoke AzureRmHDInsightHiveJob) toosubmit 작업을 사용 하면 설명 하는 hello 오류 메시지 중 하나가 지정 된 이러한 작업이 실패할 수 있습니다.

Hello 최신 버전의 hello HDInsight SDK 및 Azure PowerShell에서 이러한 호환성 문제를 해결 합니다. 업데이트 하는 것이 좋습니다 HDInsight SDK tooversion 1.3.1.6 또는 이후 및 Azure PowerShell 도구 tooversion 0.8.8 hello 이상. 액세스 toohello 얻을 수에서 최신 HDInsight SDK [NuGet][nuget-link]합니다. Hello Azure PowerShell 도구를 사용 하 여 액세스할 수 있습니다 [Microsoft 웹 플랫폼 설치 관리자][webpi-link]합니다.

## <a name="notes-for-7282014-release"></a>2014/7/28 릴리스 정보
* **새 지역에 HDInsight**: HDInsight 지리적 존재 toothree 영역을 확장 했습니다. HDInsight 고객은 다음 지역에서 클러스터를 만들 수 있습니다.
  * 동아시아
  * 미국 중북부
  * 미국 중남부
* HDInsight 버전 1.6 (HDP 1.1 및 Hadoop 1.0.3) 및 HDInsight 버전 2.1 (HDP1.3 및 Hadoop 1.2) hello Azure 포털에서에서 제거 되 고 됩니다. Toocreate Hadoop 클러스터를 계속 수를 사용 하 여 이러한 버전 hello Azure PowerShell cmdlet에 대 한 [새로 AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) 또는 hello를 사용 하 여 [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx)합니다. 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.
* 이 릴리스의 HDP(Hortonworks Data Platform) 변경 내용:

<table border="1">
<tr><th>HDP</th><th>변경 내용</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>변경 내용 없음</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>변경 내용 없음</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>2014/6/24 릴리스 정보
이 릴리스에서 향상 된 기능 toohello HDInsight 서비스를 포함 되어 있습니다.

* **HDP 2.1 가용성**: HDInsight 3.1 (을 HDP 2.1 포함)는 일반적으로 사용할 수 있으며 새 클러스터에 대 한 hello 기본 버전.
* **HBase - Azure Portal 개선 사항**: 미리 보기에서 HBase 클러스터를 사용할 수 있습니다. 단 몇 번의 클릭으로 hello 포털에서 HBase 클러스터를 만들 수 있습니다.

HBase, 수백만 개의 끝점에서에서 센서 및 원격 분석 데이터를 저장 하는 큰 데이터 집합 tooservices 작동 하는 대화형 웹 사이트에서 HDInsight의 다양 한 실시간 작업 부하를 빌드할 수 있습니다. hello 다음 단계는 Hadoop 작업을 사용 하 여 이러한 작업의 tooanalyze hello 데이터와 Azure PowerShell 및 hello 하이브 클러스터 대시보드를 통해 HDInsight에서 가능 합니다.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>HDInsight 3.1에 사전 설치되는 Apache Mahout
 [Mahout](http://hortonworks.com/hadoop/mahout/) 추가 클러스터 구성에 대 한 hello 필요 없이 Mahout 작업을 실행할 수 있도록 HDInsight 3.1 Hadoop 클러스터에 미리 설치 됩니다. 예를 들어 하면 원격 Hadoop 클러스터에 원격 데스크톱 프로토콜 (RDP)를 사용 하 여 및 추가 단계 없이 hello 다음 Hello World Mahout 명령을 실행할 수 있습니다.

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

이 절차 설명은 보다 완전 hello에 대 한 hello 설명서를 참조 하십시오. [Breiman 예제](https://mahout.apache.org/users/classification/breiman-example.html) hello Apache Mahout 웹 사이트에 있습니다.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Hive 쿼리는 HDinsight 3.1에서 Tez를 사용할 수 있음
Hive 0.13은 HDInsight 3.1에서 사용 가능하며 Tez를 사용하여 쿼리를 실행할 수 있으므로, 실질적인 성능 개선을 이룰 수 있습니다.
Tez는 기본적으로 Hive 쿼리에 사용할 수 없습니다. toouse 옵트인 해야, 합니다. 다음 코드 조각 hello를 실행 하 여 Tez를 설정할 수 있습니다.

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks에서 표준 벤치마크로 전달되는 Tez와 함께 사용하는 Hive 쿼리 성능 개선 사항의 자세한 분석을 게시했습니다. 자세한 내용은 [Enterprise Hadoop용 Apache Hive 13 벤치마킹](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/)을 참조하세요.

자세한 내용은 [Tez의 Hive](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)를 참조하세요.

### <a name="global-availability"></a>전 세계 이용 가능 여부
Hdinsight Hadoop 2.2 hello 릴리스에서 Microsoft가 사용 하도록 설정한 HDInsight Azure를 사용할 수 있는 모든 주요 지역에 있습니다. 특히, hello 서 부 유럽 및 동남 아시아 데이터 센터 온라인 상태가 있어야 합니다. 따라서 고객 toolocate 클러스터 가까운 데이터 센터 및 잠재적으로 규정 준수 요구 사항이 영역에 있습니다.

### <a name="dos--donts-between-cluster-versions"></a>클러스터 버전 간에 수행할 수 있는 작업과 수행할 수 없는 작업
**HDInsight 3.1 클러스터에 사용되는 Oozie Metastore가 이전 버전인 HDInsight 2.1 클러스터와 호환되지 않으므로 해당 이전 버전에서는 사용할 수 없음**

HDInsight 3.1 클러스터와 함께 배포한 사용자 지정 Oozie 메타 저장소 데이터베이스는 HDInsight 2.1 클러스터와 함께 다시 사용할 수 없습니다. 이 경우 hello hello metastore는 HDInsight 2.1 클러스터 로부터 가져온 경우에 합니다. 이 시나리오에는 더 이상 hello 2.1 HDInsight 클러스터에 필요한 hello metastore와 호환 되도록 3.1 HDInsight 클러스터와 함께 사용할 경우 hello metastore 스키마 업그레이드 가져옵니다 때문에 지원 되지 않습니다. 모든 시도가 tooreuse 3.1 HDInsight 클러스터와 사용 된 Oozie metastore 쓸모 hello 2.1 HDInsight 클러스터를 렌더링 합니다.

**Oozie Metastore는 클러스터 간에 공유할 수 없음**

Oozie metastore는 연결 된 toospecific 클러스터와 클러스터 간에 공유할 수는 없습니다.

### <a name="breaking-changes"></a>주요 변경 내용
**전위 구문**: hello만 "wasb: / /" 구문을 HDInsight 3.1와 3.0 클러스터에서 사용할 수 있습니다. 이전 hello "asv: / /" 구문을 HDInsight 2.1와 1.6 클러스터에서 사용할 수 있지만 HDInsight 3.1 또는 3.0 클러스터에서 지원 되지 않습니다. 즉, 모든 작업이 tooan HDInsight 클러스터를 명시적으로 3.0 또는 3.1 hello를 사용 하 여 제출 된 "asv: / /" 구문 실패 합니다. hello "wasb: / /" 구문을 대신 사용 해야 합니다. 또한 작업이 전송 tooany HDInsight 3.1 또는 사용 하 여 만든를 포함 하는 기존 metastore 명시적 3.0 클러스터 tooresources hello를 사용 하 여 참조 "asv: / /" 구문 실패 합니다. 이러한 metastore 필요 toobe hello를 사용 하 여 다시 생성 "wasb: / /" 구문 tooaddress 리소스입니다.

**포트**: hello HDInsight 서비스에서 사용 하는 hello 포트가 변경 합니다. hello Windows 운영 체제의 hello 임시 포트 범위 내에서 사용 되는 포트 번호를 hello 했습니다. 포트는 수명이 짧은 인터넷 프로토콜 기반 통신용으로 미리 정의된 사용 후 삭제되는 범위에서 자동으로 할당됩니다. hello 새 Hortonworks Data Platform (HDP) 서비스 포트 번호를 허용 되는 hello 헤드 노드에서 실행 되는 서비스에서 사용 하는 hello 포트와 함께 발생 하는 충돌 하는이 범위 tooavoid 밖에 있습니다. hello 새 포트 번호는 주요 변경 내용이 발생 하지 않습니다. 사용 되는 hello 번호는 다음과 같습니다.

 **HDInsight 1.6(HDP 1.1)**

<table border="1">
<tr><th>이름</th><th>값</th></tr>
<tr><td>dfs.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.task.tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 및 3.0(HDP 2.1 및 2.0)**

<table border="1">
<tr><th>이름</th><th>값</th></tr>
<tr><td>dfs.namenode.http-address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.namenode.https-address</td><td>headnodehost:30470</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.namenode.secondary.http-address</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>종속성
hello 다음 종속성에서에서 추가 된 HDInsight 3.x (HDP2.x):

* guice-servlet
* optiq-core
* javax.inject
* activation
* jsr305
* geronimo-jaspic_1.0_spec
* jul-to-slf4j
* java-xmlbuilder
* ant
* commons-compiler
* jdo-api
* commons-math3
* paranamer
* jaxb-impl
* stringtemplate
* eigenbase-xom
* jersey-servlet
* commons-exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq-avatica
* jta
* eigenbase-properties
* groovy-all
* hamcrest-core
* mail
* linq4j
* jpam
* jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant-launcher
* jersey-guice
* xml-apis
* stax-api
* asm-commons
* asm-tree
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* velocity
* jettison
* snappy-java
* jetty-all
* commons-dbcp

hello 다음 종속성에에서 더 이상 존재 HDInsight 3.x (HDP2.x):

* jdeb
* kfs
* sqlline
* ivy
* aspectjrt
* json :
* core
* jdo2-api
* avro-mapred
* datanucleus-enhancer
* jsp
* commons-logging-api
* commons-math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* HBase:
* snappy

### <a name="version-changes"></a>버전 변경 내용
버전 변경에 따라 hello HDInsight까지 수행한 2.x (HDP1.x) 및 HDInsight 3.x (HDP2.x):

* metrics-core: ['2.1.2'] -> ['3.0.0']
* derbynet: ['10.4.2.0'] -> ['10.10.1.1']
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* jasper-compiler: ['5.5.12'] -> ['5.5.23']
* log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: ['10.4.2.0'] -> ['10.10.1.1']
* httpcore: ['4.2.4'] -> ['4.2.5']
* hsqldb: ['1.8.0.10'] -> ['2.0.0']
* jets3t: ['0.6.1'] -> ['0.9.0']
* protobuf-java: ['2.4.1'] -> ['2.5.0']
* derby: ['10.4.2.0'] -> ['10.10.1.1']
* jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']
* commons-daemon: ['1.0.1'] -> ['1.0.13']
* datanucleus-core: ['3.0.9'] -> ['3.2.10']
* datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']
* zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']
* bonecp: ['0.7.1.RELEASE'] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>드라이버
SQL Server에 대 한 hello Java JDBC (Database Connectivity) 드라이버 HDInsight에서 내부적으로 사용 됩니다 및 외부 작업에 사용 되지 않습니다. Tooconnect tooHDInsight ODBC Open Database Connectivity ()를 사용 하 여 원하는 hello Microsoft 하이브 ODBC 드라이버를 사용 하십시오. 자세한 내용은 참조 [Microsoft ODBC Driver 하이브 hello로 Excel 연결 tooHDInsight](hdinsight-connect-excel-hive-odbc-driver.md)합니다.

### <a name="bug-fixes"></a>버그 수정
이 릴리스에서 다양 한 버그 수정 사항이 있는 HDInsight 버전을 다음 hello 새로 고치지 했습니다.

* HDInsight 2.1(HDP 1.3)
* HDInsight 3.0(HDP 2.0)
* HDInsight 3.1(HDP 2.1)

## <a name="hortonworks-release-notes"></a>Hortonworks 릴리스 정보
HDInsight 버전 클러스터에서 사용 되는 Hortonworks 데이터 플랫폼 (HDPs) hello에 대 한 릴리스 정보 hello 다음 위치에서 사용할 수 있습니다.

* HDInsight 버전 3.1 hello를 기반으로 하는 Hadoop 배포를 사용 하 여 [Hortonworks Data Platform 2.1.7][hdp-2-1-7]합니다. 2014/11/7/후 hello Azure 포털을 사용할 때 만든 hello 기본 Hadoop 클러스터입니다. 2014/11/7/된 hello 기반 전의 HDInsight 3.1 클러스터 [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight 버전 3.0 hello를 기반으로 하는 Hadoop 배포를 사용 하 여 [Hortonworks 데이터 플랫폼 2.0][hdp-2-0-8]합니다.
* HDInsight 버전 2.1 hello를 기반으로 하는 Hadoop 배포를 사용 하 여 [Hortonworks 데이터 플랫폼 1.3][hdp-1-3-0]합니다.
* HDInsight 버전 1.6 hello를 기반으로 하는 Hadoop 배포를 사용 하 여 [Hortonworks 데이터 플랫폼 1.1][hdp-1-1-0]합니다.

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
