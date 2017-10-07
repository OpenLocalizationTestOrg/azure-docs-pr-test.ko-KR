---
title: "-Azure HDInsight 클러스터에서 Hadoop Pig SSH와 aaaUse | Microsoft Docs"
description: "자세한 내용은 SSH와 tooa Linux 기반 Hadoop 클러스터를 연결 하는 방법 및 다음 사용 하 여 hello Pig 명령 toorun Pig 라틴 문을 대화형으로 또는 일괄 처리로 작업 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Hello Pig 명령 SSH ()를 사용 하 여 Linux 기반 클러스터에서 Pig 작업을 실행

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Toointeractively SSH 연결 tooyour HDInsight 클러스터에서 Pig 작업을 실행 하는 방법에 대해 알아봅니다. hello Pig 라틴 프로그래밍 언어에는 적용 된 toohello 입력 데이터 tooproduce hello 원하는 출력 toodescribe 변환을 허용 합니다.

> [!IMPORTANT]
> hello이 문서의 단계는 Linux 기반 HDInsight 클러스터가 필요합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a id="ssh"></a>SSH를 사용하여 연결

SSH tooconnect tooyour HDInsight 클러스터를 사용 합니다. hello 다음 예제에서는 tooa 클러스터 연결 라는 **myhdinsight** hello 계정인으로 **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**SSH 인증에 대 한 인증서 키를 제공한 경우** hello HDInsight 클러스터를 만든 경우 클라이언트 시스템에서 hello 개인 키의 toospecify hello 위치를 할 수 있습니다.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**SSH 인증을 위해 암호를 제공 하는 경우** hello HDInsight 클러스터를 만들 때 메시지가 표시 되 면 hello 암호를 제공 합니다.

HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a id="pig"></a>Hello Pig 명령을 사용 하 여

1. 연결 되 면 다음 명령을 hello를 사용 하 여 hello Pig CLI (명령줄 인터페이스)를 시작 합니다.

        pig

    잠시 후 `grunt>` 프롬프트가 표시됩니다.

2. Hello 문 다음을 입력 합니다.

        LOGS = LOAD '/example/data/sample.log';

    이 명령은 로그 hello sample.log 파일의 hello 내용을 로드합니다. 문 다음 hello를 사용 하 여 hello 파일의 hello 내용을 볼 수 있습니다.

        DUMP LOGS;

3. 문 다음 hello를 사용 하 여 각 레코드에서 정규식 tooextract 유일한 hello 로깅 수준을 적용 하 여 hello 데이터를 다음으로 변환 합니다.

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    사용할 수 있습니다 **덤프** hello 변환 후 tooview hello 데이터입니다. 이 예제의 경우 `DUMP LEVELS;`입니다.

4. 다음 표에 hello에 hello 문을 사용 하 여 변환을 계속:

    | Pig Latin 문 | 어떤 hello 문은 수행 |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Hello 로그 수준에 대 한 null 값을 포함 하는 행을 제거 하 고 hello 결과를 저장 `FILTEREDLEVELS`합니다. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | 로그 수준에 따라 행 하 고 hello 결과를 저장 하는 그룹 hello `GROUPEDLEVELS`합니다. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | 고유한 각 로그 수준 값 및 발생 횟수를 포함하는 데이터 집합을 만듭니다. hello 데이터 집합에 저장 될 `FREQUENCIES`합니다. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Hello 로그 수준 count (내림차순)을 기준으로 정렬 하 고로 저장 `RESULT`합니다. |

    > [!TIP]
    > 사용 하 여 `DUMP` tooview hello 결과의 각 단계를 수행한 후 hello 변환 합니다.

5. Hello를 사용 하 여 변환의 hello 결과 저장할 수도 있습니다 `STORE` 문. 예를 들어 다음 문의 hello 저장 hello `RESULT` toohello `/example/data/pigout` hello 기본 저장소 클러스터에 대 한 디렉터리:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > hello 데이터 hello 이라는 파일에 지정 된 디렉터리에 저장 됩니다 `part-nnnnn`합니다. Hello 디렉터리가 이미 있으면 오류가 발생 합니다.

6. tooexit hello grunt 프롬프트를 hello 문 다음을 입력 합니다.

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin 배치 파일

Hello Pig 명령 toorun 파일에 포함 된 Pig 라틴 문자를 사용할 수 있습니다.

1. Hello grunt 프롬프트를 종료 한 후 사용 하 여 hello 다음 명령은 라는 파일로 STDIN toopipe `pigbatch.pig`합니다. 이 파일은 hello hello SSH 사용자 계정에 대 한 홈 디렉터리에 만들어집니다.

        cat > ~/pigbatch.pig

2. 입력 또는 hello 다음 줄을 붙여 하 고 완료 되 면 Ctrl + D를 사용 합니다.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. 사용 하 여 hello 다음 명령은 toorun hello `pigbatch.pig` hello Pig 명령을 사용 하 여 파일입니다.

        pig ~/pigbatch.pig

    Hello 일괄 처리 작업이 완료 되 면 hello 출력을 따라 표시 됩니다.

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>다음 단계

Pig HDInsight에 대 한 일반 정보를 hello 문서 다음을 참조 하세요.

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)

HDInsight에서 Hadoop으로 다른 방법으로 toowork에 자세한 내용은 다음 문서는 hello 참조:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)
