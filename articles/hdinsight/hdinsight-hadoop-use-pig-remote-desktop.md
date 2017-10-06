---
title: "Hadoop Pig HDInsight-Azure의에서 원격 데스크톱 aaaUse | Microsoft Docs"
description: "Toouse HDInsight의 원격 데스크톱 연결 tooa Windows 기반 Hadoop 클러스터에서 Pig 명령 toorun Pig 라틴 문 hello 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>원격 데스크탑 연결에서 Pig 작업 실행
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

이 문서는 원격 데스크톱 연결 tooa Windows 기반 HDInsight 클러스터에서 hello Pig 명령 toorun Pig 라틴 문 사용에 대 한 연습을 제공 합니다. Pig 라틴 toocreate MapReduce 응용 프로그램 데이터 변환을 기반으로 하지 않고 매핑할 수 있으며 함수 줄일 합니다.

> [!IMPORTANT]
> 원격 데스크톱은만 hello 운영 체제로 Windows를 사용 하는 HDInsight 클러스터에 사용할 수 있습니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.
>
> HDInsight 3.4 또는 큰 참조 하십시오 [HDInsight 및 SSH와 Pig](hdinsight-hadoop-use-pig-ssh.md) Pig를 대화형으로 실행에 대 한 내용은 hello에 직접 작업 명령줄에서 클러스터입니다.

## <a id="prereq"></a>필수 조건
이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.

* Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터
* Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터

## <a id="connect"></a>원격 데스크톱을 사용하여 연결
Hello HDInsight 클러스터에 대 한 원격 데스크톱을 사용 합니다. 다음 hello 지침에 따라 tooit 연결 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.

## <a id="pig"></a>Hello Pig 명령을 사용 하 여
1. 원격 데스크톱 연결을 설정한 후 시작 hello **Hadoop 명령줄** hello 바탕 화면에서 hello 아이콘을 사용 하 여 합니다.
2. 다음 toostart hello Pig 명령을 hello를 사용 합니다.

        %pig_home%\bin\pig

    `grunt>` 프롬프트가 나타납니다.
3. Hello 문 다음을 입력 합니다.

        LOGS = LOAD 'wasb:///example/data/sample.log';

    이 명령은 hello 로그 파일에 hello sample.log 파일의 내용을 hello를 로드합니다. 다음 명령을 hello를 사용 하 여 hello 파일의 hello 내용을 볼 수 있습니다.

        DUMP LOGS;
4. 각 레코드에서 정규식 tooextract 유일한 hello 로깅 수준을 적용 하 여 hello 데이터를 변환 합니다.

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    사용할 수 있습니다 **덤프** hello 변환 후 tooview hello 데이터입니다. 이 예제의 경우 `DUMP LEVELS;`입니다.
5. 다음 조건 hello를 사용 하 여 변환을 계속 합니다. 사용 하 여 `DUMP` tooview hello 결과의 각 단계를 수행한 후 hello 변환 합니다.

    <table>
    <tr>
    <th>문</th><th>기능</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>Hello 로그 수준에 대 한 null 값을 포함 하는 행을 제거 하 고 FILTEREDLEVELS에 hello 결과 저장 합니다.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>그룹 hello 로그 수준에 따라 행 GROUPEDLEVELS에 hello 결과 저장 합니다.</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>고유한 각 로그 수준 값 및 발생 횟수를 포함하는 데이터의 새 집합을 만듭니다. FREQUENCIES에 저장됩니다.</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>횟수 (내림차순)와 저장소 hello 로그 수준에 결과 정렬</td>
    </tr>
    </table>
6.Hello를 사용 하 여 변환의 hello 결과 저장할 수도 있습니다 `STORE` 문. 예를 들어 다음 명령을 hello 저장 hello `RESULT` toohello **/example/data/pigout** 디렉터리에서 클러스터에 대 한 hello 기본 저장소 컨테이너:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > hello 데이터 hello 이라는 파일에 지정 된 디렉터리에 저장 됩니다 **파트 nnnnn**합니다. Hello 디렉터리가 이미 있는 경우는 오류 메시지가 표시 됩니다.
   >
   >
7. tooexit hello grunt 프롬프트를 hello 문 다음을 입력 합니다.

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin 배치 파일
또한 파일에 hello Pig 명령 toorun 포함 된 Pig 라틴 문자를 사용할 수 있습니다.

1. Hello grunt 프롬프트를 종료 한 후 엽니다 **메모장** 라는 새 파일을 만들고 **pigbatch.pig** hello에 **% PIG_HOME %** 디렉터리입니다.
2. Hello에 형식 또는 붙여넣기 hello 다음 줄 **pigbatch.pig** 파일을 선택한 다음 저장 합니다.

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. 사용 하 여 hello toorun hello 다음 **pigbatch.pig** hello pig 명령을 사용 하는 파일입니다.

        pig %PIG_HOME%\pigbatch.pig

    Hello 일괄 처리 작업이 완료 되 면 hello 출력 해야 수 hello 동일로 사용 하는 경우 다음이 표시 됩니다 `DUMP RESULT;` hello 이전 단계에서:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>요약
볼 수 있듯이 hello Pig 명령 있습니다 toointeractively를 MapReduce 작업을 실행 하거나 배치 파일에 저장 된 Pig 라틴 문자 작업을 실행 합니다.

## <a id="nextsteps"></a>다음 단계
HDInsight의 Pig에 대한 일반적인 정보:

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)
