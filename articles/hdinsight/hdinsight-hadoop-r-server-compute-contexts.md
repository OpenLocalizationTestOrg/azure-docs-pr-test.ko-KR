---
title: "Azure HDInsight에 R Server에 대 한 상황에 맞는 aaaCompute 옵션 | Microsoft Docs"
description: "Hello 다른 계산 컨텍스트 옵션 사용 가능한 toousers HDInsight에 R server에 대 한 자세한 내용은"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>HDInsight에서 R 서버의 계산 컨텍스트 옵션

Azure HDInsight의 Microsoft R Server는 hello 계산 컨텍스트를 설정 하 여 호출을 실행 하는 방법을 제어 합니다. 이 문서에는 hello 있는 옵션을 사용할 수 있는 toospecify 여부 및 실행 hello 가장자리 노드 또는 HDInsight 클러스터의 코어에서 병렬 처리 방법을 간략하게 설명 합니다.

클러스터의 hello 가장자리 노드 R 스크립트 편리한 위치 tooconnect toohello 클러스터 및 toorun 제공합니다. 가장자리 노드 ScaleR의 hello distributed 옵션을 실행 중인 hello 평행 화 함수 hello에 지 노드 서버의 hello 코어 수 있습니다. 실행할 수도 있습니다 이러한 hello 클러스터의 hello 노드에서 ScaleR의 Hadoop 맵 감소 또는 Spark를 사용 하 여 계산 컨텍스트.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Azure HDInsight의 Microsoft R Server
[Azure HDInsight의 Microsoft R Server](hdinsight-hadoop-r-server-overview.md) R 기반 분석에 대 한 hello 최신 기능을 제공 합니다. HDFS 컨테이너에 저장 된 데이터를 사용할 수 있습니다 프로그램 [Azure Blob](../storage/common/storage-introduction.md "Azure Blob 저장소") 저장소 계정, 데이터 레이크 저장소 또는 hello 로컬 Linux 파일 시스템입니다. R Server는 오픈 소스 R 기술을 기반으로 한 이후 hello에 R 기반 응용 프로그램을 빌드할 hello 8000 + 오픈 소스 R 패키지를 적용할 수 있습니다. Hello 루틴을 사용할 수 있습니다 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), R Server에 포함 되어 있는 Microsoft의 빅 데이터 분석 패키지 합니다.  

## <a name="compute-contexts-for-an-edge-node"></a>에지 노드에 대한 계산 컨텍스트
일반적으로 R 서버 hello 가장자리 노드에서 실행 되는 R 스크립트를 해당 노드의 hello R 인터프리터 내에서 실행 됩니다. hello 예외 ScaleR 함수를 호출 하는 단계입니다. hello ScaleR 호출 hello ScaleR 계산 컨텍스트를 설정 하는 방법에 따라 결정 되는 계산 환경에서 실행 합니다.  가장자리 노드에서 R 스크립트를 실행 하는 경우 컨텍스트는 hello hello의 가능한 값 계산:

- 로컬 순차(*‘local’*)
- 로컬 병렬(*‘localpar’*)
- Map Reduce
- Spark

hello *'local'* 및 *'localpar'* 옵션 방법만 다릅니다 **rxExec** 호출이 실행 됩니다. 모두 실행 기타 rx 함수 호출 병렬 방식으로 모든 사용 가능한 코어 ScaleR hello 사용 하 여 달리 지정 되지 않은 **numCoresToUse** 옵션을 예를 들어 `rxOptions(numCoresToUse=6)`합니다. 병렬 실행 옵션은 최적의 성능을 제공합니다.

다음 표에 hello를 hello를 다양 한 계산 컨텍스트 옵션 tooset는 호출을 실행 하는 방법을 요약 되어 있습니다.

| 계산 컨텍스트  | 어떻게 tooset                      | 실행 컨텍스트                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| 로컬 순차 | rxSetComputeContext('local')    | 직렬로 실행 됩니다 rxExec 호출을 제외 하 고 hello 지 노드 서버 hello 코어에서 병렬된 실행 |
| 로컬 병렬   | rxSetComputeContext('localpar') | Hello 지 노드 서버 hello 코어에서 병렬된 실행 |
| Spark            | RxSpark()                       | Hello HDI 클러스터의 hello 노드에서 Spark 통해 분산된 실행 평행 화 |
| Map Reduce       | RxHadoopMR()                    | 병렬 배포를 통해 실행 맵 감소 hello 노드에서 hello HDI 클러스터의 |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>계산 컨텍스트를 결정하기 위한 지침

Hello 세 가지 옵션 중 선택 하면 병렬된 실행을 제공 하는 분석 작업, hello 크기 및 데이터의 hello 위치의 hello 특성에 따라 달라 집니다. 상황에 맞는 toouse 계산를 알려 주는 간단한 수식은 없습니다. 그러나 가지, hello 올바른 선택을 확인 하거나 적어도 벤치 마크를 실행 하기 전에 선택한 내용을 좁힐 하는 데 도움이 데 도움이 되는 몇 가지 원칙은 합니다. 기본 원칙은 다음과 같습니다.

- Linux 로컬 파일 시스템 hello HDFS 보다 빠릅니다.
- Hello 데이터는 로컬, 및 XDF 중인 경우에 반복 된 분석 빠릅니다.
- 되기 소량의 텍스트 데이터 원본에서 데이터를 toostream 것이 좋습니다. 데이터의 양을 hello 큰 경우 tooXDF 분석 하기 전에 변환 합니다.
- 복사 하거나 분석을 위해 hello 데이터 toohello 가장자리 노드 스트리밍의 hello 오버 헤드가 매우 많은 양의 데이터에 대 한 어려워집니다.
- Hadoop의 분석의 경우 Spark가 Map Reduce보다 빠릅니다.

이러한 원칙은 들어 hello 다음 섹션에서는 제공 몇 가지 일반적인 규칙 경험에의 한 계산 컨텍스트를 선택 하기 위한 합니다.

### <a name="local"></a>Local
* Hello 양의 데이터 tooanalyze 작고 경우 반복 되는 분석 하지 않아도, 다음 스트리밍되 hello 일상적인 사용 하 여 분석에 직접 *'local'* 또는 *'localpar'*합니다.
* Hello 양의 데이터 tooanalyze 작거나 중간 크기의 고 반복 되는 분석, 다음 toohello 로컬 파일 시스템 복사, tooXDF, 가져오기 및 분석을 통해 *'local'* 또는 *'localpar'*합니다.

### <a name="hadoop-spark"></a>Hadoop Spark
* Hello 양의 데이터 tooanalyze 크면 가져옵니다 tooa Spark 데이터 프레임을 사용 하 여 **RxHiveData** 또는 **RxParquetData**, 또는 HDFS에서 tooXDF (저장소 문제가 제외), Spark hello를 사용 하 여 분석 하 고 컨텍스트를 계산 합니다.

### <a name="hadoop-map-reduce"></a>Hadoop Map Reduce
* 일반적으로 느린 이므로 hello Spark 계산 컨텍스트는 극복할 수 문제가 발생 하는 경우에 hello 맵 감소 계산 컨텍스트를 사용 합니다.  

## <a name="inline-help-on-rxsetcomputecontext"></a>rxSetComputeContext의 인라인 도움말
자세한 내용 및 ScaleR의 예제에 대 한 계산 컨텍스트 r에서에 대 한 도움말 hello rxSetComputeContext 메서드, 예를 들어 hello 인라인을 참조 하십시오.

    > ?rxSetComputeContext

Toohello을 참조할 수 있습니다 "[ScaleR 분산 컴퓨팅 가이드](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" hello에서 사용할 수 있는 것 [R 서버 MSDN](https://msdn.microsoft.com/library/mt674634.aspx "MSDN에 R Server") 라이브러리입니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 toospecify 사용할 수 있는 hello 옵션에 대 한 실행 hello 가장자리 노드 또는 HDInsight 클러스터의 코어에서 병렬 처리 여부 및 방법을 합니다. toolearn toouse HDInsight와 R 서버 클러스터에 대 한 자세한 hello 다음 항목을 참조 하세요.

* [Hadoop용 R 서버 개요](hdinsight-hadoop-r-server-overview.md)
* [Hadoop용 R Server 시작](hdinsight-hadoop-r-server-get-started.md)
* [RStudio 서버 tooHDInsight 추가 (클러스터 생성 중에 추가 되지) 하는 경우](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight에서 R Server의 Azure Storage 옵션](hdinsight-hadoop-r-server-storage.md)

