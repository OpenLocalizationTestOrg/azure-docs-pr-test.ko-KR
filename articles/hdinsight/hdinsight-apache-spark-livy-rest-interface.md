---
title: "Azure HDInsight의 aaaUse 리비 Spark toosubmit 작업 tooSpark 클러스터 | Microsoft Docs"
description: "어떻게 toouse Apache Spark REST API toosubmit Spark 작업 원격으로 tooan Azure HDInsight 클러스터에 알아봅니다."
keywords: apache spark rest api, livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="aaf45-104">Apache Spark REST API toosubmit 원격 작업 tooan HDInsight Spark 클러스터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="aaf45-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="aaf45-105">Toouse 리비, hello Apache Spark REST API 사용 되는 toosubmit 원격 인 tooan Azure HDInsight Spark 클러스터를 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="aaf45-106">자세한 설명서는 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aaf45-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="aaf45-107">리비 toorun 대화형 Spark 셸 사용 하거나 Spark에서 실행 하는 일괄 처리 작업 toobe 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="aaf45-108">이 문서 리비 toosubmit 일괄 처리 작업을 사용 하는 방법에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="aaf45-109">이 문서에서 hello 조각을 cURL toomake REST API 호출 toohello 리비 Spark 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="aaf45-110">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="aaf45-110">**Prerequisites:**</span></span>

* <span data-ttu-id="aaf45-111">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="aaf45-112">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aaf45-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="aaf45-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="aaf45-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="aaf45-114">이 문서에서는 cURL toodemonstrate HDInsight Spark 클러스터에 대해 toomake REST API 호출 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="aaf45-115">Livy Spark 배치 작업 제출</span><span class="sxs-lookup"><span data-stu-id="aaf45-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="aaf45-116">일괄 작업을 제출 하기 전에 hello 응용 프로그램 jar hello 클러스터와 연결 된 hello 클러스터 저장소에 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="aaf45-117">사용할 수 있습니다 [ **AzCopy**](../storage/common/storage-use-azcopy.md), 명령줄 유틸리티, toodo 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="aaf45-118">다른 다양 한 클라이언트를 tooupload 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="aaf45-119">[HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="aaf45-120">**예제**:</span><span class="sxs-lookup"><span data-stu-id="aaf45-120">**Examples**:</span></span>

* <span data-ttu-id="aaf45-121">Hello jar 파일이 hello 클러스터 저장소 (WASB)에 있으면</span><span class="sxs-lookup"><span data-stu-id="aaf45-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="aaf45-122">Toopass hello jar 파일 이름 및 입력된 파일의 일부로 classname hello (이 예제에서는 input.txt)</span><span class="sxs-lookup"><span data-stu-id="aaf45-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="aaf45-123">Hello 클러스터에서 실행 되는 Spark 리비 일괄 처리에 대 한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="aaf45-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="aaf45-124">**예제**:</span><span class="sxs-lookup"><span data-stu-id="aaf45-124">**Examples**:</span></span>

* <span data-ttu-id="aaf45-125">Tooretrieve hello 클러스터에서 실행 중인 모든 hello 리비 Spark 배치 하려면:</span><span class="sxs-lookup"><span data-stu-id="aaf45-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="aaf45-126">Tooretrieve 주어진된 batchId와 특정 일괄 처리 하려는 경우</span><span class="sxs-lookup"><span data-stu-id="aaf45-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="aaf45-127">Livy Spark 배치 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="aaf45-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="aaf45-128">**예제**:</span><span class="sxs-lookup"><span data-stu-id="aaf45-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="aaf45-129">Livy Spark 및 고가용성</span><span class="sxs-lookup"><span data-stu-id="aaf45-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="aaf45-130">리비는 hello 클러스터에서 실행 되는 Spark 작업에 대 한 고가용성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="aaf45-131">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="aaf45-132">원격으로 작업을 제출 하 고 나면 hello 리비 서비스 작동이 중지 된 경우 tooa Spark 클러스터를 hello 작업 toorun hello 백그라운드에서 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="aaf45-133">백업 리비 이면 hello 작업 및 다시 보고서의 hello 상태를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="aaf45-134">HDInsight에 대 한 Jupyter 노트북 hello 백 엔드에서 리비에 의해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="aaf45-135">노트북 Spark 작업을 실행 하는 경우 hello 리비 서비스 다시 시작을 가져옵니다 hello 노트북은 toorun hello 코드 셀을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="aaf45-136">예제 보기</span><span class="sxs-lookup"><span data-stu-id="aaf45-136">Show me an example</span></span>
<span data-ttu-id="aaf45-137">이 섹션에서는 예제 toouse 리비 Spark toosubmit 일괄 작업 확인, hello 작업의 hello 진행률을 모니터링 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="aaf45-138">hello 응용 프로그램을 사용 하 여이 예제는 hello hello 문서에서 개발한 하나 [HDInsight Spark 클러스터에서 독립 실행형 Scala 응용 프로그램 및 toorun 만들기](hdinsight-apache-spark-create-standalone-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="aaf45-139">hello 단계 여기 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-139">hello steps here assume that:</span></span>

* <span data-ttu-id="aaf45-140">Hello 클러스터와 연결 된 hello 응용 프로그램 jar toohello 저장소 계정을 이미 복사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="aaf45-141">CuRL 다음이 단계 시도 하 고 있는 hello 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="aaf45-142">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="aaf45-143">주세요 먼저 확인 리비 Spark hello 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="aaf45-144">실행 중인 배치 목록을 가져와서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="aaf45-145">사용 하 여 리비 hello에 대 한 처음으로 작업을 실행 하는 경우 hello 출력 0을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="aaf45-146">다음 코드 조각 출력 유사한 toohello을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="aaf45-147">Hello 출력의 마지막 줄에서는 hello 이라고 표시 방법을 **총: 0**, 실행 중인 일괄 처리가 제안입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="aaf45-148">이제 배치 작업을 제출하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-148">Let us now submit a batch job.</span></span> <span data-ttu-id="aaf45-149">다음 코드 조각 hello 매개 변수로 입력된 파일 (input.txt) toopass hello jar 이름 및 hello 클래스 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="aaf45-150">Windows 컴퓨터에서 다음이 단계를 실행 하는 경우 hello 권장 접근법은 입력된 파일 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="aaf45-151">hello 파일의 매개 변수를 hello **input.txt** ´ ï ´ ù.</span><span class="sxs-lookup"><span data-stu-id="aaf45-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="aaf45-152">다음 코드 조각 출력 유사한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="aaf45-153">Hello hello 출력의 마지막 행 이라고 표시 방법을 **상태: 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="aaf45-154">또한 **id:0**을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-154">It also says, **id:0**.</span></span> <span data-ttu-id="aaf45-155">여기에서 **0** hello 일괄 처리 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="aaf45-156">이제 hello 일괄 처리 id입니다. 사용 하 여이 특정 일괄 처리의 hello 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="aaf45-157">다음 코드 조각 출력 유사한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="aaf45-158">hello 출력에서는 이제 **상태: 성공**, 해당 hello 작업 제안는 성공적으로 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="aaf45-159">원하는 경우 이제 hello 일괄 처리를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="aaf45-160">다음 코드 조각 출력 유사한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="aaf45-161">hello hello 출력의 마지막 줄에서는 해당 hello 일괄 처리 삭제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="aaf45-162">Hello 작업을 해제도 실행 되는 동안 작업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="aaf45-163">그렇지 않은 경우 또는 성공적으로 완료 된 작업을 삭제 하는 경우 작업 정보 hello 완전히 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="aaf45-164">HDInsight 3.5 클러스터에서 Livy Spark 사용</span><span class="sxs-lookup"><span data-stu-id="aaf45-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="aaf45-165">기본적으로 3.5 HDInsight 클러스터는 로컬 파일 경로 tooaccess 샘플 데이터 파일이 나 jar 사용을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="aaf45-166">사용자는 좋습니다 toouse hello `wasb://` 경로 대신 tooaccess jar 예제 데이터 파일 또는 hello 클러스터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="aaf45-167">Toouse 로컬 경로 사용 하지 않으려면 hello Ambari 구성을 적절 하 게 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="aaf45-168">toodo 하므로:</span><span class="sxs-lookup"><span data-stu-id="aaf45-168">toodo so:</span></span>

1. <span data-ttu-id="aaf45-169">Hello 클러스터에 대 한 toohello Ambari 포털을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="aaf45-170">hello Ambari 웹 UI는 https://에서 HDInsight 클러스터에서 사용할 수 있는**CLUSTERNAME**. 여기서 CLUSTERNAME는 클러스터의 이름을 hello azurehdidnsight.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="aaf45-171">왼쪽 탐색 hello에서 클릭 **리비**, 클릭 하 고 **Configs**합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="aaf45-172">아래 **리비 기본** hello 속성 이름을 추가 `livy.file.local-dir-whitelist` 너무 그 값을 설정 하 고**"/"** tooallow 대 한 모든 권한을 toofile 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="aaf45-173">특정 디렉터리에만 tooa tooallow 액세스 하려는 경우 hello 경로 toothat 디렉터리 hello 값으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="aaf45-174">Azure Virtual Network 내에서 클러스터에 대한 Livy 작업 제출</span><span class="sxs-lookup"><span data-stu-id="aaf45-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="aaf45-175">Tooan Azure 가상 네트워크 내에서 HDInsight Spark 클러스터를 연결 하면 tooLivy hello 클러스터에 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="aaf45-176">이러한 경우 URL 리비 끝점은 hello `http://<IP address of hello headnode>:8998/batches`합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="aaf45-177">여기에서 **8998** 리비 hello 클러스터 헤드 노드에에서 실행 되는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="aaf45-178">비공용 포트의 서비스 액세스에 대한 자세한 내용은 [HDInsight의 Hadoop 서비스에서 사용하는 포트](hdinsight-hadoop-port-settings-for-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aaf45-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="aaf45-179">문제 해결</span><span class="sxs-lookup"><span data-stu-id="aaf45-179">Troubleshooting</span></span>

<span data-ttu-id="aaf45-180">다음은 원격 작업 제출 tooSpark 클러스터에 대 한 리비를 사용 하는 동안에 실행 될 수 있는 몇 가지 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="aaf45-181">외부 jar hello 추가 저장소를 사용 하 여 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="aaf45-182">**문제:** 리비 Spark 작업을 참조 하는 외부 jar hello 클러스터와 연결 된 hello 추가 저장소 계정에서 hello 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="aaf45-183">**해결 방법:** 해당 hello jar 원하는 toouse hello HDInsight 클러스터와 연결 된 hello 기본 저장소에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="aaf45-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aaf45-184">Next step</span></span>

* [<span data-ttu-id="aaf45-185">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf45-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="aaf45-186">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="aaf45-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

