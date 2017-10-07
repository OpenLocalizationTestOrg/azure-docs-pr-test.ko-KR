---
title: "HDInsight의 Hadoop Oozie aaaUse | Microsoft Docs"
description: "빅데이터 서비스인 HDInsight에서 Hadoop Oozie를 사용하는 방법을 알아봅니다. 에 대해 알아봅니다 어떻게 toodefine Oozie 워크플로, Oozie 작업을 제출 하 고 있습니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="5a484-104">Hadoop toodefine 함께 Oozie를 사용 하 고 HDInsight에 워크플로 실행</span><span class="sxs-lookup"><span data-stu-id="5a484-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="5a484-105">Toouse Apache Oozie toodefine 워크플로 및 실행 방법을 HDInsight에서 워크플로 hello에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="5a484-106">toolearn hello Oozie 코디네이터에 대 한 참조 [HDInsight Hadoop Oozie 코디네이터 시간 기반 사용][hdinsight-oozie-coordinator-time]합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="5a484-107">Azure Data Factory toolearn 참조 [Data Factory와 사용 하 여 Pig 및 Hive][azure-data-factory-pig-hive]합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="5a484-108">Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="5a484-109">Hello Hadoop 스택와도 통합 되어 하 고 Apache MapReduce Apache Pig, Apache Hive, Sqoop Apache Hadoop 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="5a484-110">사용 되는 tooschedule 작업은 Java 프로그램 또는 셸 스크립트와 같은 특정 tooa 시스템 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="5a484-111">이 자습서의 hello 지침에 따라 구현 hello 워크플로 두 개의 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![워크플로 다이어그램][img-workflow-diagram]

1. <span data-ttu-id="5a484-113">하이브 작업 log4j 파일에 HiveQL 스크립트 toocount hello 로그 수준 유형의 각 항목을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="5a484-114">예를 들어 hello 유형과 hello 심각도 표시 하는 [로그 수준] 필드를 포함 하는 필드의 줄에 각 log4j 파일 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="5a484-115">hello 하이브 스크립트 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="5a484-116">Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a484-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="5a484-117">Sqoop 작업 hello HiveQL 출력 tooa 테이블을 Azure SQL 데이터베이스에서 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="5a484-118">Sqoop에 대한 자세한 내용은 [HDInsight에서 Hadoop Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a484-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="5a484-119">HDInsight 클러스터에서 지원 되 Oozie 버전에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="5a484-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="5a484-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5a484-120">Prerequisites</span></span>
<span data-ttu-id="5a484-121">이 자습서를 시작 하기 전에 hello 아래 항목 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="5a484-122">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="5a484-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="5a484-123">Oozie 워크플로 정의 및 hello 관련 HiveQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="5a484-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="5a484-124">Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="5a484-125">hello 기본 워크플로 파일 이름은 *workflow.xml*합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="5a484-126">hello 다음은이 자습서에서 사용 하는 hello 워크플로 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-126">hello following is hello workflow file you use in this tutorial.</span></span>

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

<span data-ttu-id="5a484-127">Hello 워크플로에 정의 된 두 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="5a484-128">hello 시작 tooaction은 *RunHiveScript*합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="5a484-129">Hello 다음 동작은 hello 작업이 성공적으로 실행 되는 경우에 *RunSqoopExport*합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="5a484-130">hello RunHiveScript는 여러 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="5a484-131">Azure PowerShell을 사용 하 여 워크스테이션에서 hello Oozie 작업을 제출 하는 경우 hello 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="5a484-132">워크플로 변수</span><span class="sxs-lookup"><span data-stu-id="5a484-132">Workflow variables</span></span></th><th><span data-ttu-id="5a484-133">설명</span><span class="sxs-lookup"><span data-stu-id="5a484-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="5a484-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="5a484-134">${jobTracker}</span></span></td><td><span data-ttu-id="5a484-135">Hello Hadoop 작업 트래커의 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="5a484-136">HDInsight 버전 2.1 및 3.0에서 <strong>jobtrackerhost:9010</strong>를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5a484-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="5a484-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="5a484-137">${nameNode}</span></span></td><td><span data-ttu-id="5a484-138">Hello Hadoop 이름 노드의 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="5a484-139">예를 들어 hello 기본 파일 시스템 주소를 사용 하 여 <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="5a484-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="5a484-140">${queueName}</span></span></td><td><span data-ttu-id="5a484-141">으로 제출 되었습니다. 작업 hello hello 큐 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="5a484-142">사용 하 여 hello <strong>기본</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="5a484-143">Hive 작업 변수</span><span class="sxs-lookup"><span data-stu-id="5a484-143">Hive action variable</span></span></th><th><span data-ttu-id="5a484-144">설명</span><span class="sxs-lookup"><span data-stu-id="5a484-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="5a484-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="5a484-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="5a484-146">Create Table 하이브 명령 hello에 대 한 hello 소스 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="5a484-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="5a484-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="5a484-148">덮어쓰기 삽입 문 hello에 대 한 hello 출력 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="5a484-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="5a484-149">${hiveTableName}</span></span></td><td><span data-ttu-id="5a484-150">Hello hello log4j 데이터 파일을 참조 하는 hello Hive 테이블 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="5a484-151">Sqoop 작업 변수</span><span class="sxs-lookup"><span data-stu-id="5a484-151">Sqoop action variable</span></span></th><th><span data-ttu-id="5a484-152">설명</span><span class="sxs-lookup"><span data-stu-id="5a484-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="5a484-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="5a484-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="5a484-154">Hello Azure SQL 데이터베이스 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="5a484-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="5a484-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="5a484-156">Hello Azure SQL 데이터베이스 테이블 hello 데이터 내보낼 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="5a484-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="5a484-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="5a484-158">하이브 덮어쓰기 삽입 문 hello에 대 한 hello 출력 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="5a484-159">이 hello hello Sqoop 내보내기 (내보내기-dir)에 대 한 같은 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="5a484-160">Oozie 워크플로 및 워크플로 작업 사용에 대한 자세한 내용은 [Apache Oozie 4.0 설명서][apache-oozie-400](HDInsight 버전 3.0의 경우) 또는 [Apache Oozie 3.3.2 설명서][apache-oozie-332](HDInsight 버전 2.1의 경우)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a484-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="5a484-161">HiveQL 스크립트 파일을 호출 하는 hello hello 워크플로에서 하이브 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="5a484-162">이 스크립트 파일에는 세 개의 HiveQL 문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="5a484-163">**DROP TABLE 문 hello** 있는 경우 삭제 hello log4j Hive 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="5a484-164">**CREATE TABLE 문 hello** hello log4j 로그 파일의 toohello 위치를 가리키는 log4j 하이브 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="5a484-165">hello 필드 구분 기호는 ",".</span><span class="sxs-lookup"><span data-stu-id="5a484-165">hello field delimiter is ",".</span></span> <span data-ttu-id="5a484-166">hello 기본 줄 구분은 "\n"입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="5a484-167">하이브 외부 테이블은 여러 번 toorun hello Oozie 워크플로에서 하려면 hello 원래 위치에서 제거 되 고 사용 되는 tooavoid hello 데이터 파일.</span><span class="sxs-lookup"><span data-stu-id="5a484-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="5a484-168">**hello 덮어쓰기 삽입 문** hello log4j Hive 테이블에서 각 로그 수준 형식의 hello 발생 수를 세 고 hello 출력 tooa blob Azure 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="5a484-169">Hello 스크립트에 사용 되는 세 개의 변수 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="5a484-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="5a484-170">${hiveTableName}</span></span>
* <span data-ttu-id="5a484-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="5a484-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="5a484-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="5a484-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="5a484-173">hello 워크플로 정의 파일 (이 자습서에서는 workflow.xml) 런타임 시 이러한 값 toothis HiveQL 스크립트를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="5a484-174">Hello 워크플로 파일과 hello HiveQL 파일 모두 blob 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="5a484-175">이 자습서의 뒷부분에서 사용 하는 PowerShell 스크립트 hello 두 파일 toohello 기본 저장소 계정에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="5a484-176">PowerShell을 사용하여 Oozie 작업 제출</span><span class="sxs-lookup"><span data-stu-id="5a484-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="5a484-177">Azure PowerShell은 Oozie 작업을 정의하는 데 현재 어떤 cmdlet도 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="5a484-178">Hello를 사용할 수 있습니다 **Invoke-restmethod** cmdlet tooinvoke Oozie 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="5a484-179">hello Oozie 웹 서비스 API는 HTTP 나머지 JSON API.</span><span class="sxs-lookup"><span data-stu-id="5a484-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="5a484-180">Hello Oozie 웹 서비스 API에 대 한 자세한 내용은 참조 [Apache Oozie 4.0 설명서] [ apache-oozie-400] (용 HDInsight 버전 3.0) 또는 [Apache Oozie 3.3.2 설명서] [ apache-oozie-332] (HDInsight 버전 2.1)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="5a484-181">이 섹션의 PowerShell 스크립트 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="5a484-182">TooAzure를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="5a484-183">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5a484-183">Create an Azure resource group.</span></span> <span data-ttu-id="5a484-184">자세한 내용은 [Azure 리소스 관리자에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a484-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="5a484-185">Azure SQL 데이터베이스 서버, Azure SQL 데이터베이스 및 두 개의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="5a484-186">이러한 hello hello 워크플로에서 Sqoop 작업에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="5a484-187">hello 테이블 이름이 *log4jLogCount*합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="5a484-188">HDInsight 사용 되는 클러스터 toorun Oozie 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="5a484-189">tooexamine hello 클러스터 hello Azure 포털 또는 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="5a484-190">Hello oozie 워크플로 파일과 hello HiveQL 스크립트 파일 toohello 기본 파일 시스템에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="5a484-191">두 파일은 공용 Blob 컨테이너에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="5a484-192">Hello HiveQL 스크립트 (useoozie.hql) tooAzure (wasb:///tutorials/useoozie/useoozie.hql) 저장소에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="5a484-193">Workflow.xml toowasb:///tutorials/useoozie/workflow.xml를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="5a484-194">복사 hello 데이터 파일 (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="5a484-195">Oozie 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="5a484-196">tooexamine hello OOzie 작업 결과 Visual Studio 또는 다른 도구 tooconnect toohello Azure SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="5a484-197">Hello 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-197">Here is hello script.</span></span>  <span data-ttu-id="5a484-198">Windows PowerShell ISE에서 hello 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="5a484-199">Tooconfigure 하기만 하면 처음 7 변수 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

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
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="5a484-200">**toore 실행 hello 자습서**</span><span class="sxs-lookup"><span data-stu-id="5a484-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="5a484-201">toore 실행 hello 워크플로 hello 다음 항목을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="5a484-202">hello Hive 스크립트 출력 파일</span><span class="sxs-lookup"><span data-stu-id="5a484-202">hello Hive script output file</span></span>
* <span data-ttu-id="5a484-203">hello 테이블의에서 데이터를 hello log4jLogsCount</span><span class="sxs-lookup"><span data-stu-id="5a484-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="5a484-204">다음은 사용할 수 있는 PowerShell 스크립트 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="5a484-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a484-205">Next steps</span></span>
<span data-ttu-id="5a484-206">이 자습서에서는 방법에 대해 배웠습니다 toodefine는 Oozie 워크플로와 toorun는 Oozie PowerShell을 사용 하 여 작업 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5a484-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="5a484-207">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="5a484-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="5a484-208">[HDInsight에서 시간 기준의 Oozie 코디네이터 사용][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="5a484-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="5a484-209">[HDInsight tooanalyze 모바일 송수화기 사용 중인 Hadoop 하이브 사용을 시작.][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="5a484-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="5a484-210">[HDInsight에서 Azure Blob Storage 사용][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="5a484-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="5a484-211">[PowerShell을 사용하여 HDInsight 관리][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="5a484-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="5a484-212">[HDInsight에서 Hadoop 작업용 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="5a484-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="5a484-213">[HDInsight에서 Hadoop과 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5a484-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="5a484-214">[HDInsight에서 Hadoop과 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="5a484-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="5a484-215">[HDInsight에서 Hadoop과 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="5a484-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="5a484-216">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="5a484-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
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
