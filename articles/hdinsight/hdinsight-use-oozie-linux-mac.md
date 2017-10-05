---
title: "Linux 기반 HDInsight에서 Hadoop Oozie 워크플로 사용 | Microsoft Docs"
description: "Linux 기반 HDInsight에서 Hadoop Oozie를 사용합니다. 또한 Oozie 워크플로를 정의하고 Oozie 작업을 제출하는 방법에 대해서도 살펴봅니다."
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="3217f-104">Hadoop과 함께 Oozie를 사용하여 Linux 기반 HDInsight에서 워크플로 정의 및 실행</span><span class="sxs-lookup"><span data-stu-id="3217f-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="3217f-105">HDInsight에서 Hadoop와 함께 Apache Oozie를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="3217f-106">Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="3217f-107">Oozie는 Hadoop 스택과 통합되며 다음 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="3217f-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="3217f-108">Apache MapReduce</span></span>
* <span data-ttu-id="3217f-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="3217f-109">Apache Pig</span></span>
* <span data-ttu-id="3217f-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="3217f-110">Apache Hive</span></span>
* <span data-ttu-id="3217f-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="3217f-111">Apache Sqoop</span></span>

<span data-ttu-id="3217f-112">Oozie는 Java 프로그램이나 셸 스크립트와 같은 시스템에 특정한 작업을 예약하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="3217f-113">HDInsight를 사용하여 워크플로를 정의하는 또 다른 옵션은 Azure 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="3217f-114">Azure 데이터 팩터리에 대한 자세한 내용은 [데이터 팩터리에서 Pig 및 Hive 사용][azure-data-factory-pig-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3217f-115">도메인에 가입된 HDInsight에서는 Oozie를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3217f-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3217f-116">Prerequisites</span></span>

* <span data-ttu-id="3217f-117">**HDInsight 클러스터**: [Linux에서 HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3217f-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3217f-118">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3217f-119">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3217f-120">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="3217f-121">예제 워크플로</span><span class="sxs-lookup"><span data-stu-id="3217f-121">Example workflow</span></span>

<span data-ttu-id="3217f-122">이 문서에서 사용되는 워크플로에는 두 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="3217f-123">동작은 Hive, Sqoop, MapReduce 또는 기타 프로세스 실행과 같은 작업에 대한 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![워크플로 다이어그램][img-workflow-diagram]

1. <span data-ttu-id="3217f-125">Hive 동작은 HiveQL을 실행하여 HDInsight에 포함된 **hivesampletable** 에서 레코드를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="3217f-126">데이터의 각 행은 특정 모바일 장치에서의 방문을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="3217f-127">레코드 형식은 다음 텍스트와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="3217f-128">이 문서에서 사용된 Hive 스크립트는 각 플랫폼(예: Android 또는 iPhone)에 대한 총 방문 횟수를 계산하여 새 Hive 테이블에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="3217f-129">Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="3217f-130">Sqoop 동작은 새 Hive 테이블의 내용을 Azure SQL 데이터베이스의 테이블로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="3217f-131">Sqoop에 대한 자세한 내용은 [HDInsight에서 Hadoop Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="3217f-132">HDInsight 클러스터에서 지원되는 Oozie 버전에 대해서는 [HDInsight에서 제공하는 Hadoop 클러스터 버전의 새로운 기능][hdinsight-versions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="3217f-133">작업 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="3217f-133">Create the working directory</span></span>

<span data-ttu-id="3217f-134">Oozie에는 작업을 같은 디렉터리에 저장하는 데 사용되는 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="3217f-135">이 예에서는 **wasb:///tutorials/useoozie**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="3217f-136">다음 명령을 사용하여 이 디렉터리 및 이 워크플로에서 만드는 새 Hive 테이블을 저장할 데이터 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="3217f-137">`-p` 매개 변수는 경로의 모든 디렉터리가 만들어지도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="3217f-138">**data** 디렉터리는 **useooziewf.hql** 스크립트에서 사용하는 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="3217f-139">또한 Hive 및 Sqoop 작업을 실행할 때 Oozie가 사용자 계정을 가장할 수 있도록 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="3217f-140">**USERNAME** 을 로그인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="3217f-141">사용자가 이미 `users` 그룹의 멤버라는 오류가 발생하는 경우 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="3217f-142">데이터베이스 드라이버 추가</span><span class="sxs-lookup"><span data-stu-id="3217f-142">Add a database driver</span></span>

<span data-ttu-id="3217f-143">이 워크플로에서는 Sqoop를 사용하여 SQL 데이터베이스로 데이터를 내보내므로 SQL 데이터베이스와 통신하는 데 사용되는 JDBC 드라이버의 복사본을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="3217f-144">다음 명령을 사용하여 작업 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="3217f-145">워크플로에서 MapReduce 응용 프로그램이 포함된 jar 등의 다른 리소스를 사용하는 경우 이러한 리소스도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="3217f-146">Hive 쿼리 정의</span><span class="sxs-lookup"><span data-stu-id="3217f-146">Define the Hive query</span></span>

<span data-ttu-id="3217f-147">다음 단계를 사용하여 이 문서의 뒷부분에 나오는 Oozie 워크플로에서 사용되는 쿼리를 정의하는 HiveQL 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="3217f-148">SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="3217f-149">다음 명령은 `ssh` 명령을 사용하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="3217f-150">__USERNAME__을 클러스터의 SSH 사용자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="3217f-151">__CLUSTERNAME__ 을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3217f-152">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3217f-153">SSH 연결에서 다음 명령을 사용하여 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="3217f-154">nano 편집기가 열리면 파일 내용으로 다음 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="3217f-155">스크립트에서 사용되는 두 가지 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="3217f-156">**${hiveTableName}**: 만들려는 테이블의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="3217f-157">**${hiveDataFolder}**: 테이블의 데이터 파일을 저장할 위치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="3217f-158">워크플로 정의 파일(이 자습서의 경우 workflow.xml)은 런타임 시 이러한 값을 이 HiveQL 스크립트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="3217f-159">편집기를 종료하려면 Ctrl-X를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="3217f-160">메시지가 나타나면 **Y**를 선택하여 파일을 저장한 다음 **Enter**를 사용하여 **useooziewf.hql** 파일 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="3217f-161">다음 명령을 사용하여 **useooziewf.hql**을 **wasb:///tutorials/useoozie/useooziewf.hql**에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="3217f-162">이러한 명령은 클러스터용 HDFS 호환 스토리지에 **useooziewf.hql** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="3217f-163">워크플로 정의</span><span class="sxs-lookup"><span data-stu-id="3217f-163">Define the workflow</span></span>

<span data-ttu-id="3217f-164">Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="3217f-165">다음 단계를 사용하여 워크플로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="3217f-166">다음 문을 사용하여 새 파일을 만들고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="3217f-167">nano 편집기가 열리면 파일 내용으로 다음 XML을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    <span data-ttu-id="3217f-168">워크플로에 정의된 두 가지 동작은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="3217f-169">**RunHiveScript**: 이 동작은 시작 동작이며 **useooziewf.hql** Hive 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="3217f-170">**RunSqoopExport**: 이 동작은 Sqoop를 사용하여 Hive 스크립트에서 만든 데이터를 SQL Database로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="3217f-171">이 동작은 **RunHiveScript** 동작이 성공한 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="3217f-172">워크플로에 `${jobTracker}` 등의 여러 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="3217f-173">이러한 항목은 작업 정의에 사용한 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="3217f-174">작업 정의는 이 문서의 뒷부분에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="3217f-175">Sqoop 섹션의 `<archive>sqljdbc4.jar</arcive>` 항목도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="3217f-176">이 항목은 이 동작을 실행할 때 이 보관 파일을 Sqoop에 사용할 수 있게 설정하도록 Oozie에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="3217f-177">Ctrl-X를 사용한 다음 **Y**와 **Enter** 키를 사용하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="3217f-178">다음 명령을 사용하여 **workflow.xml** 파일을 **/tutorials/useoozie/workflow.xml**에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="3217f-179">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3217f-179">Create the database</span></span>

<span data-ttu-id="3217f-180">Azure SQL Database를 만들려면 [SQL Database 만들기](../sql-database/sql-database-get-started.md) 문서의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="3217f-181">데이터베이스를 만들 때 데이터베이스 이름으로 `oozietest`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="3217f-182">또한 데이터베이스 서버의 이름을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="3217f-183">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="3217f-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="3217f-184">여러 가지 방법으로 SQL 데이터베이스에 연결하여 테이블을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="3217f-185">다음 단계는 HDInsight 클러스터의 [FreeTDS](http://www.freetds.org/) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="3217f-186">다음 명령을 사용하여 HDInsight 클러스터에 FreeTDS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="3217f-187">FreeTDS가 설치되면 다음 명령을 사용하여 이전에 생성한 SQL 데이터베이스 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="3217f-188">다음 텍스트와 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="3217f-189">`1>` 프롬프트에 다음 행을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="3217f-190">`GO` 문을 입력하면 이전 문이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="3217f-191">이러한 문은 워크플로에서 사용되는 **mobiledata**라는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="3217f-192">다음을 사용하여 테이블이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="3217f-193">그러면 다음 텍스트와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="3217f-194">`exit` at the `1>` 를 입력하여 tsql 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="3217f-195">작업 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="3217f-195">Create the job definition</span></span>

<span data-ttu-id="3217f-196">작업 정의는 workflow.xml을 찾을 수 있는 위치를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="3217f-197">또한 워크플로에서 사용되는 기타 파일(예: useooziewf.hql)을 찾을 수 있는 위치를 설명합니다. 또한 워크플로 및 관련 파일 내에서 사용되는 속성 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="3217f-198">다음 명령을 사용하여 기본 저장소의 전체 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="3217f-199">이 주소는 잠시 후에 구성 파일에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="3217f-200">이 명령은 다음 XML과 유사한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="3217f-201">HDInsight 클러스터에서 Azure Storage를 기본 저장소로 사용하면 `<value>` 요소의 내용은 `wasb://`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="3217f-202">Azure Data Lake Store를 대신 사용하면 `adl://`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="3217f-203">다음 단계에서 사용되므로 `<value>` 요소의 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="3217f-204">다음 명령을 사용하여 클러스터 헤드 노드의 FQDN을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="3217f-205">이 정보는 클러스터의 JobTracker 주소에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="3217f-206">이 명령은 다음 텍스트와 비슷한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="3217f-207">JobTracker에 사용되는 포트는 8050이므로 JobTracker에 사용할 전체 주소는 `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="3217f-208">다음을 사용하여 Oozie 작업 정의 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="3217f-209">nano 편집기가 열리면 파일 내용으로 다음 XML을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

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

   * <span data-ttu-id="3217f-210">**wasb://mycontainer@mystorageaccount.blob.core.windows.net**의 모든 인스턴스를 기본 저장소로 이전에 받은 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="3217f-211">`wasb` 경로인 경우 전체 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="3217f-212">`wasb:///`만으로 줄이지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="3217f-213">**JOBTRACKERADDRESS** 를 이전에 받은 JobTracker/ResourceManager 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="3217f-214">**YourName** 을 HDInsight 클러스터의 로그인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="3217f-215">**serverName**, **adminLogin** 및 **adminPassword**를 Azure SQL Database에 대한 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="3217f-216">이 파일의 정보는 대부분 workflow.xml 또는 ooziewf.hql 파일에서 사용되는 값(예: ${nameNode})을 채우는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="3217f-217">**oozie.wf.application.path** 항목은 이 작업에서 실행한 워크플로를 포함하는 workflow.xml 파일을 찾을 수 있는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="3217f-218">Ctrl-X를 사용한 다음 **Y**와 **Enter** 키를 사용하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="3217f-219">작업 제출 및 관리</span><span class="sxs-lookup"><span data-stu-id="3217f-219">Submit and manage the job</span></span>

<span data-ttu-id="3217f-220">다음 단계에서는 Oozie 명령을 사용하여 클러스터에서 Oozie 워크플로를 제출 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="3217f-221">Oozie 명령은 [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)를 통해 제공되는 친숙한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3217f-222">Oozie 명령을 사용할 때는 HDInsight 헤드 노드에 대한 FQDN을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="3217f-223">이 FQDN은 클러스터에서만 액세스할 수 있으며, 클러스터가 Azure Virtual Network에 있는 경우에는 같은 네트워크에 있는 다른 컴퓨터에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="3217f-224">다음을 사용하여 Oozie 서비스의 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="3217f-225">이 명령은 다음 XML과 유사한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="3217f-226">`http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` 부분은 Oozie 명령에서 사용할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="3217f-227">모든 명령에 입력할 필요 없이 다음을 사용하여 URL에 대한 환경 변수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="3217f-228">URL을 이전에 받은 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="3217f-229">다음을 사용하여 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="3217f-230">이 명령은 **job.xml**에서 작업 정보를 로드하고 Oozie에 제출하지만 실행하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="3217f-231">명령이 완료되면 작업의 ID가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="3217f-232">예: `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="3217f-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="3217f-233">이 ID는 작업을 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="3217f-234">다음 명령을 사용하여 작업 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="3217f-235">`<JOBID>`를 이전 단계에서 반환된 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="3217f-236">이 명령은 다음 텍스트와 비슷한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-236">This returns information similar to the following text:</span></span>

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

    <span data-ttu-id="3217f-237">이 작업의 상태는 `PREP`입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="3217f-238">이 상태는 작업이 만들어졌지만 시작되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="3217f-239">다음 명령을 사용하여 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="3217f-240">`<JOBID>`를 이전에 반환된 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="3217f-241">이 명령 후에 상태를 확인하면 실행 중 상태가 표시되고 작업 내 동작에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="3217f-242">작업이 성공적으로 완료되면 다음 명령을 사용하여 데이터가 생성되고 SQL 데이터베이스 테이블로 내보내졌음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="3217f-243">`1>` 프롬프트에 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="3217f-244">반환되는 정보는 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="3217f-245">Oozie 명령에 대한 자세한 내용은 [Oozie 명령줄 도구](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="3217f-246">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="3217f-246">Oozie REST API</span></span>

<span data-ttu-id="3217f-247">Oozie REST API를 사용하면 Oozie와 함께 작동하는 사용자 고유의 도구를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="3217f-248">다음은 Oozie REST API 사용에 대한 HDInsight 관련 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="3217f-249">**URI**: 클러스터 외부의 `https://CLUSTERNAME.azurehdinsight.net/oozie`에서 REST API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="3217f-250">**인증**: 클러스터 HTTP 계정(admin) 및 암호를 사용하여 API에 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="3217f-251">예:</span><span class="sxs-lookup"><span data-stu-id="3217f-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="3217f-252">Oozie REST API 사용에 대한 자세한 내용은 [Oozie 웹 서비스 API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="3217f-253">Oozie 웹 UI</span><span class="sxs-lookup"><span data-stu-id="3217f-253">Oozie Web UI</span></span>

<span data-ttu-id="3217f-254">Oozie 웹 UI는 클러스터의 Oozie 작업 상태에 대한 웹 기반 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="3217f-255">웹 UI를 사용하여 다음 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="3217f-256">작업 상태</span><span class="sxs-lookup"><span data-stu-id="3217f-256">Job status</span></span>
* <span data-ttu-id="3217f-257">작업 정의</span><span class="sxs-lookup"><span data-stu-id="3217f-257">Job definition</span></span>
* <span data-ttu-id="3217f-258">구성</span><span class="sxs-lookup"><span data-stu-id="3217f-258">Configuration</span></span>
* <span data-ttu-id="3217f-259">작업의 동작 그래프</span><span class="sxs-lookup"><span data-stu-id="3217f-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="3217f-260">작업 로그</span><span class="sxs-lookup"><span data-stu-id="3217f-260">Logs for the job</span></span>

<span data-ttu-id="3217f-261">또한 작업 내의 동작에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="3217f-262">Oozie 웹 UI에 액세스하려면 다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="3217f-263">HDInsight 클러스터에 대한 SSH 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="3217f-264">자세한 내용은 [HDInsight와 함께 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="3217f-265">터널을 만든 후 웹 브라우저에서 Ambari 웹 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="3217f-266">Ambari 사이트의 URI는 **https://CLUSTERNAME.azurehdinsight.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="3217f-267">**CLUSTERNAME**을 Linux 기반 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="3217f-268">페이지의 왼쪽부터 **Oozie**, **빠른 링크**, **Oozie 웹 UI**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![메뉴 이미지](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="3217f-270">Oozie 웹 UI는 기본적으로 실행 중인 워크플로 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="3217f-271">모든 워크플로 작업을 보려면 **모든 작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![모든 작업 표시](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="3217f-273">작업에 대한 자세한 정보를 보려면 해당 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-273">Select a job to view more information about the job.</span></span>

    ![작업 정보](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="3217f-275">작업 정보 탭에서 기본 작업 정보 및 작업 내의 개별 동작을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="3217f-276">맨 위에 있는 탭을 사용하여 작업 정의 및 작업 구성을 보거나, 작업 로그에 액세스하거나, 작업의 DAG(방향성 비순환 그래프)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="3217f-277">**작업 로그**: **GetLogs** 단추를 선택하여 작업에 대한 모든 로그를 가져오거나 **검색 필터 입력** 필드를 사용하여 로그를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![작업 로그](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="3217f-279">**JobDAG**: DAG는 워크플로를 통해 가져온 데이터 경로의 그래픽 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![작업 DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="3217f-281">**작업 정보** 탭에서 동작 중 하나를 선택하면 해당 동작에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="3217f-282">예를 들어 **RunHiveScript** 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-282">For example, select the **RunHiveScript** action.</span></span>

    ![동작 정보](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="3217f-284">**콘솔 URL** 링크 등 작업에 대한 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="3217f-285">이 링크를 사용하여 작업에 대한 JobTracker 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="3217f-286">작업 예약</span><span class="sxs-lookup"><span data-stu-id="3217f-286">Scheduling jobs</span></span>

<span data-ttu-id="3217f-287">코디네이터를 통해 작업의 시작, 종료 및 발생 빈도를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="3217f-288">워크플로 일정을 정의하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="3217f-289">다음을 사용하여 **coordinator.xml**이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="3217f-290">파일 내용으로 다음 XML을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-290">Use the following XML as the contents of the file:</span></span>

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
    > <span data-ttu-id="3217f-291">`${...}` 변수는 런타임에 작업 정의의 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="3217f-292">변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="3217f-293">`${coordFrequency}`: 작업 인스턴스 실행 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="3217f-294">** `${coordStart}`: 작업 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="3217f-295">`${coordEnd}`: 작업 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="3217f-296">`${coordTimezone}`: 일광 절약 시간제(일반적으로 UTC를 사용하여 표시됨) 없이 고정된 표준 시간대에서 코디네이터 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="3217f-297">해당 시간대는 "Oozie 처리 시간대"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="3217f-298">`${wfPath}`: workflow.xml의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="3217f-299">파일을 저장하려면 Ctrl-X, **Y**, **Enter** 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="3217f-300">다음 명령을 사용하여 이 작업의 작업 디렉터리에 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="3217f-301">다음을 사용하여 **job.xml** 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="3217f-302">다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-302">Make the following changes:</span></span>

   * <span data-ttu-id="3217f-303">Oozie에서 워크플로 대신 코디네이터 파일을 실행하도록 지시하려면 `<name>oozie.wf.application.path</name>`을(를) `<name>oozie.coord.application.path</name>`(으)로 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="3217f-304">코디네이터에서 사용하는 `workflowPath` 변수를 설정하려면 다음 XML을 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="3217f-305">`wasb://mycontainer@mystorageaccount.blob.core.windows` 텍스트를 job.xml 파일의 다른 항목에 사용된 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="3217f-306">코디네이터에 대한 시작, 종료 및 빈도를 정의하려면 다음 XML을 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

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

       <span data-ttu-id="3217f-307">이러한 값은 시작 시간을 2017년 5월 10일 오후 12시로 설정하고, 종료 시간을 2017년 5월 12일로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="3217f-308">매일 이 작업을 실행하는 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-308">The interval for running this job daily.</span></span> <span data-ttu-id="3217f-309">빈도는 분 단위이므로 24시간 x 60분 = 1,440분입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="3217f-310">마지막으로, 표준 시간대는 UTC로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="3217f-311">Ctrl-X를 사용한 다음 **Y**와 **Enter** 키를 사용하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="3217f-312">작업을 실행하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="3217f-313">이 명령은 작업을 제출하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="3217f-314">Oozie Web UI를 방문하여 **코디네이터 작업** 탭을 선택하면 다음 그림과 유사한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![코디네이터 작업 탭](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="3217f-316">**다음 구체화** 항목에는 다음에 작업이 실행되는 시간이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="3217f-317">이전의 워크플로 작업과 마찬가지로 웹 UI에서 작업 항목을 선택하면 작업에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![코디네이터 작업 정보](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="3217f-319">이 이미지는 성공한 작업 실행만 표시하며, 예약된 워크플로 내의 개별 동작은 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="3217f-320">확인하려면 **작업** 항목 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-320">To see that, select one of the **Action** entries.</span></span>

    ![동작 정보](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="3217f-322">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3217f-322">Troubleshooting</span></span>

<span data-ttu-id="3217f-323">Oozie UI를 사용하여 Oozie 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="3217f-324">워크플로에서 시작된 MapReduce 작업에 대한 JobTracker 로그의 링크도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="3217f-325">문제 해결 패턴은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="3217f-326">Oozie 웹 UI에서 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="3217f-327">특정 동작에 대한 오류 또는 실패가 있는 경우 해당 동작을 선택하여 **오류 메시지** 필드에 오류에 대한 자세한 정보가 제공되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="3217f-328">사용 가능한 경우 동작의 URL을 사용하여 해당 동작에 대한 자세한 정보(예: JobTracker 로그)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="3217f-329">다음은 발생할 수 있는 특정 오류 및 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="3217f-330">JA009: 클러스터를 초기화할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3217f-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="3217f-331">**증상**: 작업 상태가 **일시 중단됨**으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="3217f-332">작업에 대한 세부 정보에 RunHiveScript 상태가 **START_MANUAL**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="3217f-333">동작을 선택하면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="3217f-334">**원인**: **job.xml** 파일에 사용된 WASB 주소에 저장소 컨테이너 또는 저장소 계정 이름이 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="3217f-335">WASB 주소 형식은 `wasb://containername@storageaccountname.blob.core.windows.net`이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="3217f-336">**해결 방법**: 작업에서 사용하는 WASB 주소를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="3217f-337">JA002: Oozie에서 &lt;USER>를 가장할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3217f-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="3217f-338">**증상**: 작업 상태가 **일시 중단됨**으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="3217f-339">작업에 대한 세부 정보에 RunHiveScript 상태가 **START_MANUAL**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="3217f-340">동작을 선택하면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="3217f-341">**원인**: 현재 사용 권한 설정에서 Oozie가 지정된 사용자 계정을 가장하도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="3217f-342">**해결 방법**: **사용자** 그룹에서 Oozie가 사용자를 가장하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="3217f-343">`groups USERNAME` 을 사용하여 사용자 계정이 멤버로 속해 있는 그룹을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="3217f-344">사용자가 **users** 그룹의 멤버가 아닌 경우 다음 명령을 사용하여 사용자를 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="3217f-345">HDInsight에서 사용자가 그룹에 추가된 것을 인식하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="3217f-346">시작 관리자 오류(Sqoop)</span><span class="sxs-lookup"><span data-stu-id="3217f-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="3217f-347">**증상**: 작업 상태가 **중단됨**으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="3217f-348">작업에 대한 세부 정보에 RunSqoopExport 상태가 **오류**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="3217f-349">동작을 선택하면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="3217f-350">**원인**: Sqoop가 데이터베이스에 액세스하는 데 필요한 데이터베이스 드라이버를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="3217f-351">**해결 방법**: Oozie 작업에서 Sqoop를 사용하는 경우 작업에 사용되는 다른 리소스(예: workflow.xml)와 함께 데이터베이스 드라이버를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="3217f-352">또한 workflow.xml의 `<sqoop>...</sqoop>` 섹션에서 데이터베이스 드라이버가 포함된 보관 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="3217f-353">예를 들어 이 문서의 작업에는 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="3217f-354">sqljdbc4.1.jar 파일을 /tutorials/useoozie 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="3217f-355">workflow.xml을 수정하여 `</sqoop>` 위의 새 줄에 다음 XML을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="3217f-356">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3217f-356">Next steps</span></span>

<span data-ttu-id="3217f-357">이 자습서에서는 Oozie 워크플로를 정의하는 방법 및 Oozie 작업을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3217f-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="3217f-358">HDInsight 작업에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3217f-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="3217f-359">[HDInsight에서 시간 기준의 Oozie 코디네이터 사용][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="3217f-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="3217f-360">[HDInsight에서 Hadoop 작업용 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="3217f-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="3217f-361">[HDInsight에서 Hadoop과 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="3217f-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="3217f-362">[HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="3217f-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="3217f-363">[HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3217f-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3217f-364">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3217f-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
