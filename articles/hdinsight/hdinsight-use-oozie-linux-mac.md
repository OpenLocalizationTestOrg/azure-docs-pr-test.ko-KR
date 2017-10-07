---
title: "Linux 기반 HDInsight에서 Hadoop Oozie 워크플로 aaaUse | Microsoft Docs"
description: "Linux 기반 HDInsight에서 Hadoop Oozie를 사용합니다. 에 대해 알아봅니다 어떻게 toodefine Oozie 워크플로, Oozie 작업을 제출 하 고 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Hadoop toodefine 함께 Oozie를 사용 하 고 Linux 기반 HDInsight의 워크플로 실행 합니다.

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

자세한 내용은 방법 toouse Apache Oozie HDInsight에서 Hadoop으로 합니다. Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다. Oozie hello Hadoop 스택와 통합 하 고 작업을 수행 하는 hello 지원:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie는 tooschedule 사용 되는 작업은 Java 프로그램 또는 셸 스크립트와 같은 특정 tooa 시스템 될 수도 있습니다.

> [!NOTE]
> HDInsight를 사용하여 워크플로를 정의하는 또 다른 옵션은 Azure 데이터 팩터리입니다. Azure Data Factory에 대 한 자세한 toolearn 참조 [Data Factory와 사용 하 여 Pig 및 Hive][azure-data-factory-pig-hive]합니다.

> [!IMPORTANT]
> 도메인에 가입된 HDInsight에서는 Oozie를 사용할 수 없습니다.

## <a name="prerequisites"></a>필수 조건

* **HDInsight 클러스터**: [Linux에서 HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="example-workflow"></a>예제 워크플로

이 문서에 사용 된 hello 워크플로 두 가지 동작을 포함 합니다. 동작은 Hive, Sqoop, MapReduce 또는 기타 프로세스 실행과 같은 작업에 대한 정의입니다.

![워크플로 다이어그램][img-workflow-diagram]

1. 하이브 작업을 실행 HiveQL 스크립트 tooextract 레코드 hello에서 **hivesampletable** HDInsight에 포함 되어 있습니다. 데이터의 각 행은 특정 모바일 장치에서의 방문을 설명합니다. 레코드 형식 hello 텍스트 다음 유사한 toohello 나타납니다.

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    이 문서에 사용 된 Hive 스크립트 hello hello 각 플랫폼 (예: Android 또는 iPhone)에 대 한 총 방문 횟수를 계산 하 고 hello 개수 tooa 새 하이브 테이블을 저장 합니다.

    Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.

2. Sqoop 작업 hello 테이블의 내용을 hello 새 하이브 테이블 tooa Azure SQL 데이터베이스를 내보냅니다. Sqoop에 대한 자세한 내용은 [HDInsight에서 Hadoop Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.

> [!NOTE]
> HDInsight 클러스터에서 지원 되 Oozie 버전에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능][hdinsight-versions]합니다.

## <a name="create-hello-working-directory"></a>Hello 작업 디렉터리 만들기

Oozie에서는 동일한 hello에 작업 toobe 저장에 필요한 리소스 디렉터리입니다. 이 예에서는 **wasb:///tutorials/useoozie**를 사용합니다. 이 디렉터리와이 워크플로 통해 만든 hello 새 하이브 테이블을 보유 하는 hello 데이터 디렉터리 명령 toocreate 다음 hello를 사용 합니다.

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> hello `-p` 매개 변수 만든 hello 경로 toobe에 모든 디렉터리를 설정 합니다. hello **데이터** 디렉터리는 hello 사용 되는 사용 되는 toohold 데이터 **useooziewf.hql** 스크립트입니다.

또한 hello 다음 Oozie Hive 및 Sqoop 작업을 실행할 때 사용자 계정을 가장할 수 있도록 보장 하는 명령을 실행 합니다. **USERNAME** 을 로그인 이름으로 바꿉니다.

```
sudo adduser USERNAME users
```

> [!NOTE]
> 오류는 무시할 수 있습니다는 hello 사용자 hello의 멤버인 이미 `users` 그룹입니다.

## <a name="add-a-database-driver"></a>데이터베이스 드라이버 추가

이 워크플로 Sqoop tooexport 데이터 tooSQL 데이터베이스를 사용 하 tootalk tooSQL 데이터베이스를 사용 하는 hello JDBC 드라이버의 복사본을 제공 해야 합니다. 사용 하 여 hello 명령 toocopy 다음 그 toohello 작업 디렉터리:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

워크플로에서 사용 하 여 다른 리소스는 MapReduce 응용 프로그램을 포함 하는 jar 같은 뿐만 아니라 이러한 리소스 tooadd 해야 합니다.

## <a name="define-hello-hive-query"></a>Hello 하이브 쿼리를 정의 합니다.

다음 단계 toocreate이이 문서의 뒷부분에 나오는 Oozie 워크플로에서 사용 되는 쿼리를 정의 하는 HiveQL 스크립트 hello를 사용 합니다.

1. SSH를 사용 하 여 toohello 클러스터를 연결 합니다. hello 다음 명령은 한 예로 hello를 사용 하 여 `ssh` 명령입니다. 대체 __USERNAME__ hello 클러스터에 대 한 SSH 사용자 hello와 합니다. 대체 __CLUSTERNAME__ hello HDInsight 클러스터의 hello 이름을 사용 합니다.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. Hello SSH 연결에서에서 명령 toocreate 파일을 다음 hello를 사용 합니다.

    ```
    nano useooziewf.hql
    ```

3. Hello nano 편집기가 열리고 나면 hello hello 파일의 내용을 hello로 다음 쿼리를 사용 합니다.

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Hello 스크립트에 사용 되는 두 개의 변수 가지가 있습니다.

    * **${hiveTableName}**: hello 테이블 toobe 생성의 hello 이름을 포함

    * **${hiveDataFolder}**: hello 테이블에 대 한 hello 위치 toostore hello 데이터 파일 포함

    hello 워크플로 정의 파일 (이 자습서에서는 workflow.xml) 전달 이러한 값 toothis HiveQL 스크립트 런타임 시

4. tooexit hello 편집기 Ctrl-X를 누릅니다. 메시지가 나타나면 선택 **Y** toosave hello 파일을 다음 사용 하 여 **Enter** toouse hello **useooziewf.hql** 파일 이름입니다.

5. 사용 하 여 hello 다음 명령을 toocopy **useooziewf.hql** 너무**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    이러한 명령은 저장 hello **useooziewf.hql** hello 클러스터에 대 한 hello HDFS 호환 저장소 파일입니다.

## <a name="define-hello-workflow"></a>Hello 워크플로 정의 합니다.

Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성됩니다. 다음 단계 toodefine hello 워크플로 hello를 사용 합니다.

1. 다음 문은 toocreate hello를 사용 하 여 하 고 새 파일을 편집 합니다.

    ```
    nano workflow.xml
    ```

2. Hello nano 편집기가 열리고 나면 hello hello 파일 내용으로 다음과 같은 XML을 입력 합니다.

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
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
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

    Hello 워크플로에 정의 된 두 개의 작업이 있습니다.

   * **RunHiveScript**:이 hello 시작 작업은 작업과 hello 실행 **useooziewf.hql** 하이브 스크립트

   * **RunSqoopExport**:이 작업 실행 하 여 hello 하이브 스크립트 tooSQL에서 만든 hello 데이터 Sqoop를 사용 하 여 데이터베이스입니다. 경우 hello에이 작업 실행 **RunHiveScript** 작업은 성공 합니다.

     hello 워크플로에 여러 항목이 같은 `${jobTracker}`합니다. 이러한 항목은 hello 작업 정의에 사용 하는 값으로 대체 됩니다. hello 작업 정의이 문서의 뒷부분에 만들어집니다.

     또한 참고 hello `<archive>sqljdbc4.jar</arcive>` hello Sqoop 섹션의에서 항목입니다. 이 항목이이 작업이 실행 되 면 Oozie toomake Sqoop에 대 한이 보관을 지시 합니다.

3. 그런 다음 Ctrl-X를 사용 하 여 **Y** 및 **Enter** toosave hello 파일입니다.

4. 사용 하 여 hello 다음 명령은 toocopy hello **workflow.xml** 파일 너무**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Hello 데이터베이스 만들기

toocreate Azure SQL 데이터베이스에서에서 다음과 같이 hello hello [SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md) 문서. Hello 데이터베이스를 만들 때 사용 하 여 `oozietest` 으로 hello 데이터베이스의 이름입니다. 또한 기록해는 hello hello 데이터베이스 서버의 이름입니다.

### <a name="create-hello-table"></a>Hello 테이블 만들기

> [!NOTE]
> 여러 가지 방법 tooconnect tooSQL 데이터베이스 toocreate 테이블 있습니다. 다음 단계 사용 하 여 hello [FreeTDS](http://www.freetds.org/) hello HDInsight 클러스터에서 합니다.


1. Hello 명령 tooinstall FreeTDS hello HDInsight 클러스터에서 다음을 사용 합니다.

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. FreeTDS를 설치한 후 다음 이전에 만든 명령 tooconnect toohello SQL 데이터베이스 서버 hello를 사용 합니다.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    텍스트 다음 출력 유사한 toohello를 나타납니다.

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. Hello에 `1>` 프롬프트 hello 줄을 다음을 입력 합니다.

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Hello 때 `GO` hello 이전 문이 계산을 문을 입력 합니다. 이러한 문은 라는 테이블을 만들어 **mobiledata** hello 워크플로에서 사용 되는 합니다.

    다음 테이블 hello tooverify 사용 하 여 hello가 만들어졌습니다.

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    텍스트 다음 출력 유사한 toohello를 표시 됩니다.

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. 입력 `exit` hello에 `1>` tooexit hello tsql 유틸리티 메시지를 표시 합니다.

## <a name="create-hello-job-definition"></a>만들기 hello 작업 정의

hello 작업 정의 toofind workflow.xml hello 위치를 설명 합니다. 위치에 대해서도 설명 toofind (예: useooziewf.hql.) hello 워크플로에서 사용 되는 기타 파일 또한 hello 워크플로 내에서 사용 되는 속성과 관련 파일에 대 한 hello 값을 정의 합니다.

1. 다음 명령 tooget hello hello 기본 저장소의 전체 주소 hello를 사용 합니다. 이 주소는 잠시 후에 hello 구성 파일에서 사용 됩니다.

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    이 명령은 정보 비슷한 toohello를 다음과 같은 XML을 반환 합니다.

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Hello HDInsight 클러스터에서 hello 기본 저장소로 Azure 저장소를 사용 하는 경우 hello `<value>` 요소 내용을로 시작 `wasb://`합니다. Azure Data Lake Store를 대신 사용하면 `adl://`로 시작합니다.

    Hello의 hello 내용을 저장 `<value>` 요소가 hello 다음 단계에서 사용 됩니다.

2. 다음 명령 tooget hello 클러스터 헤드 노드에 대 한 FQDN hello를 사용 합니다. 이 정보는 hello hello 클러스터에 대 한 JobTracker 주소에 사용 됩니다.

    ```
    hostname -f
    ```

    정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    hello JobTracker hello에 사용 되는 포트는 8050, 이므로 JobTracker hello에 대 한 전체 주소 toouse hello `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`합니다.

3. 같은 toocreate hello Oozie 작업 정의 구성이 hello를 사용 합니다.

    ```
    nano job.xml
    ```

4. Hello nano 편집기가 열리고 나면 hello hello 파일의 내용을 hello로 다음과 같은 XML을 사용 합니다.

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
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
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * 모든 인스턴스가  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  기본 저장소에 이전에 나타난 hello 값을 사용 합니다.

     > [!WARNING]
     > Hello 경로 이면는 `wasb` 경로 hello 전체 경로 사용 해야 합니다. 줄이지 마십시오 것 toojust `wasb:///`합니다.

   * 대체 **JOBTRACKERADDRESS** 앞서 받은 JobTracker/ResourceManager 주소 hello로 합니다.
   * 대체 **YourName** hello HDInsight 클러스터에 대 한 로그인 이름을 사용 합니다.
   * 대체 **serverName**, **adminLogin**, 및 **adminPassword** Azure SQL 데이터베이스에 대 한 hello 정보입니다.

     대부분의이 파일의 hello 정보 (예: ${nameNode}.) hello workflow.xml 또는 ooziewf.hql 파일에 사용 되는 사용 되는 toopopulate hello 값은

     > [!NOTE]
     > hello **oozie.wf.application.path** 항목 위치를 정의 합니다.이 작업에 의해 hello 워크플로가 포함 된 toofind hello workflow.xml 파일을 실행 합니다.

5. 그런 다음 Ctrl-X를 사용 하 여 **Y** 및 **Enter** toosave hello 파일입니다.

## <a name="submit-and-manage-hello-job"></a>Hello 작업 관리 및 제출

hello 다음 단계 Oozie 명령 toosubmit hello를 사용 하 여 워크플로 및 관리 Oozie hello 클러스터에 있습니다. hello Oozie 명령을 hello를 통해 친숙 한 인터페이스는 [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)합니다.

> [!IMPORTANT]
> Hello Oozie 명령을 사용할 때에 hello HDInsight 헤드 노드에 대 한 FQDN hello를 사용 해야 합니다. 이 FQDN만 hello 클러스터에서 액세스할 수 있거나 경우 hello 클러스터 hello에 있는 다른 컴퓨터에서 Azure 가상 네트워크에서 동일한 네트워크입니다.


1. Hello tooobtain hello URL toohello Oozie 서비스를 사용 합니다.

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    이 정보 비슷한 toohello를 다음과 같은 XML을 반환 합니다.

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` 부분은 Oozie 명령 hello로 hello URL toouse입니다.

2. 사용 하 여 hello tootype 없는 환경 변수 toocreate hello URL에 대 한 다음 모든 명령에 대해:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    이전에 수신한 hello로 hello URL을 대체 합니다.
3. Toosubmit hello 작업을 수행 하는 hello를 사용 합니다.

    ```
    oozie job -config job.xml -submit
    ```

    이 명령은 hello 작업 정보를 로드 **job.xml** 하 고 제출 tooOozie, 하지만 실행 되지 않습니다.

    Hello 명령이 완료 되 면 hello 작업의 hello ID를 반환 합니다. 예: `0000005-150622124850154-oozie-oozi-W`. 이 ID가 사용 되는 toomanage hello 작업.

4. 다음 명령을 hello를 사용 하 여 hello 작업의 hello 상태를 봅니다.

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > 대체 `<JOBID>` hello로 hello 이전 단계에서 반환 된 ID입니다.

    정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    이 작업의 상태는 `PREP`입니다. 이 상태는 hello 작업 생성 되었지만 시작 되지 않습니다 나타냅니다.

5. 다음 명령 toostart hello 작업 hello를 사용 합니다.

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > 대체 `<JOBID>` hello로 ID 이전에 반환 합니다.

    이 명령은 후 hello 상태를 확인 하는 경우 실행 중 상태가 되며 hello 작업 내에서 hello 작업에 대 한 정보가 반환 됩니다.

6. Hello 작업이 성공적으로 완료 되 면 hello 데이터가 생성 된 및 명령을 다음 hello를 사용 하 여 toohello SQL 데이터베이스 테이블을 내보낸를 확인할 수 있습니다.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    Hello에 `1>` hello 다음 쿼리를 입력 합니다.

    ```
    SELECT * FROM mobiledata
    GO
    ```

    반환 된 hello 정보는 텍스트 다음 비슷한 toohello:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Hello Oozie 명령에 대 한 자세한 내용은 참조 하십시오. [Oozie 명령줄 도구](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html)합니다.

## <a name="oozie-rest-api"></a>Oozie REST API

hello Oozie REST API 사용 하면 toobuild Oozie를 사용 하는 고유한 도구입니다. hello 다음은 HDInsight hello Oozie REST API를 사용 하는 방법에 대 한 특정 정보입니다.

* **URI**: hello REST API에 hello 클러스터 외부에서 액세스할 수 있습니다`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **인증**: hello 클러스터 HTTP (관리자) 계정 및 암호를 사용 하 여 toohello API를 인증 합니다. 예:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Hello Oozie REST API 사용에 대 한 자세한 내용은 참조 하십시오. [Oozie 웹 서비스 API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)합니다.

## <a name="oozie-web-ui"></a>Oozie 웹 UI

hello Oozie 웹 UI hello 클러스터에 hello Oozie 작업 상태에 대 한 웹 기반 뷰를 제공합니다. hello 웹 UI를 통해 다음 정보는 tooview hello 있습니다.

* 작업 상태
* 작업 정의
* 구성
* Hello 작업에서 hello 동작이 그래프
* Hello 작업에 대 한 로그

또한 작업 내의 동작에 대한 세부 정보를 볼 수 있습니다.

tooaccess hello Oozie 웹 UI를 hello 다음 단계를 따르십시오.

1. SSH 터널 toohello HDInsight 클러스터를 만듭니다. 내용은 hello를 참조 하십시오. [사용 하 여 SSH 터널링 HDInsight와](hdinsight-linux-ambari-ssh-tunnel.md) 문서.

2. 가 채널을 만든 후 hello Ambari web UI 웹 브라우저에서 엽니다. hello Ambari 사이트에 대 한 hello URI는 **https://CLUSTERNAME.azurehdinsight.net**합니다. 대체 **CLUSTERNAME** Linux 기반 HDInsight 클러스터의 hello 이름의 합니다.

3. Hello hello 페이지의 왼쪽에서 선택 **Oozie**, 다음 **빠른 링크**, 마지막으로 **Oozie 웹 UI**합니다.

    ![hello 메뉴의 이미지](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. hello Oozie 웹 UI 기본값 toodisplaying 워크플로 작업을 실행 합니다. 모든 워크플로 작업을 선택 하는 toosee **모든 작업**합니다.

    ![모든 작업 표시](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. 작업 tooview hello 작업에 대 한 자세한 정보를 선택 합니다.

    ![작업 정보](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Hello 작업 정보 탭에서 기본 작업 정보 및 hello hello 작업 내의 개별 작업을 볼 수 있습니다. Hello 탭을 사용 하 여 볼 수는 hello 맨 hello 작업 정의 작업 구성 액세스 hello 작업 로그를 보거나 전달 된 비순환 그래프 (DAG) hello 작업의 합니다.

   * **작업 로그**: 선택 hello **GetLogs** tooget hello 작업에 대 한 모든 로그 단추 또는 hello를 사용 하 여 **입력 검색 필터** toofilter 로그 필드

       ![작업 로그](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: hello DAG는 hello 워크플로 통해 수행 하는 hello 데이터 경로 대 한 그래픽 개요

       ![작업 DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Hello에서 hello 작업 중 하나를 선택 하면 **작업 정보** 탭 hello 동작에 대 한 정보를 제공 합니다. 예를 들어 hello 선택 **RunHiveScript** 동작 합니다.

    ![동작 정보](./media/hdinsight-use-oozie-linux-mac/action.png)

8. 링크 toohello 같은 hello 동작에 대 한 정보를 볼 수 **콘솔 URL**합니다. 이 링크는 hello 작업에 대 한 사용된 tooview JobTracker 정보를 수 있습니다.

## <a name="scheduling-jobs"></a>작업 예약

hello 코디네이터 toospecify를 작업에 대 한 시작, 종료 및 발생 빈도 수 있습니다. toodefine hello 워크플로 사용 하 여 hello 다음 단계에 대 한 일정:

1. Toocreate 라는 파일을 다음 사용 하 여 hello **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Hello hello 파일의 내용을 hello로 다음과 같은 XML을 사용 합니다.

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > hello `${...}` 변수가 실행 시 hello 작업 정의의 값으로 대체 됩니다. hello 변수는 합니다.
    >
    > * `${coordFrequency}`: Hello 작업의 인스턴스를 실행 사이의 시간입니다.
    > ** `${coordStart}`: hello 작업 시작 시간입니다.
    > * `${coordEnd}`: hello 작업 종료 시간입니다.
    > * `${coordTimezone}`: 일광 절약 시간제(일반적으로 UTC를 사용하여 표시됨) 없이 고정된 표준 시간대에서 코디네이터 작업을 처리합니다. 이 표준 시간대 hello "Oozie 처리 표준 시간대입니다." 라고 합니다.
    > * `${wfPath}`: 경로 toohello workflow.xml hello 합니다.

2. toosave hello 파일, Ctrl-X를 사용 하 여 **Y**, 및 **Enter**합니다.

3. 다음 명령 toocopy hello 파일 toohello 작업 디렉터리가이 작업에 대 한 hello를 사용 합니다.

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. 사용 하 여 hello toomodify hello 다음 **job.xml** 파일:

    ```
    nano job.xml
    ```

    Hello 다음 변경 내용을 확인 하십시오.

   * hello 워크플로 변경 하는 대신 tooinstruct oozie toorun hello 코디네이터 파일 `<name>oozie.wf.application.path</name>` 너무`<name>oozie.coord.application.path</name>`합니다.

   * tooset hello `workflowPath` hello coordinator에 의해 사용 되는 변수는 다음과 같은 XML hello 추가:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Hello 대체 `wasb://mycontainer@mystorageaccount.blob.core.windows` hello job.xml 파일의 다른 항목에서 사용 하는 hello 값으로는 텍스트입니다.

   * toodefine hello 시작, 종료 및 hello coordinator 주파수 hello 다음과 같은 XML을 추가 합니다.

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       이러한 값은 시작 시간 too12 hello 설정: 2017 년 5 월 10 일 오후 00 hello 종료 시간, 12, tooMay 2017 합니다. 이 작업을 매일 실행에 대 한 hello 간격입니다. hello 빈도가 분, 24 시간 x 60 분의 1, 440 분 = 하므로 합니다. 마지막으로, 표준 시간대 hello tooUTC 설정 됩니다.

5. 그런 다음 Ctrl-X를 사용 하 여 **Y** 및 **Enter** toosave hello 파일입니다.

6. 다음 명령을 사용 하 여 hello toorun hello 작업:

    ```
    oozie job -config job.xml -run
    ```

    이 명령은 제출 하 고 hello 작업을 시작 합니다.

7. Hello Oozie 웹 UI를 방문 하 고 hello를 선택 하는 경우 **코디네이터 작업** 정보 비슷한 toohello 이미지 다음 참조 탭:

    ![코디네이터 작업 탭](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    hello **다음 구체화** 항목 다음에 작업 실행 hello hello 포함 되어 있습니다.

8. 비슷한 toohello hello 웹 UI에서에서 hello 작업 항목을 선택 하면 이전 워크플로 작업 hello 작업에서 정보를 표시 합니다.

    ![코디네이터 작업 정보](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > 이 이미지에는 예약 된 hello 워크플로 내에서 개별 동작 hello 작업의 성공적인 실행만 보여 줍니다. hello 중 하나를 선택 하는 toosee **동작** 항목입니다.

    ![동작 정보](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>문제 해결

hello Oozie UI tooview Oozie 로그 수 있습니다. 또한 hello 워크플로에 의해 시작 되는 MapReduce 작업에 대 한 링크 tooJobTracker 로그를 포함 합니다. 문제 해결에 대 한 hello 패턴 이어야 합니다.

1. Oozie 웹 UI에서 hello 작업 보기입니다.

2. 선택 하는 경우 hello 동작 toosee hello 없을 경우 오류 또는 특정 작업에 대 한 오류, **오류 메시지가** 필드 hello 실패 시 자세한 정보를 제공 합니다.

3. 사용 가능한 경우 hello URL 사용 hello 동작 tooview에서 자세한 정보 (예: JobTracker 로그의 경우) hello 동작에 대 한 합니다.

hello는 다음과 같은 특정 오류가 발생할 수 있습니다 및 방법을 tooresolve 해당 합니다.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: 클러스터를 초기화할 수 없음

**증상**: 작업 상태를 변경할 수를 너무 hello**SUSPENDED**합니다. Hello 작업에 대 한 세부 정보 표시로 hello RunHiveScript 상태 **START_MANUAL**합니다. Hello 동작을 선택 하면 hello 다음과 같은 오류 메시지가 표시 됩니다.

    JA009: Cannot initialize Cluster. Please check your configuration for map

**원인**: hello에 사용 되는 WASB 주소 hello **job.xml** 파일 hello 저장소 컨테이너 또는 저장소 계정 이름이 포함 되어 있지 않습니다. hello WASB 주소 형식 이어야 `wasb://containername@storageaccountname.blob.core.windows.net`합니다.

**해결 방법**: hello 작업에 의해 사용 되는 hello WASB 주소를 변경 합니다.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie tooimpersonate 허용 되지 않습니다 &lt;사용자 >

**증상**: 작업 상태를 변경할 수를 너무 hello**SUSPENDED**합니다. Hello 작업에 대 한 세부 정보 표시로 hello RunHiveScript 상태 **START_MANUAL**합니다. Hello 동작을 선택 하면 다음과 같은 오류 메시지가 hello 표시:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**원인**: 현재 사용 권한 설정을 Oozie 불가 tooimpersonate hello 사용자 계정을 지정 합니다.

**해상도**: Oozie hello에 tooimpersonate 사용자를 사용할 수 **사용자** 그룹입니다. 사용 하 여 hello `groups USERNAME` 사용자 계정을 hello toosee hello 그룹의 멤버인 합니다. Hello 사용자가 hello의 구성원이 아닌 경우 **사용자** 그룹에서 다음 명령 tooadd hello 사용자 toohello 그룹 hello를 사용 하 여:

    sudo adduser USERNAME users

> [!NOTE]
> HDInsight는 hello 추가 된 사용자 그룹 toohello 인식 하기 전에 몇 분 정도 걸릴 수 있습니다.

### <a name="launcher-error-sqoop"></a>시작 관리자 오류(Sqoop)

**증상**: 작업 상태를 변경할 수를 너무 hello**KILLED**합니다. Hello 작업에 대 한 세부 정보 표시로 hello RunSqoopExport 상태 **오류**합니다. Hello 동작을 선택 하면 다음과 같은 오류 메시지가 hello 표시:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**원인**: Sqoop 없습니다 tooload hello 데이터베이스 드라이버 필요한 tooaccess hello 데이터베이스입니다.

**해결 방법**: Sqoop Oozie 작업에서를 사용할 때 포함 해야 hello로 hello 데이터베이스 드라이버 hello 작업에서 사용 하는 다른 리소스 (예: hello workflow.xml). Hello에서 hello 데이터베이스 드라이버를 포함 하는 hello 보관 파일을 참조할 수도 `<sqoop>...</sqoop>` hello workflow.xml의 섹션입니다.

예를 들어이 문서에 대 한 일에 대 한 단계를 수행 하는 hello를 사용 합니다.

1. Hello sqljdbc4.1.jar 파일 toohello /tutorials/useoozie 디렉터리를 복사 합니다.

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Hello workflow.xml tooadd hello 위에 새 줄에 다음과 같은 XML을 수정 `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 방법에 대해 배웠습니다 toodefine Oozie 워크플로 방법과 toorun Oozie 작업 합니다. HDInsight 작업에 대해 자세히 toolearn hello 다음 문서 참조:

* [HDInsight에서 시간 기준의 Oozie 코디네이터 사용][hdinsight-oozie-coordinator-time]
* [HDInsight에서 Hadoop 작업용 데이터 업로드][hdinsight-upload-data]
* [HDInsight에서 Hadoop과 Sqoop 사용][hdinsight-use-sqoop]
* [HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]
* [HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
