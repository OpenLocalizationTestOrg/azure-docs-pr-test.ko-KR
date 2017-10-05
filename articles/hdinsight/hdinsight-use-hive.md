---
title: "Apache Hive 및 HiveQL이란? - Azure HDInsight | Microsoft Docs"
description: "Apache Hive는 Hadoop용 데이터 웨어하우스 시스템입니다. Transact-SQL과 유사하게 HiveQL을 사용하여 Hive에 저장된 데이터를 쿼리할 수 있습니다. 이 문서에서는 Azure HDInsight와 함께 Hive 및 HiveQL을 사용하는 방법에 알아봅니다."
keywords: hiveql,what is hive,hadoop hiveql,how to use hive,learn hive,what is hive
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
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="3c30c-106">Azure HDInsight의 Apache Hive 및 HiveQL이란?</span><span class="sxs-lookup"><span data-stu-id="3c30c-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="3c30c-107">[Apache Hive](http://hive.apache.org/)는 Hadoop용 데이터 웨어하우스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="3c30c-108">Hive를 사용하면 데이터의 요약, 쿼리 및 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="3c30c-109">Hive 쿼리는 SQL과 유사한 쿼리 언어인 HiveQL로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="3c30c-110">Hive를 사용하면 크게 구조가 없는 데이터에 구조를 투영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="3c30c-111">구조를 정의한 후에 Java 또는 MapReduce 지식 없이 해당 데이터를 쿼리할 때에 HiveQL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="3c30c-112">HDInsight는 특정 워크로드에 맞게 조정되는 여러 클러스터 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="3c30c-113">다음과 같은 클러스터 형식이 Hive 쿼리에 가장 자주 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="3c30c-114">__대화형 Hive__: [LLAP(낮은 대기 시간 분석 처리)](https://cwiki.apache.org/confluence/display/Hive/LLAP) 기능을 제공하여 대화형 쿼리에 대한 응답 시간을 개선하는 Hadoop 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="3c30c-115">자세한 내용은 [HDInsight의 대화형 Hive로 시작](hdinsight-hadoop-use-interactive-hive.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="3c30c-116">__Hadoop__: 배치 프로세싱 워크로드에 대해 조정된 Hadoop 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="3c30c-117">자세한 내용은 [HDInsight의 Hadoop으로 시작](hdinsight-hadoop-linux-tutorial-get-started.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="3c30c-118">__Spark__: Apache Spark는 Hive로 작업하기 위한 기본 제공 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="3c30c-119">자세한 내용은 [HDInsight의 Spark로 시작](hdinsight-apache-spark-jupyter-spark-sql.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="3c30c-120">__HBase__: HiveQL은 HBase에 저장된 데이터를 쿼리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="3c30c-121">자세한 내용은 [HDInsight의 HBase로 시작](hdinsight-hbase-tutorial-get-started-linux.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="3c30c-122">Hive 사용 방법</span><span class="sxs-lookup"><span data-stu-id="3c30c-122">How to use Hive</span></span>

<span data-ttu-id="3c30c-123">다음 테이블을 사용하여 HDInsight와 함께 Hive를 사용하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="3c30c-124">다음을 원하는 경우 **이 메서드를 사용**...</span><span class="sxs-lookup"><span data-stu-id="3c30c-124">**Use this method** if you want...</span></span> | <span data-ttu-id="3c30c-125">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="3c30c-125">...an **interactive** shell</span></span> | <span data-ttu-id="3c30c-126">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="3c30c-126">...**batch** processing</span></span> | <span data-ttu-id="3c30c-127">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="3c30c-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="3c30c-128">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="3c30c-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="3c30c-129">Hive 보기</span><span class="sxs-lookup"><span data-stu-id="3c30c-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="3c30c-130">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-130">✔</span></span> |<span data-ttu-id="3c30c-131">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-131">✔</span></span> |<span data-ttu-id="3c30c-132">Linux</span><span class="sxs-lookup"><span data-stu-id="3c30c-132">Linux</span></span> |<span data-ttu-id="3c30c-133">모두(브라우저 기반)</span><span class="sxs-lookup"><span data-stu-id="3c30c-133">Any (browser based)</span></span> |
| [<span data-ttu-id="3c30c-134">Beeline 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3c30c-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="3c30c-135">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-135">✔</span></span> |<span data-ttu-id="3c30c-136">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-136">✔</span></span> |<span data-ttu-id="3c30c-137">Linux</span><span class="sxs-lookup"><span data-stu-id="3c30c-137">Linux</span></span> |<span data-ttu-id="3c30c-138">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="3c30c-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3c30c-139">REST API</span><span class="sxs-lookup"><span data-stu-id="3c30c-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="3c30c-140">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-140">✔</span></span> |<span data-ttu-id="3c30c-141">Linux 또는 Windows*</span><span class="sxs-lookup"><span data-stu-id="3c30c-141">Linux or Windows*</span></span> |<span data-ttu-id="3c30c-142">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="3c30c-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3c30c-143">Visual Studio용 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="3c30c-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="3c30c-144">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-144">✔</span></span> |<span data-ttu-id="3c30c-145">Linux 또는 Windows*</span><span class="sxs-lookup"><span data-stu-id="3c30c-145">Linux or Windows*</span></span> |<span data-ttu-id="3c30c-146">Windows</span><span class="sxs-lookup"><span data-stu-id="3c30c-146">Windows</span></span> |
| [<span data-ttu-id="3c30c-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c30c-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="3c30c-148">✔</span><span class="sxs-lookup"><span data-stu-id="3c30c-148">✔</span></span> |<span data-ttu-id="3c30c-149">Linux 또는 Windows*</span><span class="sxs-lookup"><span data-stu-id="3c30c-149">Linux or Windows*</span></span> |<span data-ttu-id="3c30c-150">Windows</span><span class="sxs-lookup"><span data-stu-id="3c30c-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3c30c-151">\* Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3c30c-152">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="3c30c-153">Windows 기반 HDInsight 클러스터를 사용하는 경우 브라우저에서 [쿼리 콘솔](hdinsight-hadoop-use-hive-query-console.md) 또는 [원격 데스크톱](hdinsight-hadoop-use-hive-remote-desktop.md)을 사용하여 Hive 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="3c30c-154">HiveQL 언어 참조</span><span class="sxs-lookup"><span data-stu-id="3c30c-154">HiveQL language reference</span></span>

<span data-ttu-id="3c30c-155">HiveQL 언어 참조는 [언어 설명서(https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="3c30c-156">Hive 및 데이터 구조</span><span class="sxs-lookup"><span data-stu-id="3c30c-156">Hive and data structure</span></span>

<span data-ttu-id="3c30c-157">Hive는 구조화되거나 반구조화된 데이터로 작업하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="3c30c-158">예를 들어 필드가 특정 문자로 구분된 텍스트 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="3c30c-159">다음 HiveQL 문은 공백으로 구분된 데이터에 대해 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="3c30c-160">또한 Hive는 복잡하거나 불규칙하게 구조화된 데이터에 대한 사용자 지정을 **serializer/deserializers(SerDe)** 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="3c30c-161">자세한 내용은 [HDInsight와 함께 사용자 지정 JSON SerDe를 사용하는 방법](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="3c30c-162">Hive에서 지원하는 파일 형식에 대한 자세한 내용은 [언어 설명서(https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="3c30c-163">Hive 내부 테이블과 외부 테이블 비교</span><span class="sxs-lookup"><span data-stu-id="3c30c-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="3c30c-164">Hive로 다음과 같은 두 가지 형식의 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="3c30c-165">__내부__: 데이터가 Hive 데이터 웨어하우스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="3c30c-166">데이터 웨어하우스는 클러스터의 기본 저장소인 `/hive/warehouse/`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="3c30c-167">다음과 같은 경우에 내부 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-167">Use internal tables when:</span></span>

    * <span data-ttu-id="3c30c-168">데이터가 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-168">Data is temporary.</span></span>
    * <span data-ttu-id="3c30c-169">Hive로 테이블 및 데이터의 수명 주기를 관리하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="3c30c-170">__외부__: 데이터가 데이터 웨어하우스 외부에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="3c30c-171">클러스터에서 액세스할 수 있는 저장소에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="3c30c-172">다음과 같은 경우에 외부 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-172">Use external tables when:</span></span>

    * <span data-ttu-id="3c30c-173">데이터를 Hive 외부에서도 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="3c30c-174">예를 들어, 데이터 파일이 다른 프로세스에 의해 업데이트됩니다(파일을 잠그지 않음).</span><span class="sxs-lookup"><span data-stu-id="3c30c-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="3c30c-175">테이블을 삭제한 후에도 데이터는 기본 위치에 남아 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="3c30c-176">기본이 아닌 저장소 계정과 같은 사용자 지정 위치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="3c30c-177">Hive가 아닌 프로그램이 데이터 형식, 위치 등을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="3c30c-178">자세한 내용은 [Hive 내부 및 외부 테이블 소개][cindygross-hive-tables] 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="3c30c-179">UDF(사용자 정의 함수)</span><span class="sxs-lookup"><span data-stu-id="3c30c-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="3c30c-180">Hive는 **사용자 정의 함수(UDF)**를 통해 확장 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="3c30c-181">UDF를 사용하면 HiveQL에서 쉽게 모델링할 수 있는 기능 또는 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="3c30c-182">Hive와 함께 UDF를 사용하는 방법의 예는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="3c30c-183">Hive와 함께 Java 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="3c30c-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="3c30c-184">Hive 및 Pig와 함께 Python 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="3c30c-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="3c30c-185">Hive 및 Pig와 함께 C# 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="3c30c-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="3c30c-186">HDInsight에 사용자 지정 Hive 사용자 정의 함수를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c30c-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="3c30c-187">날짜/시간 형식을 Hive 타임스탬프로 변환하는 Hive 사용자 지정 함수 예제</span><span class="sxs-lookup"><span data-stu-id="3c30c-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="3c30c-188"><a id="data"></a>예제 데이터</span><span class="sxs-lookup"><span data-stu-id="3c30c-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="3c30c-189">HDInsight에서 Hive는 `hivesampletable`이라는 내부 테이블로 미리 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="3c30c-190">또한 HDInsight는 Hive와 함께 사용할 수 있는 예제 데이터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="3c30c-191">이러한 데이터 집합은 `/example/data` 및 `/HdiSamples` 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="3c30c-192">이러한 디렉터리는 클러스터의 기본 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="3c30c-193"><a id="job"></a>예제 Hive 쿼리</span><span class="sxs-lookup"><span data-stu-id="3c30c-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="3c30c-194">다음 HiveQL 문은 열을 `/example/data/sample.log` 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="3c30c-195">이전 예제에서 HiveQL 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="3c30c-196">`set hive.execution.engine=tez;`: Tez를 사용하도록 실행 엔진을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="3c30c-197">MapReduce 대신 Tez를 사용하면 쿼리 성능 향상을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="3c30c-198">Tez에 대한 자세한 내용은 [향상된 성능을 위해 Apache Tez 사용](#usetez)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3c30c-199">이 문은 Windows 기반 HDInsight 클러스터를 사용할 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="3c30c-200">Tez는 Linux 기반 HDInsight의 기본 실행 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="3c30c-201">`DROP TABLE`: 이미 테이블이 있는 경우 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="3c30c-202">`CREATE EXTERNAL TABLE`: Hive에서 새 **외부** 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="3c30c-203">외부 테이블만 테이블 정의를 Hive에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="3c30c-204">데이터는 원래 위치에 원래 형식으로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="3c30c-205">`ROW FORMAT`: 데이터의 형식 지정 방식을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="3c30c-206">이 경우, 각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="3c30c-207">`STORED AS TEXTFILE LOCATION`: 데이터가 저장된 위치(`example/data` 디렉터리) 및 텍스트로 저장되었음을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="3c30c-208">데이터는 디렉터리 내에서 하나의 파일 또는 여러 파일에 걸쳐 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="3c30c-209">`SELECT`: **t4** 열에 **[ERROR]** 값이 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="3c30c-210">이 값을 포함하는 행이 3개 있으므로 이 문은 **3** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="3c30c-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive는 디렉터리의 모든 파일에 스키마를 적용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="3c30c-212">이 경우 디렉터리에 스키마와 일치하지 않는 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="3c30c-213">결과에 가비지 데이터가 나타나는 것을 방지하기 위해 이 문은 .log로 끝나는 파일의 데이터만 반환해야 함을 Hive에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="3c30c-214">외부 원본에서 기본 데이터를 업데이트하길 원하는 경우에는 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="3c30c-215">예를 들어 자동화된 데이터 업로드 프로세스 또는 MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="3c30c-216">외부 테이블을 삭제하면 데이터가 삭제되지 **않고** 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="3c30c-217">외부 테이블 대신 **내부** 테이블을 만들려면 다음 HiveQL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="3c30c-218">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="3c30c-219">`CREATE TABLE IF NOT EXISTS`: 테이블이 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="3c30c-220">**EXTERNAL** 키워드가 사용되지 않으므로 이 문은 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="3c30c-221">테이블은 Hive 데이터 웨어하우스에 저장되며 Hive에서 전적으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="3c30c-222">`STORED AS ORC`: 데이터를 ORC(Optimized Row Columnar) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="3c30c-223">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="3c30c-224">`INSERT OVERWRITE ... SELECT`: **[ERROR]**가 포함된 **log4jLogs** 테이블에서 행을 선택하고 데이터를 **errorLogs** 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="3c30c-225">외부 테이블과 달리 내부 테이블을 삭제하면 기본 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="3c30c-226">Hive 쿼리 성능 향상</span><span class="sxs-lookup"><span data-stu-id="3c30c-226">Improve Hive query performance</span></span>

### <span data-ttu-id="3c30c-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="3c30c-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="3c30c-228">[Apache Tez](http://tez.apache.org) 는 Hive와 같이 데이터를 많이 사용하는 응용 프로그램을 큰 규모에서도 훨씬 더 효율적으로 실행할 수 있는 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="3c30c-229">Tez는 Linux 기반 HDInsight 클러스터에 대해 기본값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="3c30c-230">Tez는 현재 Windows 기반 HDInsight 클러스터에 대해 기본적으로 꺼져 있으며 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="3c30c-231">Tez를 사용하려면 Hive 쿼리에 대해 다음 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="3c30c-232">Tez는 Linux 기반 HDInsight 클러스터의 기본 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="3c30c-233">[Tez의 Hive 디자인 문서](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)에는 선택 가능한 구현 및 튜닝 구성과 관련된 세부 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="3c30c-234">Tez를 사용하여 실행된 작업을 디버깅하도록 보조하려면 HDInsight는 Tez 작업의 세부 정보를 볼 수 있도록 다음 웹 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="3c30c-235">Linux 기반 HDInsight에서 Ambari Tez 보기 사용</span><span class="sxs-lookup"><span data-stu-id="3c30c-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="3c30c-236">Windows 기반 HDInsight 클러스터에서 Tez UI 사용</span><span class="sxs-lookup"><span data-stu-id="3c30c-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="3c30c-237">LLAP(짧은 대기 시간 분석 처리)</span><span class="sxs-lookup"><span data-stu-id="3c30c-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="3c30c-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP)(Live Long and Process라고도 함)는 쿼리의 메모리 내 캐싱을 수행할 수 있는 Hive 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="3c30c-239">LLAP 덕분에 Hive 쿼리를 훨씬 빠르게, [일부 경우에는 Hive 1.x보다 26배 더 빠르게](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/) 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="3c30c-240">HDInsight는 대화형 Hive 클러스터 형식으로 LLAP를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="3c30c-241">자세한 내용은 [대화형 Hive로 시작](hdinsight-hadoop-use-interactive-hive.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="3c30c-242">Hive 작업 및 SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="3c30c-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="3c30c-243">SSIS(SQL Server Integration Services)를 사용하여 Hive 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="3c30c-244">Azure Feature Pack for SSIS는 HDInsight에서 Hive 작업을 하는 다음 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="3c30c-245">[Azure HDInsight Hive 작업][hivetask]</span><span class="sxs-lookup"><span data-stu-id="3c30c-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="3c30c-246">[Azure 구독 연결 관리자][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="3c30c-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="3c30c-247">[여기][ssispack]에서 Azure Feature Pack for SSIS에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3c30c-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="3c30c-248"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c30c-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3c30c-249">이제 Hive의 정의 및 HDInsight에서 Hadoop와 Hive를 사용하는 방법을 살펴보았으므로 다음 링크를 사용하여 Azure HDInsight로 작업하는 다른 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c30c-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="3c30c-250">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="3c30c-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="3c30c-251">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3c30c-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3c30c-252">[HDInsight에서 MapReduce 작업 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3c30c-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
