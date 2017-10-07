---
title: "aaaMapReduce 및 Azure HDInsight에서 Hadoop으로 원격 데스크톱 | Microsoft Docs"
description: "자세한 방법을 toouse 원격 데스크톱 tooconnect tooHadoop HDInsight 및 MapReduce 작업을 실행된 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>원격 데스크톱을 사용하는 HDInsight에서 Hadoop과 MapReduce 사용
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

이 문서에서는 원격 데스크톱을 사용 하 여 tooconnect tooa HDInsight의 Hadoop 클러스터 하는 방법에 대해 알아봅니다 쿼리하고 hello Hadoop 명령을 사용 하 여 MapReduce 작업을 실행 합니다.

> [!IMPORTANT]
> 원격 데스크톱은 Windows 기반 HDInsight 클러스터에서만 사용할 수 있습니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.
>
> 예: HDInsight 3.4 또는 큰 참조 [SSH 사용 하 여 MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md) toohello HDInsight 클러스터를 연결 하 고 MapReduce 작업 실행에 대 한 내용은 합니다.

## <a id="prereq"></a>필수 조건
이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.

* Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터
* Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터

## <a id="connect"></a>원격 데스크톱을 사용하여 연결
Hello HDInsight 클러스터에 대 한 원격 데스크톱을 사용 합니다. 다음 hello 지침에 따라 tooit 연결 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.

## <a id="hadoop"></a>Hello Hadoop 명령을 사용 하 여
Hello HDInsight 클러스터에 연결 된 toohello 데스크톱 인 경우 hello Hadoop 명령을 사용 하 여 단계 toorun MapReduce 작업을 수행 하는 hello를 사용 합니다.

1. Hello HDInsight 바탕 화면에서 시작 hello **Hadoop 명령줄**합니다. 새 명령 프롬프트에서 hello 열립니다 **c:\apps\dist\hadoop-&lt;버전 번호 >** 디렉터리입니다.

   > [!NOTE]
   > hello 버전 번호는 Hadoop를 업데이트할 때 변경 됩니다. hello **HADOOP_HOME** 환경 변수 사용된 toofind hello 경로가 될 수 있습니다. 예를 들어 `cd %HADOOP_HOME%` tooknow hello 버전 번호를 요구 하지 않고 변경 내용 디렉터리 toohello Hadoop 디렉터리입니다.
   >
   >
2. toouse hello **Hadoop** toorun 예제 MapReduce 작업 명령에서 다음 명령을 hello를 사용 하 여:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Hello 시작 **wordcount** hello에 포함 되어 있는 클래스 **mapreduce hadoop-examples.jar** hello 현재 디렉터리의 파일입니다. 입력으로 사용 하 여 hello **wasb://example/data/gutenberg/davinci.txt** 문서 및 출력에 저장 됩니다: **wasb: / / / 예제/데이터/WordCountOutput**합니다.

   > [!NOTE]
   > 이 MapReduce 작업과 hello 예제 데이터에 대 한 자세한 내용은 참조 <a href="hdinsight-use-mapreduce.md">HDInsight Hadoop에서 사용 하 여 MapReduce</a>합니다.
   >
   >
3. 처리 되 고 hello 작업이 완료 되 면 유사한 toohello 다음 정보를 반환 hello 작업 세부 정보를 내보냅니다.

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. 다음 명령 toolist hello 출력 파일에 저장 하는 hello를 사용 하 여 hello 작업이 완료 되 면 **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    **_SUCCESS** 및 **part-r-00000**이라는 두 개의 파일이 표시됩니다. hello **파트-r-00000** 이 작업에 대 한 hello 출력 파일에 포함 되어 있습니다.

   > [!NOTE]
   > 일부 MapReduce 작업은 여러 hello 결과 분할할 수 **파트-r-# # #** 파일입니다. 이 경우 hello를 사용 하 여 # # # hello 파일의 tooindicate hello 순서가 접미사입니다.
   >
   >
5. 다음 명령을 사용 하 여 hello tooview hello 출력:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    그러면 목록이 포함 된 hello 단어 hello에 표시 됩니다 **wasb://example/data/gutenberg/davinci.txt** hello 각 단어 발생 한 횟수와 함께 파일입니다. hello 다음은 hello 파일에 포함 되어야 하는 hello 데이터의 예입니다.

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>요약
볼 수 있듯이 hello Hadoop 명령 쉽게 toorun MapReduce 작업에 제공 된 HDInsight 클러스터와 다음 보기 hello 작업 출력 합니다.

## <a id="nextsteps"></a>다음 단계
HDInsight의 MapReduce 작업에 대한 일반적인 정보:

* [HDInsight Hadoop에서 MapReduce 사용](hdinsight-use-mapreduce.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
