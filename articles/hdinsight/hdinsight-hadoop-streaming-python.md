---
title: "HDInsight-Azure와 aaaDevelop Python 스트리밍 MapReduce 작업 | Microsoft Docs"
description: "자세한 내용은 방법 스트리밍 MapReduce 작업에서 Python toouse 합니다. Hadoop은 Java 이외의 언어로 작성하기 위해 MapReduce용 스트리밍 API를 제공합니다."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>HDInsight용 Python 스트리밍 MapReduce 프로그램 개발

자세한 방법을 스트리밍 MapReduce 작업에서 Python toouse 합니다. Hadoop은 MapReduce Java 이외의 언어에서 함수를 줄이려면 없고 toowrite 지도 사용할 수에 대 한 스트리밍 API를 제공 합니다. hello이 문서의 단계 hello 맵 구현 및 Python에서 구성 요소를 줄입니다.

## <a name="prerequisites"></a>필수 조건

* HDInsight 클러스터의 Linux 기반 Hadoop

  > [!IMPORTANT]
  > 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* 텍스트 편집기

  > [!IMPORTANT]
  > hello 텍스트 편집기는 hello 줄 끝으로 LF를 사용 해야 합니다. CRLF의 줄 끝을 사용 하 여 Linux 기반 HDInsight 클러스터에서 hello MapReduce 작업을 실행할 때 오류가 발생 합니다.

* hello `ssh` 및 `scp` 명령, 또는 [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>단어 개수

이 예제는 매퍼와 리듀서를 사용하여 python에서 구현된 기본 단어 수입니다. hello 매퍼를 개별 단어로 문장을 분리 하며 hello 리 듀 서 hello 단어를 집계 하 고 tooproduce hello 출력을 계산 합니다.

hello 순서도 다음 단계를 줄이려면와 hello 맵 중 수행 되 보여 줍니다.

![hello mapreduce 프로세스의 그림](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>MapReduce 스트리밍

Hadoop toospecify를 파일 hello 맵을 포함 하는 작업에 의해 사용 되는 논리를 줄일 수 있습니다. hello hello에 대 한 특정 요구 사항 매핑 및 논리를 감소 됩니다.

* **입력**: 줄이고 지도 hello 구성 요소 STDIN에서 입력된 데이터를 읽어야 합니다.
* **출력**: 줄이고 지도 hello 구성 요소에 출력 데이터 tooSTDOUT 작성 해야 합니다.
* **데이터 형식**: hello 데이터를 사용 하 고 생성 되는 탭 문자로 구분 되는 키/값 쌍 이어야 합니다.

Python hello를 사용 하 여 이러한 요구 사항을 쉽게 처리할 수 `sys` STDIN 및 사용 하 여 모듈 tooread `print` tooprint tooSTDOUT 합니다. hello 나머지 작업은 단순히 서식 탭을 사용 하 여 hello 데이터 (`\t`) hello 키와 값 사이의 문자입니다.

## <a name="create-hello-mapper-and-reducer"></a>Hello 매퍼 및 리 듀 서 만들기

1. 라는 파일을 만들어 `mapper.py` 사용 하 여 hello hello 내용으로 코드를 다음 및:

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. 라는 파일을 만들어 **reducer.py** 사용 하 여 hello hello 내용으로 코드를 다음 및:

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a>PowerShell을 사용하여 실행

tooensure 파일 hello 오른쪽 줄 끝에 있는 PowerShell 스크립트 뒤 사용 하 여 hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

다음 PowerShell 스크립트 tooupload hello 파일이 hello를 사용 하 여, hello 작업을 실행 및 hello 출력을 보려면:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>SSH 세션에서 실행

1. 개발 환경에서의 hello 동일으로 디렉터리 `mapper.py` 및 `reducer.py` 파일을 hello 다음 명령을 사용 합니다.

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    대체 `username` 클러스터에 대 한 SSH 사용자 이름이 hello 및 `clustername` 클러스터의 hello 이름의 합니다.

    이 명령은 hello 로컬 시스템 toohello 헤드 노드에서 hello 파일을 복사합니다.

    > [!NOTE]
    > SSH 계정 암호 toosecure을 사용해 hello 암호에 대 한 메시지가 표시 됩니다. SSH 키를 사용한 경우 toouse hello `-i` 매개 변수 및 hello 경로 toohello 개인 키입니다. 예: `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. SSH를 사용 하 여 toohello 클러스터를 연결 합니다.

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. tooensure hello mapper.py 및 reducer.py 줄 끝을 hello 다음 명령을 사용 하 여 hello를 가집니다.

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. 명령 toostart hello MapReduce 작업을 수행 하는 hello를 사용 합니다.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    이 명령은 hello 부분 뒤에 있습니다.

   * **hadoop-streaming.jar**: 스트리밍 MapReduce 작업을 수행할 때 사용합니다. Hello 제공 하는 외부 MapReduce 코드로 Hadoop를 인터페이스입니다.

   * **-파일**: 지정 된 hello 추가 파일 toohello MapReduce 작업 합니다.

   * **-매퍼**: 지시 Hadoop 매퍼 hello toouse의 파일입니다.

   * **-리 듀 서**: 지시 Hadoop 리 듀 서 hello toouse의 파일입니다.

   * **-입력**:에서 단어 수를 계산 해야 하는 hello 입력된 파일입니다.

   * **-출력**: 출력 hello hello 디렉터리에 기록 됩니다.

    Hello MapReduce 작업을 개발할 때, hello 프로세스 백분율로 표시 됩니다.

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. 다음 명령을 사용 하 여 hello tooview hello 출력:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    이 명령은 발생 한 단어와 hello 단어에 몇 번의 목록이 표시 됩니다.

## <a name="next-steps"></a>다음 단계

이제 MapRedcue 스트리밍 toouse HDInsight와 작업 하는 방법을 설명 했습니다 hello 링크 tooexplore 다음 다른 방법으로 toowork와 함께 사용 하 Azure HDInsight 합니다.

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 MapReduce 작업 사용](hdinsight-use-mapreduce.md)
