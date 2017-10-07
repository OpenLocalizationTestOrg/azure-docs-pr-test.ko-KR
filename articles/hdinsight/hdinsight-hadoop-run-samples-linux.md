---
title: "Azure HDInsight에서 Hadoop MapReduce 예제 aaaRun | Microsoft Docs"
description: "HDInsight에 포함된 jar 파일의 MapReduce 샘플을 사용하여 시작하세요. SSH tooconnect toohello 클러스터를 사용 하 고 hello Hadoop 명령 toorun 샘플 작업을 사용 합니다."
keywords: "hadoop 예제 jar,hadoop 예제 jar,hadoop mapreduce 예제,mapreduce 예제"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>HDInsight에 포함 된 hello MapReduce 예제 실행

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

HDInsight에서 Hadoop으로 toorun hello MapReduce 예제를 포함 하는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>필수 조건

* **HDInsight 클러스터**: [Linux HDInsight에서 Hive와 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.

    > [!IMPORTANT]
    > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* **SSH 클라이언트**: 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a name="hello-mapreduce-examples"></a>hello MapReduce 예제

**위치**: hello 샘플 hello에서 HDInsight 클러스터에 있는 `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`합니다.

**내용을**: hello 샘플 다음이 보관 파일에 포함 되어 있습니다.

* `aggregatewordcount`: 집계 기반 mapreduce 프로그램 hello 입력된 파일에서 hello 단어 수를 계산 합니다.
* `aggregatewordhist`: 집계 hello 입력된 파일에 있는 hello 단어의 hello 히스토그램을 계산 하는 mapreduce 프로그램을 기반으로 합니다.
* `bbp`: Pi의 베일리-Borwein-Plouffe toocompute 정확한 자리를 사용 하는 mapreduce 프로그램입니다.
* `dbcount`예제에서는 작업: 데이터베이스에 저장 된 hello 페이지 보기 로그 계산입니다.
* `distbbp`: Pi의 BBP 형 수식 toocompute 정확한 비트를 사용 하는 mapreduce 프로그램입니다.
* `grep`: Hello 세는 mapreduce 프로그램 hello 입력에는 정규식의 일치 합니다.
* `join`: 정렬되고 동일하게 분할된 데이터 집합을 통해 조인을 수행하는 작업
* `multifilewc`: 여러 파일의 단어 수를 계산하는 작업
* `pentomino`: Mapreduce 타일 프로그램 toofind 솔루션 toopentomino 문제를 배치 합니다.
* `pi`: 준난수 몬테카를로 방법을 사용하여 Pi를 추정하는 mapreduce 프로그램
* `randomtextwriter`: 노드당 10GB의 임의 텍스트 데이터를 기록하는 mapreduce 프로그램
* `randomwriter`: 노드당 10GB의 임의 데이터를 기록하는 mapreduce 프로그램
* `secondarysort`2 차 정렬 toohello 정의: 예제 단계를 줄입니다.
* `sort`Mapreduce 프로그램: hello 임의 기록기가 기록한 hello 데이터 정렬입니다.
* `sudoku`: sudoku 해 찾기
* `teragen`: Hello terasort에 대 한 데이터를 생성 합니다.
* `terasort`: Hello terasort를 실행 합니다.
* `teravalidate`: terasort 결과 확인
* `wordcount`: Hello 입력된 파일에서 hello 단어 수를 계산 하는 mapreduce 프로그램입니다.
* `wordmean`: Hello hello 입력된 파일에서 hello 단어의 평균 길이 계산 하는 mapreduce 프로그램입니다.
* `wordmedian`: Hello 단어 hello 입력된 파일에서의 hello 중앙값 길이 계산 하는 mapreduce 프로그램입니다.
* `wordstandarddeviation`: Mapreduce 프로그램의 hello hello 단어 hello 길이의 hello 표준 편차를 계산 하는 입력 파일입니다.

**소스 코드**: 소스 코드에 대 한 이러한 예제는 hello에서 HDInsight 클러스터에 포함 되어 `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`합니다.

> [!NOTE]
> hello `2.2.4.9-1` hello에서 경로 hello HDInsight 클러스터에 대 한 hello Hortonworks Data Platform의 hello 버전 및 클러스터에 대해 다를 수 있습니다.

## <a name="run-hello-wordcount-example"></a>Hello wordcount 예제 실행

1. TooHDInsight SSH를 사용 하 여 연결 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. Hello에서 `username@#######:~$` 명령 toolist hello 예제를 따르는 hello를 사용 하 여, 메시지를 표시 합니다.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    이 명령은 hello이이 문서의 이전 섹션에서 샘플의 hello 목록을 생성합니다.

3. 명령 tooget 도움말에 나오는 특정 샘플에 사용 하 여 hello 합니다. 이 경우 hello **wordcount** 샘플:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Hello 메시지의 뒤에 나타납니다.

        Usage: wordcount <in> [<in>...] <out>

    이 메시지는 hello 원본 문서에 대 한 여러 입력된 경로 제공할 수 있는지를 나타냅니다. hello 최종 경로가 hello 출력 (hello 소스 문서에 있는 단어의 수) 저장 됩니다.

4. Hello 전자 필기장의 레오나르도 다빈치, 클러스터와 함께 예제 데이터로 제공 되는 모든 단어 hello toocount 다음 사용 합니다.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    이 작업에 대한 입력은 `/example/data/gutenberg/davinci.txt`에서 읽습니다. 이 예제의 출력은 `/example/data/davinciwordcount`에 저장됩니다. 두 경로 로컬 파일 시스템이 아닌 hello hello 클러스터에 대 한 기본 저장소에 있습니다.

   > [!NOTE]
   > Hello 단어 수 샘플에 대 한 hello 도움말에서 설명 했 듯이도 여러 개의 입력된 파일을 지정할 수 있습니다. 예를 들어 `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` 는 davinci.txt와 ulysses.txt 모두에서 단어 수를 계산합니다.

5. Hello 작업이 완료 되 면 다음 명령 tooview hello 출력 hello를 사용 합니다.

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    이 명령은 hello 작업에 의해 생성 된 모든 hello 출력 파일을 연결 합니다. Hello 출력 toohello 콘솔에 표시 됩니다. hello는 텍스트 다음 비슷한 toohello 출력:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    각 행에는 단어와 hello에서 발생 한 횟수 입력 데이터를 나타냅니다.

## <a name="hello-sudoku-example"></a>hello Sudoku 예제

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) 는 9개의 3x3 표로 구성된 논리 퍼즐입니다. Hello 표의 일부 셀에는 번호가, hello ´ ֲ toosolve hello 빈 셀에 대 한 고 다른 사용자는 비어 있습니다. hello 이전 링크 방법은 hello 퍼즐을 갖지만 hello이이 샘플은 toosolve hello 빈 셀에 대 한. 이 입력 형식에 따라 hello에 있는 파일 이어야 합니다.

* 9개 열의 9개 행
* 각 열은 숫자 또는 `?` (빈 셀을 나타냄)를 포함할 수 있음
* 셀은 공백으로 구분됨

특정 방식으로 tooconstruct Sudoku 퍼즐;는 숫자 열 이나 행을 반복할 수 없습니다. 제대로 생성 된 hello HDInsight 클러스터에 예가 있습니다. 파일은에 `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` hello 텍스트 다음을 포함 합니다.

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

toorun hello Sudoku 예제를 통해이 예제에서는 문제를 사용 하 여 다음 명령을 hello:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

hello 결과 텍스트 다음 비슷한 toohello 나타납니다.

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Pi(π) 예제

hello pi 예제를 사용 하 여 통계 (준 Monte Carlo) pi 메서드 tooestimate hello 값입니다. 점은 단위 정사각형 내에 임의로 배치됩니다. hello 사각형에 원을 포함 되어 있습니다. hello hello 포인트 hello 원 속하는 확률은으로 같은 toohello hello 원, pi/4입니다. pi의 hello 값 4R의 hello 값에서 예상할 수 있습니다. R는 hello 비율 hello 원 toohello hello 사각형 내에 있는 요소의 총 수 내에 있는 점의 hello 수입니다. hello 큰 hello 샘플 사용 하는 지점의 hello 더 나은 hello 예상 값은입니다.

이 샘플 명령은 toorun 다음 hello를 사용 합니다. 이 명령은 pi 10,000,000 샘플 tooestimate hello 값이 16 지도 사용합니다.

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

hello이 명령에서 반환 된 값은 유사한 너무**3.14159155000000000000**합니다. 참조를 hello pi의 처음 10 개의 소수 자릿수는 3.1415926535입니다.

## <a name="10-gb-greysort-example"></a>10GB Greysort 예제

GraySort는 벤치마크 정렬입니다. hello 메트릭을 많은 양의 데이터를 일반적으로 100TB 최소 정렬 하는 동안이 작업을 수행 하는 hello 정렬 속도 (TB/분)입니다.

이 샘플에서는 비교적 빠르게 실행할 수 있도록 적절한 10GB의 데이터를 사용합니다. Hello MapReduce Owen O'Malley 및 Arun Murthy에서 개발 된 응용 프로그램을 사용 합니다. 이러한 응용 프로그램 0.578 TB/min (173 분에서 100TB)의 속도와 2009 년에 hello 연간 범용 ("daytona") 테라바이트 정렬 벤치 마크를 획득 합니다. 이 및 다른 정렬 벤치 마크에 대 한 자세한 내용은 참조 hello [Sortbenchmark](http://sortbenchmark.org/) 사이트입니다.

이 샘플에서는 세 가지 집합의 MapReduce 프로그램을 사용합니다.

* **TeraGen**: toosort 데이터의 행을 생성 하는 MapReduce 프로그램

* **TeraSort**: hello 입력된 데이터를 샘플링 하 고 MapReduce toosort hello 데이터를 사용 하 여 총 주문으로

    TeraSort는 사용자 지정 파티셔너를 제외하고 표준 MapReduce 정렬입니다. hello 파티 셔 너 샘플링 N-1 키 hello 각 reduce에 대 한 키 범위를 정의 하는 정렬 된 목록을 사용 합니다. 특히, 모든 키 이러한 샘플 [i-1] < = k e y < 샘플 [i] tooreduce 보내집니다 i. 이 파티 셔이 너 hello 출력을 줄이려면 i + 1 보다 작은의 hello 출력 i 저하 있다는 보장이 모두 있습니다.

* **TeraValidate**: 해당 hello 출력의 유효성을 검사 하는 MapReduce 프로그램 전역적으로 정렬

    파일당 하나의 맵 hello 출력 디렉터리에 생성 하 고 각 지도 사용 하면 각 키 보다 작거나 같은 toohello 이전 합니다. hello 맵 함수 hello의 레코드를 먼저 생성 하 고 각 파일의 키를 마지막 합니다. reduce 함수 hello 해당 hello를 사용 하면 i 파일의 첫 번째 키 파일 i-1의 마지막 키 hello 보다 큽니다. 가 출력 되었지만 hello 잘못 hello 키가 있는 단계를 줄일 문제 보고 됩니다.

사용 하 여 hello 다음 단계 toogenerate 데이터를 정렬 하 고 hello 출력을 확인 합니다.

1. 10GB의 데이터 저장된 toohello HDInsight 클러스터의 기본 저장소는 생성에서 `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    hello `-Dmapred.map.tasks` 개수 맵 작업 toouse이이 작업에 대 한 Hadoop에 알려 줍니다. hello 마지막 두 매개 변수는 hello 작업 toocreate 지시 10GB의 데이터 및 toostore에서 `/example/data/10GB-sort-input`합니다.

2. 같은 명령 toosort hello 데이터가 hello를 사용 합니다.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    hello `-Dmapred.reduce.tasks` 수 줄이기 작업 toouse hello 작업에 대 한 Hadoop에 알려 줍니다. hello 마지막 두 매개 변수가 정당한 hello 입력 고 출력 데이터에 대 한 위치.

3. 같은 toovalidate hello 데이터가 hello 정렬에 의해 생성 된 hello를 사용 합니다.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>다음 단계

이 문서에서 어떻게 toorun hello 샘플에 포함 된 hello Linux 기반 HDInsight 클러스터에 배웠습니다. HDInsight Pig, Hive, 및 MapReduce 사용에 대 한 자습서, hello 다음 항목을 참조 하세요.

* [HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]
* [HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Hadoop과 MapReduce 사용][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
