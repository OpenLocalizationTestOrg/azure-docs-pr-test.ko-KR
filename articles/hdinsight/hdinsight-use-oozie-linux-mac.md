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
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="93c2c-104">Hadoop toodefine 함께 Oozie를 사용 하 고 Linux 기반 HDInsight의 워크플로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="93c2c-105">자세한 내용은 방법 toouse Apache Oozie HDInsight에서 Hadoop으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="93c2c-106">Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="93c2c-107">Oozie hello Hadoop 스택와 통합 하 고 작업을 수행 하는 hello 지원:</span><span class="sxs-lookup"><span data-stu-id="93c2c-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="93c2c-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="93c2c-108">Apache MapReduce</span></span>
* <span data-ttu-id="93c2c-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="93c2c-109">Apache Pig</span></span>
* <span data-ttu-id="93c2c-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="93c2c-110">Apache Hive</span></span>
* <span data-ttu-id="93c2c-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="93c2c-111">Apache Sqoop</span></span>

<span data-ttu-id="93c2c-112">Oozie는 tooschedule 사용 되는 작업은 Java 프로그램 또는 셸 스크립트와 같은 특정 tooa 시스템 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="93c2c-113">HDInsight를 사용하여 워크플로를 정의하는 또 다른 옵션은 Azure 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="93c2c-114">Azure Data Factory에 대 한 자세한 toolearn 참조 [Data Factory와 사용 하 여 Pig 및 Hive][azure-data-factory-pig-hive]합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93c2c-115">도메인에 가입된 HDInsight에서는 Oozie를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93c2c-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93c2c-116">Prerequisites</span></span>

* <span data-ttu-id="93c2c-117">**HDInsight 클러스터**: [Linux에서 HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="93c2c-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="93c2c-118">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="93c2c-119">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="93c2c-120">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93c2c-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="93c2c-121">예제 워크플로</span><span class="sxs-lookup"><span data-stu-id="93c2c-121">Example workflow</span></span>

<span data-ttu-id="93c2c-122">이 문서에 사용 된 hello 워크플로 두 가지 동작을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="93c2c-123">동작은 Hive, Sqoop, MapReduce 또는 기타 프로세스 실행과 같은 작업에 대한 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![워크플로 다이어그램][img-workflow-diagram]

1. <span data-ttu-id="93c2c-125">하이브 작업을 실행 HiveQL 스크립트 tooextract 레코드 hello에서 **hivesampletable** HDInsight에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="93c2c-126">데이터의 각 행은 특정 모바일 장치에서의 방문을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="93c2c-127">레코드 형식 hello 텍스트 다음 유사한 toohello 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="93c2c-128">이 문서에 사용 된 Hive 스크립트 hello hello 각 플랫폼 (예: Android 또는 iPhone)에 대 한 총 방문 횟수를 계산 하 고 hello 개수 tooa 새 하이브 테이블을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="93c2c-129">Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93c2c-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="93c2c-130">Sqoop 작업 hello 테이블의 내용을 hello 새 하이브 테이블 tooa Azure SQL 데이터베이스를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="93c2c-131">Sqoop에 대한 자세한 내용은 [HDInsight에서 Hadoop Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93c2c-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="93c2c-132">HDInsight 클러스터에서 지원 되 Oozie 버전에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능][hdinsight-versions]합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="93c2c-133">Hello 작업 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="93c2c-133">Create hello working directory</span></span>

<span data-ttu-id="93c2c-134">Oozie에서는 동일한 hello에 작업 toobe 저장에 필요한 리소스 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="93c2c-135">이 예에서는 **wasb:///tutorials/useoozie**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="93c2c-136">이 디렉터리와이 워크플로 통해 만든 hello 새 하이브 테이블을 보유 하는 hello 데이터 디렉터리 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="93c2c-137">hello `-p` 매개 변수 만든 hello 경로 toobe에 모든 디렉터리를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="93c2c-138">hello **데이터** 디렉터리는 hello 사용 되는 사용 되는 toohold 데이터 **useooziewf.hql** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="93c2c-139">또한 hello 다음 Oozie Hive 및 Sqoop 작업을 실행할 때 사용자 계정을 가장할 수 있도록 보장 하는 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="93c2c-140">**USERNAME** 을 로그인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="93c2c-141">오류는 무시할 수 있습니다는 hello 사용자 hello의 멤버인 이미 `users` 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="93c2c-142">데이터베이스 드라이버 추가</span><span class="sxs-lookup"><span data-stu-id="93c2c-142">Add a database driver</span></span>

<span data-ttu-id="93c2c-143">이 워크플로 Sqoop tooexport 데이터 tooSQL 데이터베이스를 사용 하 tootalk tooSQL 데이터베이스를 사용 하는 hello JDBC 드라이버의 복사본을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="93c2c-144">사용 하 여 hello 명령 toocopy 다음 그 toohello 작업 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="93c2c-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="93c2c-145">워크플로에서 사용 하 여 다른 리소스는 MapReduce 응용 프로그램을 포함 하는 jar 같은 뿐만 아니라 이러한 리소스 tooadd 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="93c2c-146">Hello 하이브 쿼리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-146">Define hello Hive query</span></span>

<span data-ttu-id="93c2c-147">다음 단계 toocreate이이 문서의 뒷부분에 나오는 Oozie 워크플로에서 사용 되는 쿼리를 정의 하는 HiveQL 스크립트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="93c2c-148">SSH를 사용 하 여 toohello 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="93c2c-149">hello 다음 명령은 한 예로 hello를 사용 하 여 `ssh` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="93c2c-150">대체 __USERNAME__ hello 클러스터에 대 한 SSH 사용자 hello와 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="93c2c-151">대체 __CLUSTERNAME__ hello HDInsight 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="93c2c-152">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93c2c-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="93c2c-153">Hello SSH 연결에서에서 명령 toocreate 파일을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="93c2c-154">Hello nano 편집기가 열리고 나면 hello hello 파일의 내용을 hello로 다음 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="93c2c-155">Hello 스크립트에 사용 되는 두 개의 변수 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="93c2c-156">**${hiveTableName}**: hello 테이블 toobe 생성의 hello 이름을 포함</span><span class="sxs-lookup"><span data-stu-id="93c2c-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="93c2c-157">**${hiveDataFolder}**: hello 테이블에 대 한 hello 위치 toostore hello 데이터 파일 포함</span><span class="sxs-lookup"><span data-stu-id="93c2c-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="93c2c-158">hello 워크플로 정의 파일 (이 자습서에서는 workflow.xml) 전달 이러한 값 toothis HiveQL 스크립트 런타임 시</span><span class="sxs-lookup"><span data-stu-id="93c2c-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="93c2c-159">tooexit hello 편집기 Ctrl-X를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="93c2c-160">메시지가 나타나면 선택 **Y** toosave hello 파일을 다음 사용 하 여 **Enter** toouse hello **useooziewf.hql** 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="93c2c-161">사용 하 여 hello 다음 명령을 toocopy **useooziewf.hql** 너무**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="93c2c-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="93c2c-162">이러한 명령은 저장 hello **useooziewf.hql** hello 클러스터에 대 한 hello HDFS 호환 저장소 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="93c2c-163">Hello 워크플로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-163">Define hello workflow</span></span>

<span data-ttu-id="93c2c-164">Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="93c2c-165">다음 단계 toodefine hello 워크플로 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="93c2c-166">다음 문은 toocreate hello를 사용 하 여 하 고 새 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="93c2c-167">Hello nano 편집기가 열리고 나면 hello hello 파일 내용으로 다음과 같은 XML을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

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

    <span data-ttu-id="93c2c-168">Hello 워크플로에 정의 된 두 개의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="93c2c-169">**RunHiveScript**:이 hello 시작 작업은 작업과 hello 실행 **useooziewf.hql** 하이브 스크립트</span><span class="sxs-lookup"><span data-stu-id="93c2c-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="93c2c-170">**RunSqoopExport**:이 작업 실행 하 여 hello 하이브 스크립트 tooSQL에서 만든 hello 데이터 Sqoop를 사용 하 여 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="93c2c-171">경우 hello에이 작업 실행 **RunHiveScript** 작업은 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="93c2c-172">hello 워크플로에 여러 항목이 같은 `${jobTracker}`합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="93c2c-173">이러한 항목은 hello 작업 정의에 사용 하는 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="93c2c-174">hello 작업 정의이 문서의 뒷부분에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="93c2c-175">또한 참고 hello `<archive>sqljdbc4.jar</arcive>` hello Sqoop 섹션의에서 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="93c2c-176">이 항목이이 작업이 실행 되 면 Oozie toomake Sqoop에 대 한이 보관을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="93c2c-177">그런 다음 Ctrl-X를 사용 하 여 **Y** 및 **Enter** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="93c2c-178">사용 하 여 hello 다음 명령은 toocopy hello **workflow.xml** 파일 너무**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="93c2c-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="93c2c-179">Hello 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="93c2c-179">Create hello database</span></span>

<span data-ttu-id="93c2c-180">toocreate Azure SQL 데이터베이스에서에서 다음과 같이 hello hello [SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="93c2c-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="93c2c-181">Hello 데이터베이스를 만들 때 사용 하 여 `oozietest` 으로 hello 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="93c2c-182">또한 기록해는 hello hello 데이터베이스 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="93c2c-183">Hello 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="93c2c-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="93c2c-184">여러 가지 방법 tooconnect tooSQL 데이터베이스 toocreate 테이블 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="93c2c-185">다음 단계 사용 하 여 hello [FreeTDS](http://www.freetds.org/) hello HDInsight 클러스터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="93c2c-186">Hello 명령 tooinstall FreeTDS hello HDInsight 클러스터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="93c2c-187">FreeTDS를 설치한 후 다음 이전에 만든 명령 tooconnect toohello SQL 데이터베이스 서버 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="93c2c-188">텍스트 다음 출력 유사한 toohello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="93c2c-189">Hello에 `1>` 프롬프트 hello 줄을 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="93c2c-190">Hello 때 `GO` hello 이전 문이 계산을 문을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="93c2c-191">이러한 문은 라는 테이블을 만들어 **mobiledata** hello 워크플로에서 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="93c2c-192">다음 테이블 hello tooverify 사용 하 여 hello가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="93c2c-193">텍스트 다음 출력 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="93c2c-194">입력 `exit` hello에 `1>` tooexit hello tsql 유틸리티 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="93c2c-195">만들기 hello 작업 정의</span><span class="sxs-lookup"><span data-stu-id="93c2c-195">Create hello job definition</span></span>

<span data-ttu-id="93c2c-196">hello 작업 정의 toofind workflow.xml hello 위치를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="93c2c-197">위치에 대해서도 설명 toofind (예: useooziewf.hql.) hello 워크플로에서 사용 되는 기타 파일 또한 hello 워크플로 내에서 사용 되는 속성과 관련 파일에 대 한 hello 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="93c2c-198">다음 명령 tooget hello hello 기본 저장소의 전체 주소 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="93c2c-199">이 주소는 잠시 후에 hello 구성 파일에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="93c2c-200">이 명령은 정보 비슷한 toohello를 다음과 같은 XML을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="93c2c-201">Hello HDInsight 클러스터에서 hello 기본 저장소로 Azure 저장소를 사용 하는 경우 hello `<value>` 요소 내용을로 시작 `wasb://`합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="93c2c-202">Azure Data Lake Store를 대신 사용하면 `adl://`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="93c2c-203">Hello의 hello 내용을 저장 `<value>` 요소가 hello 다음 단계에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="93c2c-204">다음 명령 tooget hello 클러스터 헤드 노드에 대 한 FQDN hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="93c2c-205">이 정보는 hello hello 클러스터에 대 한 JobTracker 주소에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="93c2c-206">정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="93c2c-207">hello JobTracker hello에 사용 되는 포트는 8050, 이므로 JobTracker hello에 대 한 전체 주소 toouse hello `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="93c2c-208">같은 toocreate hello Oozie 작업 정의 구성이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="93c2c-209">Hello nano 편집기가 열리고 나면 hello hello 파일의 내용을 hello로 다음과 같은 XML을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

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

   * <span data-ttu-id="93c2c-210">모든 인스턴스가  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  기본 저장소에 이전에 나타난 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="93c2c-211">Hello 경로 이면는 `wasb` 경로 hello 전체 경로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="93c2c-212">줄이지 마십시오 것 toojust `wasb:///`합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="93c2c-213">대체 **JOBTRACKERADDRESS** 앞서 받은 JobTracker/ResourceManager 주소 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="93c2c-214">대체 **YourName** hello HDInsight 클러스터에 대 한 로그인 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="93c2c-215">대체 **serverName**, **adminLogin**, 및 **adminPassword** Azure SQL 데이터베이스에 대 한 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="93c2c-216">대부분의이 파일의 hello 정보 (예: ${nameNode}.) hello workflow.xml 또는 ooziewf.hql 파일에 사용 되는 사용 되는 toopopulate hello 값은</span><span class="sxs-lookup"><span data-stu-id="93c2c-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="93c2c-217">hello **oozie.wf.application.path** 항목 위치를 정의 합니다.이 작업에 의해 hello 워크플로가 포함 된 toofind hello workflow.xml 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="93c2c-218">그런 다음 Ctrl-X를 사용 하 여 **Y** 및 **Enter** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="93c2c-219">Hello 작업 관리 및 제출</span><span class="sxs-lookup"><span data-stu-id="93c2c-219">Submit and manage hello job</span></span>

<span data-ttu-id="93c2c-220">hello 다음 단계 Oozie 명령 toosubmit hello를 사용 하 여 워크플로 및 관리 Oozie hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="93c2c-221">hello Oozie 명령을 hello를 통해 친숙 한 인터페이스는 [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93c2c-222">Hello Oozie 명령을 사용할 때에 hello HDInsight 헤드 노드에 대 한 FQDN hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="93c2c-223">이 FQDN만 hello 클러스터에서 액세스할 수 있거나 경우 hello 클러스터 hello에 있는 다른 컴퓨터에서 Azure 가상 네트워크에서 동일한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="93c2c-224">Hello tooobtain hello URL toohello Oozie 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="93c2c-225">이 정보 비슷한 toohello를 다음과 같은 XML을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="93c2c-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` 부분은 Oozie 명령 hello로 hello URL toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="93c2c-227">사용 하 여 hello tootype 없는 환경 변수 toocreate hello URL에 대 한 다음 모든 명령에 대해:</span><span class="sxs-lookup"><span data-stu-id="93c2c-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="93c2c-228">이전에 수신한 hello로 hello URL을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="93c2c-229">Toosubmit hello 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="93c2c-230">이 명령은 hello 작업 정보를 로드 **job.xml** 하 고 제출 tooOozie, 하지만 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="93c2c-231">Hello 명령이 완료 되 면 hello 작업의 hello ID를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="93c2c-232">예: `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="93c2c-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="93c2c-233">이 ID가 사용 되는 toomanage hello 작업.</span><span class="sxs-lookup"><span data-stu-id="93c2c-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="93c2c-234">다음 명령을 hello를 사용 하 여 hello 작업의 hello 상태를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="93c2c-235">대체 `<JOBID>` hello로 hello 이전 단계에서 반환 된 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="93c2c-236">정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-236">This returns information similar toohello following text:</span></span>

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

    <span data-ttu-id="93c2c-237">이 작업의 상태는 `PREP`입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="93c2c-238">이 상태는 hello 작업 생성 되었지만 시작 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="93c2c-239">다음 명령 toostart hello 작업 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="93c2c-240">대체 `<JOBID>` hello로 ID 이전에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="93c2c-241">이 명령은 후 hello 상태를 확인 하는 경우 실행 중 상태가 되며 hello 작업 내에서 hello 작업에 대 한 정보가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="93c2c-242">Hello 작업이 성공적으로 완료 되 면 hello 데이터가 생성 된 및 명령을 다음 hello를 사용 하 여 toohello SQL 데이터베이스 테이블을 내보낸를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="93c2c-243">Hello에 `1>` hello 다음 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="93c2c-244">반환 된 hello 정보는 텍스트 다음 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="93c2c-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="93c2c-245">Hello Oozie 명령에 대 한 자세한 내용은 참조 하십시오. [Oozie 명령줄 도구](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="93c2c-246">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="93c2c-246">Oozie REST API</span></span>

<span data-ttu-id="93c2c-247">hello Oozie REST API 사용 하면 toobuild Oozie를 사용 하는 고유한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="93c2c-248">hello 다음은 HDInsight hello Oozie REST API를 사용 하는 방법에 대 한 특정 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="93c2c-249">**URI**: hello REST API에 hello 클러스터 외부에서 액세스할 수 있습니다`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="93c2c-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="93c2c-250">**인증**: hello 클러스터 HTTP (관리자) 계정 및 암호를 사용 하 여 toohello API를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="93c2c-251">예:</span><span class="sxs-lookup"><span data-stu-id="93c2c-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="93c2c-252">Hello Oozie REST API 사용에 대 한 자세한 내용은 참조 하십시오. [Oozie 웹 서비스 API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="93c2c-253">Oozie 웹 UI</span><span class="sxs-lookup"><span data-stu-id="93c2c-253">Oozie Web UI</span></span>

<span data-ttu-id="93c2c-254">hello Oozie 웹 UI hello 클러스터에 hello Oozie 작업 상태에 대 한 웹 기반 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="93c2c-255">hello 웹 UI를 통해 다음 정보는 tooview hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="93c2c-256">작업 상태</span><span class="sxs-lookup"><span data-stu-id="93c2c-256">Job status</span></span>
* <span data-ttu-id="93c2c-257">작업 정의</span><span class="sxs-lookup"><span data-stu-id="93c2c-257">Job definition</span></span>
* <span data-ttu-id="93c2c-258">구성</span><span class="sxs-lookup"><span data-stu-id="93c2c-258">Configuration</span></span>
* <span data-ttu-id="93c2c-259">Hello 작업에서 hello 동작이 그래프</span><span class="sxs-lookup"><span data-stu-id="93c2c-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="93c2c-260">Hello 작업에 대 한 로그</span><span class="sxs-lookup"><span data-stu-id="93c2c-260">Logs for hello job</span></span>

<span data-ttu-id="93c2c-261">또한 작업 내의 동작에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="93c2c-262">tooaccess hello Oozie 웹 UI를 hello 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="93c2c-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="93c2c-263">SSH 터널 toohello HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="93c2c-264">내용은 hello를 참조 하십시오. [사용 하 여 SSH 터널링 HDInsight와](hdinsight-linux-ambari-ssh-tunnel.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="93c2c-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="93c2c-265">가 채널을 만든 후 hello Ambari web UI 웹 브라우저에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="93c2c-266">hello Ambari 사이트에 대 한 hello URI는 **https://CLUSTERNAME.azurehdinsight.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="93c2c-267">대체 **CLUSTERNAME** Linux 기반 HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="93c2c-268">Hello hello 페이지의 왼쪽에서 선택 **Oozie**, 다음 **빠른 링크**, 마지막으로 **Oozie 웹 UI**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![hello 메뉴의 이미지](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="93c2c-270">hello Oozie 웹 UI 기본값 toodisplaying 워크플로 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="93c2c-271">모든 워크플로 작업을 선택 하는 toosee **모든 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![모든 작업 표시](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="93c2c-273">작업 tooview hello 작업에 대 한 자세한 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-273">Select a job tooview more information about hello job.</span></span>

    ![작업 정보](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="93c2c-275">Hello 작업 정보 탭에서 기본 작업 정보 및 hello hello 작업 내의 개별 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="93c2c-276">Hello 탭을 사용 하 여 볼 수는 hello 맨 hello 작업 정의 작업 구성 액세스 hello 작업 로그를 보거나 전달 된 비순환 그래프 (DAG) hello 작업의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="93c2c-277">**작업 로그**: 선택 hello **GetLogs** tooget hello 작업에 대 한 모든 로그 단추 또는 hello를 사용 하 여 **입력 검색 필터** toofilter 로그 필드</span><span class="sxs-lookup"><span data-stu-id="93c2c-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![작업 로그](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="93c2c-279">**JobDAG**: hello DAG는 hello 워크플로 통해 수행 하는 hello 데이터 경로 대 한 그래픽 개요</span><span class="sxs-lookup"><span data-stu-id="93c2c-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![작업 DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="93c2c-281">Hello에서 hello 작업 중 하나를 선택 하면 **작업 정보** 탭 hello 동작에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="93c2c-282">예를 들어 hello 선택 **RunHiveScript** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-282">For example, select hello **RunHiveScript** action.</span></span>

    ![동작 정보](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="93c2c-284">링크 toohello 같은 hello 동작에 대 한 정보를 볼 수 **콘솔 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="93c2c-285">이 링크는 hello 작업에 대 한 사용된 tooview JobTracker 정보를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="93c2c-286">작업 예약</span><span class="sxs-lookup"><span data-stu-id="93c2c-286">Scheduling jobs</span></span>

<span data-ttu-id="93c2c-287">hello 코디네이터 toospecify를 작업에 대 한 시작, 종료 및 발생 빈도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="93c2c-288">toodefine hello 워크플로 사용 하 여 hello 다음 단계에 대 한 일정:</span><span class="sxs-lookup"><span data-stu-id="93c2c-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="93c2c-289">Toocreate 라는 파일을 다음 사용 하 여 hello **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="93c2c-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="93c2c-290">Hello hello 파일의 내용을 hello로 다음과 같은 XML을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-290">Use hello following XML as hello contents of hello file:</span></span>

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
    > <span data-ttu-id="93c2c-291">hello `${...}` 변수가 실행 시 hello 작업 정의의 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="93c2c-292">hello 변수는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="93c2c-293">`${coordFrequency}`: Hello 작업의 인스턴스를 실행 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="93c2c-294">** `${coordStart}`: hello 작업 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="93c2c-295">`${coordEnd}`: hello 작업 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="93c2c-296">`${coordTimezone}`: 일광 절약 시간제(일반적으로 UTC를 사용하여 표시됨) 없이 고정된 표준 시간대에서 코디네이터 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="93c2c-297">이 표준 시간대 hello "Oozie 처리 표준 시간대입니다." 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="93c2c-298">`${wfPath}`: 경로 toohello workflow.xml hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="93c2c-299">toosave hello 파일, Ctrl-X를 사용 하 여 **Y**, 및 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="93c2c-300">다음 명령 toocopy hello 파일 toohello 작업 디렉터리가이 작업에 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="93c2c-301">사용 하 여 hello toomodify hello 다음 **job.xml** 파일:</span><span class="sxs-lookup"><span data-stu-id="93c2c-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="93c2c-302">Hello 다음 변경 내용을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93c2c-302">Make hello following changes:</span></span>

   * <span data-ttu-id="93c2c-303">hello 워크플로 변경 하는 대신 tooinstruct oozie toorun hello 코디네이터 파일 `<name>oozie.wf.application.path</name>` 너무`<name>oozie.coord.application.path</name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="93c2c-304">tooset hello `workflowPath` hello coordinator에 의해 사용 되는 변수는 다음과 같은 XML hello 추가:</span><span class="sxs-lookup"><span data-stu-id="93c2c-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="93c2c-305">Hello 대체 `wasb://mycontainer@mystorageaccount.blob.core.windows` hello job.xml 파일의 다른 항목에서 사용 하는 hello 값으로는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="93c2c-306">toodefine hello 시작, 종료 및 hello coordinator 주파수 hello 다음과 같은 XML을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

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

       <span data-ttu-id="93c2c-307">이러한 값은 시작 시간 too12 hello 설정: 2017 년 5 월 10 일 오후 00 hello 종료 시간, 12, tooMay 2017 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="93c2c-308">이 작업을 매일 실행에 대 한 hello 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-308">hello interval for running this job daily.</span></span> <span data-ttu-id="93c2c-309">hello 빈도가 분, 24 시간 x 60 분의 1, 440 분 = 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="93c2c-310">마지막으로, 표준 시간대 hello tooUTC 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="93c2c-311">그런 다음 Ctrl-X를 사용 하 여 **Y** 및 **Enter** toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="93c2c-312">다음 명령을 사용 하 여 hello toorun hello 작업:</span><span class="sxs-lookup"><span data-stu-id="93c2c-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="93c2c-313">이 명령은 제출 하 고 hello 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="93c2c-314">Hello Oozie 웹 UI를 방문 하 고 hello를 선택 하는 경우 **코디네이터 작업** 정보 비슷한 toohello 이미지 다음 참조 탭:</span><span class="sxs-lookup"><span data-stu-id="93c2c-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![코디네이터 작업 탭](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="93c2c-316">hello **다음 구체화** 항목 다음에 작업 실행 hello hello 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="93c2c-317">비슷한 toohello hello 웹 UI에서에서 hello 작업 항목을 선택 하면 이전 워크플로 작업 hello 작업에서 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![코디네이터 작업 정보](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="93c2c-319">이 이미지에는 예약 된 hello 워크플로 내에서 개별 동작 hello 작업의 성공적인 실행만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="93c2c-320">hello 중 하나를 선택 하는 toosee **동작** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-320">toosee that, select one of hello **Action** entries.</span></span>

    ![동작 정보](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="93c2c-322">문제 해결</span><span class="sxs-lookup"><span data-stu-id="93c2c-322">Troubleshooting</span></span>

<span data-ttu-id="93c2c-323">hello Oozie UI tooview Oozie 로그 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="93c2c-324">또한 hello 워크플로에 의해 시작 되는 MapReduce 작업에 대 한 링크 tooJobTracker 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="93c2c-325">문제 해결에 대 한 hello 패턴 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="93c2c-326">Oozie 웹 UI에서 hello 작업 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="93c2c-327">선택 하는 경우 hello 동작 toosee hello 없을 경우 오류 또는 특정 작업에 대 한 오류, **오류 메시지가** 필드 hello 실패 시 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="93c2c-328">사용 가능한 경우 hello URL 사용 hello 동작 tooview에서 자세한 정보 (예: JobTracker 로그의 경우) hello 동작에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="93c2c-329">hello는 다음과 같은 특정 오류가 발생할 수 있습니다 및 방법을 tooresolve 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="93c2c-330">JA009: 클러스터를 초기화할 수 없음</span><span class="sxs-lookup"><span data-stu-id="93c2c-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="93c2c-331">**증상**: 작업 상태를 변경할 수를 너무 hello**SUSPENDED**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="93c2c-332">Hello 작업에 대 한 세부 정보 표시로 hello RunHiveScript 상태 **START_MANUAL**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="93c2c-333">Hello 동작을 선택 하면 hello 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="93c2c-334">**원인**: hello에 사용 되는 WASB 주소 hello **job.xml** 파일 hello 저장소 컨테이너 또는 저장소 계정 이름이 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="93c2c-335">hello WASB 주소 형식 이어야 `wasb://containername@storageaccountname.blob.core.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="93c2c-336">**해결 방법**: hello 작업에 의해 사용 되는 hello WASB 주소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="93c2c-337">JA002: Oozie tooimpersonate 허용 되지 않습니다 &lt;사용자 ></span><span class="sxs-lookup"><span data-stu-id="93c2c-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="93c2c-338">**증상**: 작업 상태를 변경할 수를 너무 hello**SUSPENDED**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="93c2c-339">Hello 작업에 대 한 세부 정보 표시로 hello RunHiveScript 상태 **START_MANUAL**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="93c2c-340">Hello 동작을 선택 하면 다음과 같은 오류 메시지가 hello 표시:</span><span class="sxs-lookup"><span data-stu-id="93c2c-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="93c2c-341">**원인**: 현재 사용 권한 설정을 Oozie 불가 tooimpersonate hello 사용자 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="93c2c-342">**해상도**: Oozie hello에 tooimpersonate 사용자를 사용할 수 **사용자** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="93c2c-343">사용 하 여 hello `groups USERNAME` 사용자 계정을 hello toosee hello 그룹의 멤버인 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="93c2c-344">Hello 사용자가 hello의 구성원이 아닌 경우 **사용자** 그룹에서 다음 명령 tooadd hello 사용자 toohello 그룹 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="93c2c-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="93c2c-345">HDInsight는 hello 추가 된 사용자 그룹 toohello 인식 하기 전에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="93c2c-346">시작 관리자 오류(Sqoop)</span><span class="sxs-lookup"><span data-stu-id="93c2c-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="93c2c-347">**증상**: 작업 상태를 변경할 수를 너무 hello**KILLED**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="93c2c-348">Hello 작업에 대 한 세부 정보 표시로 hello RunSqoopExport 상태 **오류**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="93c2c-349">Hello 동작을 선택 하면 다음과 같은 오류 메시지가 hello 표시:</span><span class="sxs-lookup"><span data-stu-id="93c2c-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="93c2c-350">**원인**: Sqoop 없습니다 tooload hello 데이터베이스 드라이버 필요한 tooaccess hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="93c2c-351">**해결 방법**: Sqoop Oozie 작업에서를 사용할 때 포함 해야 hello로 hello 데이터베이스 드라이버 hello 작업에서 사용 하는 다른 리소스 (예: hello workflow.xml).</span><span class="sxs-lookup"><span data-stu-id="93c2c-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="93c2c-352">Hello에서 hello 데이터베이스 드라이버를 포함 하는 hello 보관 파일을 참조할 수도 `<sqoop>...</sqoop>` hello workflow.xml의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="93c2c-353">예를 들어이 문서에 대 한 일에 대 한 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="93c2c-354">Hello sqljdbc4.1.jar 파일 toohello /tutorials/useoozie 디렉터리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="93c2c-355">Hello workflow.xml tooadd hello 위에 새 줄에 다음과 같은 XML을 수정 `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="93c2c-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="93c2c-356">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93c2c-356">Next steps</span></span>

<span data-ttu-id="93c2c-357">이 자습서에서는 방법에 대해 배웠습니다 toodefine Oozie 워크플로 방법과 toorun Oozie 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c2c-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="93c2c-358">HDInsight 작업에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="93c2c-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="93c2c-359">[HDInsight에서 시간 기준의 Oozie 코디네이터 사용][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="93c2c-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="93c2c-360">[HDInsight에서 Hadoop 작업용 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="93c2c-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="93c2c-361">[HDInsight에서 Hadoop과 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="93c2c-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="93c2c-362">[HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="93c2c-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="93c2c-363">[HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="93c2c-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="93c2c-364">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="93c2c-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
