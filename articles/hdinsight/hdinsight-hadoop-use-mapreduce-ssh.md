---
title: "aaaMapReduce 및 Azure HDInsight에서 Hadoop으로 SSH 연결 | Microsoft Docs"
description: "HDInsight에서 Hadoop을 사용 하 여 toouse SSH toorun MapReduce을 작업 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>SSH를 사용하여 HDInsight에서 Hadoop과 MapReduce 사용

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

SSH (보안 셸) 연결 tooHDInsight에서 MapReduce toosubmit 작업 하는 방법에 대해 알아봅니다.

> [!NOTE]
> 잘 알고 있는 경우 Linux 기반 Hadoop을 사용 하 여 서버에 있지만 새 tooHDInsight 참조 하십시오 [Linux 기반 HDInsight 팁](hdinsight-hadoop-linux-information.md)합니다.

## <a id="prereq"></a>필수 조건

* Linux 기반 HDInsight(HDInsight의 Hadoop) 클러스터

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* SSH 클라이언트. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a id="ssh"></a>SSH를 사용하여 연결

SSH를 사용 하 여 toohello 클러스터를 연결 합니다. 다음 명령을 hello 라는 tooa 클러스터를 연결 하는 예를 들어 **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**SSH 인증에 대 한 인증서 키를 사용 하는 경우**, hello 개인 키의 toospecify hello 위치 클라이언트 시스템에서 같이 할 수 있습니다.

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**SSH 인증에 대 한 암호를 사용 하는 경우**, 메시지가 표시 되 면 tooprovide hello 암호 필요 합니다.

HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a id="hadoop"></a>Hadoop 명령 사용

1. 연결 된 toohello HDInsight 클러스터를 한 후 명령 toostart MapReduce 작업을 수행 하는 hello를 사용 합니다.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    이 명령은 시작 hello `wordcount` hello에 포함 되어 있는 클래스 `hadoop-mapreduce-examples.jar` 파일입니다. Hello를 사용 하 여 `/example/data/gutenberg/davinci.txt` 입력 및 출력으로 문서에 저장 된 `/example/data/WordCountOutput`합니다.

    > [!NOTE]
    > 이 MapReduce 작업과 hello 예제 데이터에 대 한 자세한 내용은 참조 [HDInsight의 Hadoop에서 사용 하 여 MapReduce](hdinsight-use-mapreduce.md)합니다.

2. 처리 하 고 텍스트 hello 작업이 완료 되었을 때 다음 정보 비슷한 toohello 반환 hello 작업 세부 정보를 내보냅니다.

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Hello 작업이 완료 되 면 다음 명령 toolist hello 출력 파일이 hello를 사용 합니다.

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    이 명령은 `_SUCCESS` 및 `part-r-00000`의 두 개의 파일을 표시합니다. hello `part-r-00000` 이 작업에 대 한 hello 출력 파일에 포함 되어 있습니다.

    > [!NOTE]
    > 일부 MapReduce 작업은 여러 hello 결과 분할할 수 **파트-r-# # #** 파일입니다. 이 경우 hello를 사용 하 여 # # # hello 파일의 tooindicate hello 순서가 접미사입니다.

4. 다음 명령을 사용 하 여 hello tooview hello 출력:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    이 명령은 hello에 포함 된 hello 단어의 목록을 표시 **wasb://example/data/gutenberg/davinci.txt** 파일과 hello 각 단어 발생 한 횟수입니다. hello 다음 텍스트는 hello 파일에 포함 된 hello 데이터의 예입니다.

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>요약

볼 수 있듯이 Hadoop 명령은 제공 쉽게 toorun는 HDInsight 클러스터와 다음 hello 작업 출력 보기에 있는 MapReduce 작업 합니다.

## <a id="nextsteps"></a>다음 단계

HDInsight의 MapReduce 작업에 대한 일반적인 정보:

* [HDInsight Hadoop에서 MapReduce 사용](hdinsight-use-mapreduce.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
