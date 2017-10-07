---
title: "aaaUse Hadoop 하이브 및 HDInsight-Azure의에서 원격 데스크톱 | Microsoft Docs"
description: "원격 데스크톱을 사용 하 여 HDInsight의 클러스터 tooconnect tooHadoop 방법을 알아보고 hello 하이브 명령줄 인터페이스를 사용 하 여 하이브 쿼리를 실행 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>원격 데스크톱을 사용하여 HDInsight에서 Hadoop과 Hive 사용
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

이 문서에서는 hello 하이브 명령줄 인터페이스 (CLI)를 사용 하 여 HDInsight 클러스터 원격 데스크톱을 사용 하 여 다음을 실행 하이브 tooconnect tooan 쿼리 하는 방법을 배웁니다.

> [!IMPORTANT]
> 원격 데스크톱은만 hello 운영 체제로 Windows를 사용 하는 HDInsight 클러스터에 사용할 수 있습니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.
>
> 참조에 대 한 HDInsight 3.4 또는 큰 [HDInsight Beeline와 사용 하 여 하이브](hdinsight-hadoop-use-hive-beeline.md) 명령줄에서 직접 hello 클러스터에서 하이브 쿼리 실행에 대 한 내용은 합니다.

## <a id="prereq"></a>필수 조건
이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.

* Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터
* Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터

## <a id="connect"></a>원격 데스크톱을 사용하여 연결
Hello HDInsight 클러스터에 대 한 원격 데스크톱을 사용 합니다. 다음 hello 지침에 따라 tooit 연결 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.

## <a id="hive"></a>Hello 하이브 명령을 사용 하 여
Hello HDInsight 클러스터에 대해 toohello 데스크톱에 연결 했으므로 때 하이브가 있는 toowork 단계를 수행 하는 hello를 사용 합니다.

1. Hello HDInsight 바탕 화면에서 시작 hello **Hadoop 명령줄**합니다.
2. Hello 명령 toostart hello 하이브 CLI 다음을 입력 합니다.

        %hive_home%\bin\hive

    나타납니다 hello CLI 시작 되 면 hello 하이브 CLI 프롬프트: `hive>`합니다.
3. Hello CLI를 사용 하 여 hello 문을 toocreate 라는 새 테이블을 다음 입력 **log4jLogs** 예제 데이터를 사용 하 여:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    이러한 문은 hello 다음 작업을 수행 합니다.

   * **DROP TABLE**: hello 테이블이 이미 있는 경우 hello 테이블 및 hello 데이터 파일을 삭제 합니다.
   * **CREATE EXTERNAL TABLE**: Hive에서 새 ‘외부’ 테이블을 만듭니다. 외부 테이블 (데이터는 hello 원래 위치에 그대로 남아 hello) 하이브에 hello 테이블 정의 저장 합니다.

     > [!NOTE]
     > 외부 소스 (예: 자동화 된 데이터 업로드 프로세스) 또는 다른 MapReduce 작업을 업데이트할 데이터 toobe 기본 hello 예상 으로만 toouse hello에 대 한 최신 데이터를 쿼리 하는 하이브 항상 하려는 경우 외부 테이블을 사용 해야 합니다.
     >
     > 외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.
     >
     >
   * **행 형식**: hello 데이터 형식 지정 방법을 하이브 알려 줍니다. 이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.
   * **AS 텍스트 파일 저장 위치**: hello 데이터를 하이브 지시 (hello 예제/데이터 디렉터리)를 저장 하 고 텍스트로 저장 됩니다.
   * **선택**: 모든 행의 개수를 선택 합니다. 여기서 열 **t4** hello 값이 포함 된 **[오류]**합니다. 이 경우 이 값을 포함하는 행이 3개 있으므로 **3** 값이 반환되어야 합니다.
   * **INPUT__FILE__NAME LIKE '%.log'** - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다. 이 제한 hello 검색 toohello sample.log 파일 hello 데이터가 포함 되 고 반환 하는 데이터 다른 예제에서 정의한 hello 스키마와 일치 하지 않는 데이터 파일 유지 됩니다.
4. 다음 문은 toocreate 라는 새 'internal' 테이블이 사용 하 여 hello **살펴볼**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    이러한 문은 hello 다음 작업을 수행 합니다.

   * **CREATE TABLE IF NOT EXISTS**: 테이블이 아직 없는 경우 테이블을 만듭니다. 때문에 hello **외부** 이 hello 하이브 데이터 웨어하우스에 저장 된 Hive에서 완전히 관리 되 고 있는 내부 테이블에는, 키워드가 사용 되지 않습니다.

     > [!NOTE]
     > 와 달리 **외부** hello 내부 데이터를 삭제 하는 테이블의 경우 내부 테이블도 삭제 합니다.
     >
     >
   * **AS ORC 저장**: 최적화 된 행의 열 (ORC) 형식의 hello 데이터를 저장 합니다. Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.
   * **덮어쓰기 삽입... 선택**: hello에서 행을 선택 **log4jLogs** 이 있는 테이블 **[오류]**, 삽입 hello에 데이터를 hello 다음 **살펴볼** 테이블입니다.

     포함 하는 행만 tooverify **[오류]** 열 t4 저장된 toohello 있었습니다 **살펴볼** 테이블에서 다음 행에서 hello 모든 문을 tooreturn hello를 사용 하 여 **살펴볼**:

       SELECT * from errorLogs;

     데이터 중 t4 열에 모두 **[ERROR]** 가 포함된 3개 행이 반환되어야 합니다.

## <a id="summary"></a>요약
볼 수 있듯이 hello hello 하이브 명령을 제공 하는 HDInsight 클러스터에서 하이브 쿼리를 실행 하는 쉽게 toointeractively, 모니터 hello 상태, 작업 및 hello 출력을 검색 합니다.

## <a id="nextsteps"></a>다음 단계
HDInsight의 Hive에 대한 일반적인 정보:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)

HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)

Tez 하이브가 있는 사용 하는 경우 hello 다음 디버깅 정보에 대 한 문서를 참조 하세요.

* [Windows 기반 HDInsight의 hello Tez UI를 사용 하 여](hdinsight-debug-tez-ui.md)
* [Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
