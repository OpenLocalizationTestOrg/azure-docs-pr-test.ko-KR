---
title: "Apache Hive 및 HiveQL-Azure HDInsight aaaWhat은 | Microsoft Docs"
description: "Apache Hive는 Hadoop용 데이터 웨어하우스 시스템입니다. HiveQL을 비슷한 tooTransact-SQL을 사용 하 여 하이브에 저장 된 데이터를 쿼리할 수 있습니다. 이 문서에서는 설명 toouse 하이브 방법 및 Azure HDInsight와 HiveQL 합니다."
keywords: "hiveql, hive, hadoop hiveql 이란 toouse 하이브 하는 방법에 대해 알아봅니다 하이브를 하이브 란"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="5eca0-106">Azure HDInsight의 Apache Hive 및 HiveQL이란?</span><span class="sxs-lookup"><span data-stu-id="5eca0-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="5eca0-107">[Apache Hive](http://hive.apache.org/)는 Hadoop용 데이터 웨어하우스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="5eca0-108">Hive를 사용하면 데이터의 요약, 쿼리 및 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="5eca0-109">하이브 쿼리는 쿼리 언어와 유사한 tooSQL HiveQL로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="5eca0-110">하이브 주로 구조화 되지 않은 데이터에 tooproject 구조를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="5eca0-111">Hello 구조를 정의한 후에 Java 또는 MapReduce 지식 없이 HiveQL tooquery hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="5eca0-112">HDInsight는 특정 워크로드에 맞게 조정되는 여러 클러스터 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="5eca0-113">클러스터 유형만 hello 하이브 쿼리에 대 한 가장 자주 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="5eca0-114">__대화형 하이브__:를 제공 하는 Hadoop 클러스터 [낮은 대기 시간 분석 처리 (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) 대화형 쿼리에 대 한 기능 tooimprove 응답 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="5eca0-115">자세한 내용은 참조 hello [대화형 HDInsight의 Hive 시작](hdinsight-hadoop-use-interactive-hive.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5eca0-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="5eca0-116">__Hadoop__: 배치 프로세싱 워크로드에 대해 조정된 Hadoop 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="5eca0-117">자세한 내용은 참조 hello [HDInsight에서 Hadoop으로 시작](hdinsight-hadoop-linux-tutorial-get-started.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5eca0-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="5eca0-118">__Spark__: Apache Spark는 Hive로 작업하기 위한 기본 제공 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="5eca0-119">자세한 내용은 참조 hello [HDInsight의 spark 시작](hdinsight-apache-spark-jupyter-spark-sql.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5eca0-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="5eca0-120">__HBase__: HiveQL HBase에서 저장 된 데이터를 사용 하는 tooquery 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="5eca0-121">자세한 내용은 참조 hello [HDInsight에서 HBase 시작](hdinsight-hbase-tutorial-get-started-linux.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5eca0-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="5eca0-122">Toouse 하이브 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5eca0-122">How toouse Hive</span></span>

<span data-ttu-id="5eca0-123">HDInsight와 toouse 하이브 어떻게 테이블 toodiscover 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="5eca0-124">다음을 원하는 경우 **이 메서드를 사용**...</span><span class="sxs-lookup"><span data-stu-id="5eca0-124">**Use this method** if you want...</span></span> | <span data-ttu-id="5eca0-125">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="5eca0-125">...an **interactive** shell</span></span> | <span data-ttu-id="5eca0-126">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="5eca0-126">...**batch** processing</span></span> | <span data-ttu-id="5eca0-127">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="5eca0-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="5eca0-128">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="5eca0-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="5eca0-129">Hive 보기</span><span class="sxs-lookup"><span data-stu-id="5eca0-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="5eca0-130">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-130">✔</span></span> |<span data-ttu-id="5eca0-131">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-131">✔</span></span> |<span data-ttu-id="5eca0-132">Linux</span><span class="sxs-lookup"><span data-stu-id="5eca0-132">Linux</span></span> |<span data-ttu-id="5eca0-133">모두(브라우저 기반)</span><span class="sxs-lookup"><span data-stu-id="5eca0-133">Any (browser based)</span></span> |
| [<span data-ttu-id="5eca0-134">Beeline 클라이언트</span><span class="sxs-lookup"><span data-stu-id="5eca0-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="5eca0-135">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-135">✔</span></span> |<span data-ttu-id="5eca0-136">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-136">✔</span></span> |<span data-ttu-id="5eca0-137">Linux</span><span class="sxs-lookup"><span data-stu-id="5eca0-137">Linux</span></span> |<span data-ttu-id="5eca0-138">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="5eca0-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="5eca0-139">REST API</span><span class="sxs-lookup"><span data-stu-id="5eca0-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="5eca0-140">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-140">✔</span></span> |<span data-ttu-id="5eca0-141">Linux 또는 Windows*</span><span class="sxs-lookup"><span data-stu-id="5eca0-141">Linux or Windows*</span></span> |<span data-ttu-id="5eca0-142">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="5eca0-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="5eca0-143">Visual Studio용 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="5eca0-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="5eca0-144">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-144">✔</span></span> |<span data-ttu-id="5eca0-145">Linux 또는 Windows*</span><span class="sxs-lookup"><span data-stu-id="5eca0-145">Linux or Windows*</span></span> |<span data-ttu-id="5eca0-146">Windows</span><span class="sxs-lookup"><span data-stu-id="5eca0-146">Windows</span></span> |
| [<span data-ttu-id="5eca0-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5eca0-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="5eca0-148">✔</span><span class="sxs-lookup"><span data-stu-id="5eca0-148">✔</span></span> |<span data-ttu-id="5eca0-149">Linux 또는 Windows*</span><span class="sxs-lookup"><span data-stu-id="5eca0-149">Linux or Windows*</span></span> |<span data-ttu-id="5eca0-150">Windows</span><span class="sxs-lookup"><span data-stu-id="5eca0-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5eca0-151">\*Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5eca0-152">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5eca0-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="5eca0-153">Windows 기반 HDInsight 클러스터를 사용 하는 경우에 hello을 사용할 수 있습니다 [쿼리 콘솔](hdinsight-hadoop-use-hive-query-console.md) 브라우저에서 또는 [원격 데스크톱](hdinsight-hadoop-use-hive-remote-desktop.md) toorun 하이브 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="5eca0-154">HiveQL 언어 참조</span><span class="sxs-lookup"><span data-stu-id="5eca0-154">HiveQL language reference</span></span>

<span data-ttu-id="5eca0-155">HiveQL 언어 참조는 hello에서 사용할 수 있는 [언어 설명서 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="5eca0-156">Hive 및 데이터 구조</span><span class="sxs-lookup"><span data-stu-id="5eca0-156">Hive and data structure</span></span>

<span data-ttu-id="5eca0-157">하이브는 toowork로 구성 하는 방식을 반 구조화 된 데이터를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="5eca0-158">예를 들어 텍스트 파일 hello 필드 특정 문자로 구분 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="5eca0-159">HiveQL 문 다음 hello 공백으로 구분 된 데이터에 대해 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="5eca0-160">또한 Hive는 복잡하거나 불규칙하게 구조화된 데이터에 대한 사용자 지정을 **serializer/deserializers(SerDe)** 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="5eca0-161">자세한 내용은 참조 hello [어떻게 toouse HDInsight와 사용자 지정 JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) 문서.</span><span class="sxs-lookup"><span data-stu-id="5eca0-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="5eca0-162">하이브에서 지 원하는 파일 형식에 대 한 자세한 내용은 참조 hello [언어 설명서 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="5eca0-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="5eca0-163">Hive 내부 테이블과 외부 테이블 비교</span><span class="sxs-lookup"><span data-stu-id="5eca0-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="5eca0-164">Hive로 다음과 같은 두 가지 형식의 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="5eca0-165">__내부__: hello 하이브 데이터 웨어하우스에 저장 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="5eca0-166">hello 데이터 웨어하우스는에 `/hive/warehouse/` hello 클러스터에 대 한 hello 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="5eca0-167">다음과 같은 경우에 내부 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-167">Use internal tables when:</span></span>

    * <span data-ttu-id="5eca0-168">데이터가 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-168">Data is temporary.</span></span>
    * <span data-ttu-id="5eca0-169">하이브 toomanage hello 수명 주기를 hello 테이블 및 데이터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="5eca0-170">__외부__: hello 데이터 웨어하우스 외부 데이터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="5eca0-171">hello 데이터 hello 클러스터에서 액세스할 수 있는 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="5eca0-172">다음과 같은 경우에 외부 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-172">Use external tables when:</span></span>

    * <span data-ttu-id="5eca0-173">하이브 외부 hello 데이터도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="5eca0-174">예를 들어 hello 데이터 파일 (즉 잠그지 않습니다 hello 파일.) 다른 프로세스에 의해 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="5eca0-175">데이터의 위치를 hello 테이블을 삭제 한 후에 기본 hello tooremain이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="5eca0-176">기본이 아닌 저장소 계정과 같은 사용자 지정 위치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="5eca0-177">하이브 이외의 프로그램 hello 데이터 형식, 위치 등을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="5eca0-178">자세한 내용은 참조 hello [하이브 내부 및 외부 테이블 소개] [ cindygross-hive-tables] 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="5eca0-179">UDF(사용자 정의 함수)</span><span class="sxs-lookup"><span data-stu-id="5eca0-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="5eca0-180">Hive는 **사용자 정의 함수(UDF)**를 통해 확장 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="5eca0-181">UDF는 tooimplement 기능이 나 HiveQL에서 쉽게 모델링 되지 논리를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="5eca0-182">하이브 Udf 사용의 예를 들어 hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5eca0-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="5eca0-183">Hive와 함께 Java 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="5eca0-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="5eca0-184">Hive 및 Pig와 함께 Python 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="5eca0-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="5eca0-185">Hive 및 Pig와 함께 C# 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="5eca0-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="5eca0-186">사용자 정의 사용자 지정 하이브 tooadd tooHDInsight 작동 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5eca0-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="5eca0-187">예제 하이브 사용자 정의 함수 tooconvert 날짜/시간 형식 tooHive 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="5eca0-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="5eca0-188"><a id="data"></a>예제 데이터</span><span class="sxs-lookup"><span data-stu-id="5eca0-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="5eca0-189">HDInsight에서 Hive는 `hivesampletable`이라는 내부 테이블로 미리 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="5eca0-190">또한 HDInsight는 Hive와 함께 사용할 수 있는 예제 데이터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="5eca0-191">이러한 데이터 집합 hello에 저장 된 `/example/data` 및 `/HdiSamples` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="5eca0-192">이 디렉터리는 클러스터에 대 한 hello 기본 저장소에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="5eca0-193"><a id="job"></a>예제 Hive 쿼리</span><span class="sxs-lookup"><span data-stu-id="5eca0-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="5eca0-194">HiveQL 문은 프로젝트 열 hello에 끌어 다음 hello `/example/data/sample.log` 파일:</span><span class="sxs-lookup"><span data-stu-id="5eca0-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="5eca0-195">Hello 앞의 예제에서 hello HiveQL 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="5eca0-196">`set hive.execution.engine=tez;`: 세트 실행 엔진 toouse Tez hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="5eca0-197">MapReduce 대신 Tez를 사용하면 쿼리 성능 향상을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="5eca0-198">Tez에 자세한 내용은 참조 hello [성능 향상된을 위해 사용 하 여 Apache Tez](#usetez) 섹션.</span><span class="sxs-lookup"><span data-stu-id="5eca0-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5eca0-199">이 문은 Windows 기반 HDInsight 클러스터를 사용할 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="5eca0-200">Tez은 Linux 기반 HDInsight 용 hello 기본 실행 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="5eca0-201">`DROP TABLE`: Hello 테이블이 이미 존재 하는 경우이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="5eca0-202">`CREATE EXTERNAL TABLE`: Hive에서 새 **외부** 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="5eca0-203">외부 테이블만 하이브에 hello 테이블 정의 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="5eca0-204">hello 데이터 hello 원래 형태로 표시 하 고 hello 원래 위치에 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="5eca0-205">`ROW FORMAT`: 하이브 hello 데이터 형식 지정 방법을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="5eca0-206">이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="5eca0-207">`STORED AS TEXTFILE LOCATION`: 지시 하이브 여기서 hello 데이터가 저장 됩니다 (hello `example/data` 디렉터리) 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="5eca0-208">hello 데이터 hello 디렉터리 내에서 여러 파일에 걸쳐 분산 또는 한 파일에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="5eca0-209">`SELECT`: 모든 행의 개수를 hello 선택 열 **t4** hello 값이 포함 된 **[오류]**합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="5eca0-210">이 값을 포함하는 행이 3개 있으므로 이 문은 **3** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="5eca0-211">`INPUT__FILE__NAME LIKE '%.log'`-하이브 tooapply hello 스키마 tooall hello 디렉터리에 파일을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="5eca0-212">이 경우 hello 디렉터리 hello 스키마와 일치 하지 않는 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="5eca0-213">tooprevent 가비지 데이터 hello 결과에,이 문은 알 수 하이브 것만 반환할지 여부를 데이터 파일의 끝에서. 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="5eca0-214">외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="5eca0-215">예를 들어 자동화된 데이터 업로드 프로세스 또는 MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="5eca0-216">외부 테이블 삭제는 **하지** hello 데이터 삭제 hello 테이블 정의 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="5eca0-217">toocreate는 **내부** 대신 외부 테이블에서 다음 HiveQL hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5eca0-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="5eca0-218">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="5eca0-219">`CREATE TABLE IF NOT EXISTS`: Hello 테이블이 존재 하지 않는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="5eca0-220">때문에 hello **외부** 키워드가 사용 되지 않습니다,이 문은 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="5eca0-221">hello hello 하이브 데이터 웨어하우스에 저장 된 테이블과 하이브에서 완전히 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="5eca0-222">`STORED AS ORC`: Hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="5eca0-223">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="5eca0-224">`INSERT OVERWRITE ... SELECT`: Hello에서 행을 선택 합니다. **log4jLogs** 포함 된 테이블 **[오류]**, 다음 hello에 데이터 hello를 삽입 하 고 **살펴볼** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="5eca0-225">외부 테이블의 경우와 달리 hello 기본 데이터를 삭제도 내부 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="5eca0-226">Hive 쿼리 성능 향상</span><span class="sxs-lookup"><span data-stu-id="5eca0-226">Improve Hive query performance</span></span>

### <span data-ttu-id="5eca0-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="5eca0-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="5eca0-228">[Apache Tez](http://tez.apache.org) 는 하이브를 규모에 훨씬 더 효율적으로 toorun 등 데이터 중심 응용 프로그램을 허용 하는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="5eca0-229">Tez는 Linux 기반 HDInsight 클러스터에 대해 기본값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="5eca0-230">Tez는 현재 Windows 기반 HDInsight 클러스터에 대해 기본적으로 꺼져 있으며 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="5eca0-231">하이브 쿼리용 tootake 활용 Tez, 다음 값 hello 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="5eca0-232">Tez은 Linux 기반 HDInsight 클러스터에 대 한 hello 기본 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="5eca0-233">hello [Tez 디자인 문서에서 하이브](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) hello 구현 선택 항목 및 튜닝 구성 하는 방법에 대 한 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="5eca0-234">작업을 디버깅 tooaid Tez를 사용 하 여 실행, HDInsight hello 다음 Tez 작업의 tooview 세부 정보를 사용할 수 있는 웹 Ui를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="5eca0-235">Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5eca0-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="5eca0-236">Windows 기반 HDInsight의 hello Tez UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5eca0-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="5eca0-237">LLAP(짧은 대기 시간 분석 처리)</span><span class="sxs-lookup"><span data-stu-id="5eca0-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="5eca0-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP)(Live Long and Process라고도 함)는 쿼리의 메모리 내 캐싱을 수행할 수 있는 Hive 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="5eca0-239">LLAP는 하이브 쿼리를 훨씬 빠르게 너무[26 x 일부 경우에는 1.x 하이브 보다 더 빠르게](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="5eca0-240">HDInsight은 클러스터 유형 대화형 하이브 hello LLAP를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="5eca0-241">자세한 내용은 참조 hello [대화형 하이브 시작](hdinsight-hadoop-use-interactive-hive.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5eca0-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="5eca0-242">Hive 작업 및 SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="5eca0-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="5eca0-243">SQL Server Integration Services (SSIS) toorun 하이브 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="5eca0-244">SSIS 용 Azure 기능 팩 hello 다음과 같은 구성 요소가 HDInsight의 Hive 작업을 사용 하는 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="5eca0-245">[Azure HDInsight Hive 작업][hivetask]</span><span class="sxs-lookup"><span data-stu-id="5eca0-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="5eca0-246">[Azure 구독 연결 관리자][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="5eca0-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="5eca0-247">자세한 정보 hello Azure 기능 팩에 대 한 SSIS [여기][ssispack]합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="5eca0-248"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="5eca0-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5eca0-249">하이브 이란 배운 했으므로 방식과 HDInsight 사용 하 여 hello 뒤에서 Hadoop으로 연결 tooexplore Azure HDInsight와 다른 방법으로 toowork toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eca0-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="5eca0-250">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="5eca0-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="5eca0-251">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="5eca0-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="5eca0-252">[HDInsight에서 MapReduce 작업 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="5eca0-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
