---
title: "aaaUse HDInsight의 Hadoop Oozie 코디네이터 시간 기반 | Microsoft Docs"
description: "빅데이터 서비스인 HDInsight에서 시간 기준 Hadoop Oozie 코디네이터를 사용하는 방법을 알아봅니다. 자세한 방법을 toodefine Oozie 워크플로 및 코디네이터 및 작업을 제출 합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Hadoop으로 Oozie 코디네이터 시간 기반을 사용 하 여 HDInsight toodefine 워크플로에서 작업 및 작업
이 문서에서는 시간에 따라 toodefine 워크플로 및 코디네이터 및 tootrigger 코디네이터 작업 hello 하는 방법을 설명 합니다. 통해 유용한 toogo는 [HDInsight 사용 하 여 Oozie] [ hdinsight-use-oozie] 이 문서를 읽기 전에 합니다. 또한 tooOozie를 예약할 수도 있습니다 Azure 데이터 팩터리를 사용 하 여 작업 합니다. Azure Data Factory toolearn 참조 [Data Factory와 사용 하 여 Pig 및 Hive](../data-factory/data-factory-data-transformation-activities.md)합니다.

> [!NOTE]
> 이 문서를 사용하려면 Windows 기반 HDInsight 클러스터가 필요합니다. Linux 기반 클러스터에서 시간을 기준으로 작업을 비롯 한 Oozie를 사용 하는 방법은 참조 하십시오. [Hadoop toodefine 및 Linux 기반 HDInsight에서 워크플로 실행을 사용 하 여 Oozie](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Oozie 정의
Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다. Hello Hadoop 스택와도 통합 되어 하 고 Apache MapReduce Apache Pig, Apache Hive, Sqoop Apache Hadoop 작업을 지원 합니다. 사용 되는 tooschedule 작업은 Java 프로그램 셸 스크립트와 같은 특정 tooa 시스템 수도 있습니다.

hello 다음 그림이 보여줍니다 hello 워크플로 구현 합니다.

![워크플로 다이어그램][img-workflow-diagram]

hello 워크플로 두 개의 작업이 포함 되어 있습니다.

1. 하이브 작업 log4j 로그 파일에 HiveQL 스크립트 toocount hello 로그 수준 유형의 각 항목을 실행합니다. 예를 들어 [로그 수준] 필드 tooshow hello 유형 및 hello 심각도 포함 된 필드의 줄의 각 log4j 로그 구성 됩니다.

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    hello 하이브 스크립트 출력은 유사 합니다.

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.
2. Sqoop 작업 hello HiveQL 작업 출력 tooa 테이블을 Azure SQL 데이터베이스에서 내보냅니다. Sqoop에 대한 자세한 내용은 [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.

> [!NOTE]
> HDInsight 클러스터에서 지원 되 Oozie 버전에 대 한 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure PowerShell이 포함된 워크스테이션**.

    > [!IMPORTANT]
    > Azure 서비스 관리자를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거됩니다. Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.
    >
    > Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell. 해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.

* **HDInsight 클러스터**. HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기][hdinsight-provision] 또는 [HDInsight 시작][hdinsight-get-started]을 참조하세요. Hello 데이터 toogo hello 자습서를 통해 다음이 필요 합니다.

    <table border = "1">
    <tr><th>클러스터 속성</th><th>Windows PowerShell 변수 이름</th><th>값</th><th>설명</th></tr>
    <tr><td>HDInsight 클러스터 이름</td><td>$clusterName</td><td></td><td>hello HDInsight 클러스터는이 자습서를 실행 합니다.</td></tr>
    <tr><td>HDInsight 클러스터 사용자 이름</td><td>$clusterUsername</td><td></td><td>hello HDInsight 클러스터 사용자 이름입니다. </td></tr>
    <tr><td>HDInsight 클러스터 사용자 암호 </td><td>$clusterPassword</td><td></td><td>hello HDInsight 클러스터 사용자 암호입니다.</td></tr>
    <tr><td>Azure 저장소 계정 이름</td><td>$storageAccountName</td><td></td><td>Azure 저장소 계정 사용할 수 있는 toohello HDInsight 클러스터입니다. 이 자습서에 대 한 hello 클러스터 프로 비전 프로세스 중에 지정한 hello 기본 저장소 계정을 사용 합니다.</td></tr>
    <tr><td>Azure Blob 컨테이너 이름</td><td>$containerName</td><td></td><td>예를 들어 hello 기본 HDInsight 클러스터 파일 시스템에 사용 되는 hello Azure Blob 저장소 컨테이너를 사용 합니다. 기본적으로 hello hello HDInsight 클러스터와 동일한 이름을 가집니다.</td></tr>
    </table>
* **Azure SQL 데이터베이스**입니다. 워크스테이션에서 SQL 데이터베이스 서버 tooallow 액세스 hello에 대 한 방화벽 규칙을 구성 해야 합니다. Azure SQL 데이터베이스를 만들고 hello 방화벽을 구성 하는 방법에 대 한 지침은 [처음 사용 하는 Azure SQL 데이터베이스] [sql 데이터베이스-started]. 이 문서에서는이 자습서에 필요한 hello Azure SQL 데이터베이스 테이블을 만들기 위한 Windows PowerShell 스크립트를 제공 합니다.

    <table border = "1">
    <tr><th>SQL 데이터베이스 속성</th><th>Windows PowerShell 변수 이름</th><th>값</th><th>설명</th></tr>
    <tr><td>SQL 데이터베이스 서버 이름</td><td>$sqlDatabaseServer</td><td></td><td>hello SQL 데이터베이스 서버 toowhich Sqoop는 데이터를 내보냅니다. </td></tr>
    <tr><td>SQL 데이터베이스 로그인 이름</td><td>$sqlDatabaseLogin</td><td></td><td>SQL 데이터베이스 로그인 이름입니다.</td></tr>
    <tr><td>SQL 데이터베이스 로그인 암호</td><td>$sqlDatabaseLoginPassword</td><td></td><td>SQL 데이터베이스 로그인 암호입니다.</td></tr>
    <tr><td>SQL 데이터베이스 이름</td><td>$sqlDatabaseName</td><td></td><td>hello Azure SQL 데이터베이스 toowhich Sqoop는 데이터를 내보냅니다. </td></tr>
    </table>

  > [!NOTE]
  > 기본적으로 Azure SQL 데이터베이스는 Azure HDInsight 같은 Azure 서비스로부터의 연결을 허용합니다. 이 방화벽 설정을 사용 하지 않으면 hello Azure 포털에서에서 설정 해야 합니다. SQL Database 만들기 및 방화벽 규칙 구성에 대한 지침은 [SQL Database 만들기 및 구성][sqldatabase-get-started]을 참조하세요.

> [!NOTE]
> Hello 테이블의 채우기 hello 값입니다. 이 자습서를 완료하는 데 유용합니다.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Oozie 워크플로 정의 및 hello 관련 HiveQL 스크립트
Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성되었습니다. hello 기본 워크플로 파일 이름은 *workflow.xml*합니다.  다음 배포 toohello HDInsight 클러스터가이 자습서의 뒷부분에 나오는 Azure PowerShell을 사용 하 여 쿼리하고 hello 워크플로 파일을 로컬로 저장 합니다.

HiveQL 스크립트 파일을 호출 하는 hello hello 워크플로에서 하이브 동작 합니다. 이 스크립트 파일에는 세 개의 HiveQL 문이 포함되어 있습니다.

1. **DROP TABLE 문 hello** 있는 경우 삭제 hello log4j Hive 테이블입니다.
2. **CREATE TABLE 문 hello** log4j Hive 외부 테이블 hello log4j 로그 파일의 toohello 위치를 가리키는 만듭니다
3. **hello log4j 로그 파일의 위치를 hello**합니다. hello 필드 구분 기호는 ",". hello 기본 줄 구분은 "\n"입니다. 하이브 외부 테이블 toorun hello Oozie 워크플로 여러 번을 원하는 경우에 hello 원래 위치에서 제거 되 고 사용 되는 tooavoid hello 데이터 파일은.
4. **hello 덮어쓰기 삽입 문** 에서 각 로그 수준 형식의 hello 발생 수를 세 log4j Hive 테이블 hello와 hello 출력 tooan Azure Blob 저장소 위치를 저장 합니다.

> [!NOTE]
> 알려진 Hive 경로 문제가 있습니다. Oozie 작업을 제출할 때 이 문제가 발생합니다. hello TechNet Wiki에서 확인할 수 있습니다 hello 문제 해결에 대 한 지침을 hello: [HDInsight Hive 오류: 수 없습니다 toorename][technetwiki-hive-error]합니다.

**toodefine hello HiveQL 스크립트 파일 toobe hello 워크플로 통해 호출**

1. 콘텐츠를 수행 하는 hello로 텍스트 파일을 만듭니다.

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Hello 스크립트에 사용 되는 세 개의 변수 가지가 있습니다.

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     hello 워크플로 정의 파일 (이 자습서에서는 workflow.xml)는 런타임 시 이러한 값 toothis HiveQL 스크립트를 전달 합니다.
2. Hello 파일으로 저장 **C:\Tutorials\UseOozie\useooziewf.hql** ANSI (ASCII) 인코딩을 사용 하 여 합니다. (텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.) 이 스크립트 파일에는 hello 자습서의 뒷부분에 나오는 배포 toohello HDInsight 클러스터 됩니다.

**toodefine 워크플로**

1. 콘텐츠를 수행 하는 hello로 텍스트 파일을 만듭니다.

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    Hello 워크플로에 정의 된 두 가지 작업이 있습니다. hello 시작 tooaction은 *RunHiveScript*합니다. Hello 매크로 함수를 실행 하는 경우 *확인*, hello 다음 작업은 *RunSqoopExport*합니다.

    hello RunHiveScript는 여러 변수가 있습니다. Azure PowerShell을 사용 하 여 워크스테이션에서 hello Oozie 작업을 제출 하는 경우에 hello 값을 전달 합니다.

    워크플로 변수

    <table border = "1">
    <tr><th>워크플로 변수</th><th>설명</th></tr>
    <tr><td>${jobTracker}</td><td>Hello Hadoop 작업 트래커의 hello URL을 지정 합니다. HDInsight 클러스터 버전 3.0 및 2.0에는 <strong>jobtrackerhost:9010</strong>을 사용합니다.</td></tr>
    <tr><td>${nameNode}</td><td>Hello Hadoop 이름 노드의 hello URL을 지정 합니다. 기본 파일 시스템 wasb hello를 사용 하 여: / / 주소, 예를 들어 <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>합니다.</td></tr>
    <tr><td>${queueName}</td><td>에 제출할 작업 hello hello 큐 이름을 지정 합니다. <strong>기본값</strong>을 사용합니다.</td></tr>
    </table>

    Hive 작업 변수

    <table border = "1">
    <tr><th>Hive 작업 변수</th><th>설명</th></tr>
    <tr><td>${hiveDataFolder}</td><td>Create Table 하이브 명령 hello에 대 한 hello 소스 디렉터리입니다.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>hello 덮어쓰기 삽입 문 hello에 대 한 출력 폴더입니다.</td></tr>
    <tr><td>${hiveTableName}</td><td>hello log4j 데이터 파일을 참조 하는 hello Hive 테이블의 hello 이름입니다.</td></tr>
    </table>

    Sqoop 작업 변수

    <table border = "1">
    <tr><th>Sqoop 작업 변수</th><th>설명</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>SQL 데이터베이스 연결 문자열입니다.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>hello Azure SQL 데이터베이스 테이블 toowhere hello 데이터를 내보냅니다.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>하이브 덮어쓰기 삽입 문 hello에 대 한 hello 출력 폴더입니다. 이 hello hello Sqoop 내보내기 (내보내기-dir)에 대 한 같은 폴더입니다.</td></tr>
    </table>

    Oozie 워크플로 및 hello 워크플로 동작을 사용 하는 방법에 대 한 자세한 내용은 참조 [Apache Oozie 4.0 설명서] [ apache-oozie-400] (버전에 대 한 HDInsight 클러스터 3.0) 또는 [Apache Oozie 3.3.2 설명서] [ apache-oozie-332] (버전에 대 한 HDInsight 클러스터 2.1).

1. Hello 파일으로 저장 **C:\Tutorials\UseOozie\workflow.xml** ANSI (ASCII) 인코딩을 사용 하 여 합니다. (텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.)

**toodefine 코디네이터**

1. 콘텐츠를 수행 하는 hello로 텍스트 파일을 만듭니다.

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Hello 정의 파일에 사용 되는 다섯 개의 변수 가지가 있습니다.

   | 변수 | 설명 |
   | --- | --- |
   | ${coordFrequency} |작업 일시 중지 시간입니다. 빈도는 항상 분 단위로 표시됩니다. |
   | ${coordStart} |작업 시작 시간입니다. |
   | ${coordEnd} |작업 종료 시간입니다. |
   | ${coordTimezone} |Oozie는 일광 절약 시간제(UTC를 사용하여 일반적으로 표시 됨)없이 고정된 시간대에서 코디네이터 작업을 처리합니다. 이 표준 시간대 hello "Oozie 처리 표준 시간대입니다." 라고 합니다. |
   | ${wfPath} |hello workflow.xml에 대 한 hello 경로입니다.  Hello 워크플로 파일 이름을 hello 기본 파일 이름 (workflow.xml) 없는 경우에 지정 해야 합니다. |
2. Hello 파일으로 저장 **C:\Tutorials\UseOozie\coordinator.xml** hello ANSI (ASCII) 인코딩을 사용 하 여 합니다. (텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Hello Oozie 프로젝트를 배포 하 고 hello 자습서 준비
Azure PowerShell 스크립트 tooperform hello 다음을 실행 합니다.

* 복사 hello HiveQL 스크립트 (useoozie.hql) tooAzure Blob 저장소, wasb:///tutorials/useoozie/useoozie.hql 합니다.
* Workflow.xml toowasb:///tutorials/useoozie/workflow.xml를 복사 합니다.
* Coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml를 복사 합니다.
* 복사 hello 데이터 파일 (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log 합니다.
* Sqoop 내보내기 데이터를 저장할 Azure SQL 데이터베이스 테이블을 만듭니다. hello 테이블 이름이 *log4jLogCount*합니다.

**HDInsight 저장소 이해**

HDInsight는 데이터 저장소로 Azure Blob 저장소를 사용합니다. wasb: / /는 Microsoft의 Azure Blob 저장소에 hello distributed Hadoop 파일 시스템 (HDFS)의 구현입니다. 자세한 내용은 [HDInsight와 함께 Azure Blob Storage 사용][hdinsight-storage]을 참조하십시오.

HDInsight 클러스터를 프로 비전 할 때 Azure Blob 저장소 계정과 해당 계정에서 특정 컨테이너로 지정 됩니다 hello 기본 파일 시스템으로 같은 HDFS. 또한 toothis 저장소 계정을 추가할 수 있습니다 hello에서 추가 저장소 계정을 동일한 Azure 구독 또는 hello 프로 비전 프로세스 중 각기 다른 Azure 구독. 저장소 계정 추가에 대한 지침은 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요. 이 자습서에 사용 된 toosimplify hello Azure PowerShell 스크립트를 모두 hello 파일이 hello 기본 파일 시스템 컨테이너에 저장 된 위치에 */자습서/useoozie*합니다. 기본적으로이 컨테이너는 hello HDInsight 클러스터 이름을 이름이 hello에 있습니다.
hello 구문은 다음과 같습니다.

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Hello만 *wasb: / /* 구문을 HDInsight 클러스터 버전 3.0에서에서 사용할 수 있습니다. 이전 hello *asv: / /* 구문을 HDInsight 2.1와 1.6 클러스터에서 사용할 수 있지만 3.0 HDInsight 클러스터에서 지원 되지 않습니다.
>
> wasb hello: / / 경로 가상 경로입니다. 자세한 내용은 [HDInsight와 함께 Azure Blob Storage 사용][hdinsight-storage]을 참조하십시오.

Hello 기본 파일 시스템 컨테이너에 저장 된 파일의 Uri (사용 하 고 workflow.xml 예를 들어)를 수행 하는 hello를 사용 하 여 HDInsight에서 액세스할 수 있습니다.

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Hello 저장소 계정에서 직접 tooaccess hello 파일을 원하는 경우 hello blob hello 파일에 대 한 이름은 다음과 같습니다.

    tutorials/useoozie/workflow.xml

**Hive 내부 테이블 및 외부 테이블 이해**

몇 가지 방법으로 하이브 내부 및 외부 테이블에 대 한 tooknow 필요 합니다.

* CREATE TABLE 명령을 hello를 내부 테이블에는 관리 되는 테이블이 라고도 만듭니다. hello 기본 컨테이너에서 hello 데이터 파일이 있어야 합니다.
* CREATE TABLE 명령을 hello hello 데이터 toohello 파일/hive/웨어하우스/이동<TableName> hello 기본 컨테이너의 폴더입니다.
* CREATE EXTERNAL TABLE 명령 hello 외부 테이블을 만듭니다. hello 기본 컨테이너 외부 hello 데이터 파일이 위치할 수 있습니다.
* CREATE EXTERNAL TABLE 명령 hello hello 데이터 파일을 이동 하지 않습니다.
* CREATE EXTERNAL TABLE 명령 hello hello 위치 절에 지정 된 hello 폴더 아래의 하위 폴더도 모두를 허용 하지 않습니다. 이 hello 자습서 hello sample.log 파일의 복사본을 만들어 하는 이유는 hello 이유.

자세한 내용은 [HDInsight: Hive 내부 및 외부 테이블 소개][cindygross-hive-tables]를 참조하세요.

**tooprepare hello 자습서**

1. Windows PowerShell ISE 열기 hello (hello Windows 8 시작 화면에 입력 **PowerShell_ISE**, 클릭 하 고 **Windows PowerShell ISE**합니다. 자세한 내용은 [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start]을 참조하세요.)
2. Hello 아래쪽 창에 명령 tooconnect tooyour Azure 구독을 다음 hello를 실행 합니다.

    ```powershell
    Add-AzureAccount
    ```

    하면 Azure 계정 자격 증명된 tooenter 됩니다. 이 메서드는 구독 연결을 추가 하는 시간이 초과 있으며, 12 시간 후 있습니다 toorun hello cmdlet 다시 있습니다.

   > [!NOTE]
   > 여러 Azure 구독이 있는 hello 기본 구독이 지원 되지 않으면 원하는 toouse hello 사용 하 여 hello <strong>Select-azuresubscription</strong> cmdlet tooselect 구독 합니다.

3. Hello hello 스크립트 창에 스크립트를 다음 복사한 다음 hello 처음 여섯 개의 변수를 설정 합니다.

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    참조 hello에 대 한 자세한 설명은 hello 변수, [필수 구성 요소](#prerequisites) 이 자습서의 섹션입니다.

4. Hello toohello 스크립트 hello 스크립트 창에서 다음을 추가 합니다.

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. 클릭 **스크립트 실행** 하거나 키를 눌러 **F5** toorun hello 스크립트입니다. hello 출력 비슷합니다 됩니다.

    ![자습서 준비 출력][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Hello Oozie 프로젝트 실행
Azure PowerShell은 Oozie 작업을 정의하는 데 현재 어떤 cmdlet도 제공하지 않습니다. Hello를 사용할 수 있습니다 **Invoke-restmethod** cmdlet tooinvoke Oozie 웹 서비스입니다. hello Oozie 웹 서비스 API는 HTTP 나머지 JSON API. Hello Oozie 웹 서비스 API에 대 한 자세한 내용은 참조 [Apache Oozie 4.0 설명서] [ apache-oozie-400] (버전에 대 한 HDInsight 클러스터 3.0) 또는 [Apache Oozie 3.3.2 설명서] [ apache-oozie-332] (버전에 대 한 HDInsight 클러스터 2.1).

**toosubmit Oozie 작업**

1. 열기 hello Windows PowerShell ISE (Windows 8 시작 화면에 입력 **PowerShell_ISE**, 클릭 하 고 **Windows PowerShell ISE**합니다. 자세한 내용은 [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start]을 참조하세요.)
2. 그러나 복사 hello 다음 hello 스크립트 창으로 스크립팅 하 고 다음 집합 hello 먼저 14 개의 변수 (건너뛸 **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    참조 hello에 대 한 자세한 설명은 hello 변수, [필수 구성 요소](#prerequisites) 이 자습서의 섹션입니다.

    $coordstart 및 $coordend는 hello 워크플로 시작 및 종료 시간입니다. toofind hello UTC/GMT 시간 bing.com에 "utc 시간"을 검색 합니다. hello $coordFrequency toorun hello 워크플로에서 분 단위 빈도입니다.
3. Hello toohello 스크립트 다음에 추가 합니다. 이 부분 hello Oozie 페이로드를 정의합니다.

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > hello 주요한 차이점 비교 toohello 워크플로 제출 페이로드 파일은 hello 변수 **oozie.coord.application.path**합니다. 워크플로 작업을 제출할 때는 대신 **oozie.wf.application.path** 를 사용합니다.

4. Hello toohello 스크립트 다음에 추가 합니다. 이 부분 hello Oozie 웹 서비스 상태를 확인합니다.

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Hello toohello 스크립트 다음에 추가 합니다. 이 부분은 Oozie 작업을 만듭니다.

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > 워크플로 작업을 전송 하면 hello 작업이 만들어진 후에 다른 웹 서비스 호출 toostart hello 작업을 해야 합니다. 이 경우 hello 코디네이터 작업 시간에 의해 트리거됩니다. hello 작업이 자동으로 시작 됩니다.

6. Hello toohello 스크립트 다음에 추가 합니다. 이 부분 hello Oozie 작업 상태를 확인합니다.

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (선택 사항) Hello toohello 스크립트 다음에 추가 합니다.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Hello toohello 스크립트에 다음을 추가 합니다.

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Toorun hello에 대 한 추가 기능을 원하는 경우 hello # 기호를 제거 합니다.
9. HDinsight 클러스터 버전이 2.1인 경우 "https://$clusterName.azurehdinsight.net:443/oozie/v2/"를 "https://$clusterName.azurehdinsight.net:443/oozie/v1/"로 바꿉니다. HDInsight 클러스터 버전 2.1 지원의 버전이 아닌 2 hello 웹 서비스를 수행합니다.
10. 클릭 **스크립트 실행** 하거나 키를 눌러 **F5** toorun hello 스크립트입니다. hello 출력 비슷합니다 됩니다.

     ![자습서 실행 워크플로 출력][img-runworkflow-output]
11. Tooyour SQL 데이터베이스 toosee hello 내보낸 데이터를 연결 합니다.

**toocheck hello 작업 오류 로그**

워크플로 tootroubleshoot hello Oozie 로그 파일에 있습니다 C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log hello 클러스터 헤드 노드에에서 합니다. RDP에 대 한 자세한 내용은 참조 [관리 HDInsight 클러스터를 사용 하 여 Azure 포털 hello][hdinsight-admin-portal]합니다.

**toorerun hello 자습서**

toorerun hello 워크플로 hello 다음 작업을 수행 해야 합니다.

* Hello 하이브 스크립트 출력 파일을 삭제 합니다.
* Hello log4jLogsCount 테이블에서 hello 데이터를 삭제 합니다.

다음은 사용할 수 있는 Windows PowerShell 스크립트 샘플입니다:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>다음 단계
이 자습서에서는 방법에 대해 배웠습니다 toodefine Oozie 워크플로 및 Oozie 코디네이터 라면 및 Oozie 코디네이터 toorun Azure PowerShell을 사용 하 여 작업 하는 방법입니다. 더 toolearn hello 다음 문서를 참조:

* [HDInsight 시작][hdinsight-get-started]
* [HDInsight에서 Azure Blob Storage 사용][hdinsight-storage]
* [Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]
* [데이터 tooHDInsight 업로드][hdinsight-upload-data]
* [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]
* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
