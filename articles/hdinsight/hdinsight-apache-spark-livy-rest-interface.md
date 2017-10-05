---
title: "Azure HDInsight에서 Livy Spark를 사용하여 Spark 클러스터에 작업 제출 | Microsoft Docs"
description: "Apache Spark REST API를 사용하여 Azure HDInsight 클러스터에 원격으로 Spark 작업을 제출하는 방법을 알아봅니다."
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
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="ea705-104">Apache Spark REST API를 사용하여 HDInsight Spark 클러스터에 원격 작업 제출</span><span class="sxs-lookup"><span data-stu-id="ea705-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="ea705-105">Azure HDInsight Spark 클러스터에 원격 작업을 제출하는 데 사용되는 Livy, Apache Spark REST API를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="ea705-106">자세한 설명서는 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea705-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="ea705-107">Livy를 사용하여 대화형 Spark 셸을 실행하거나 Spark에서 실행되도록 배치 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="ea705-108">이 문서는 Livy를 사용하여 배치 작업을 제출하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="ea705-109">이 문서의 코드 조각은 cURL을 사용하여 Livy Spark 끝점에 대한 REST API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="ea705-110">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="ea705-110">**Prerequisites:**</span></span>

* <span data-ttu-id="ea705-111">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ea705-112">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea705-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="ea705-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="ea705-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="ea705-114">이 문서에서는 cURL을 사용하여 HDInsight Spark 클러스터에 대해 REST API 호출을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="ea705-115">Livy Spark 배치 작업 제출</span><span class="sxs-lookup"><span data-stu-id="ea705-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="ea705-116">배치 작업을 제출하기 전에 클러스터와 연결된 클러스터 저장소에 응용 프로그램 jar을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="ea705-117">[**AzCopy**](../storage/common/storage-use-azcopy.md) 명령줄 유틸리티를 사용하면 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="ea705-118">데이터를 업로드하는 데 사용할 수 있는 다른 클라이언트도 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="ea705-119">[HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="ea705-120">**예제**:</span><span class="sxs-lookup"><span data-stu-id="ea705-120">**Examples**:</span></span>

* <span data-ttu-id="ea705-121">jar 파일이 클러스터 저장소(WASB)에 있는 경우</span><span class="sxs-lookup"><span data-stu-id="ea705-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="ea705-122">입력 파일의 일부분으로 jar 파일 이름 및 클래스 이름을 전달하려는 경우(이 예제에서는 input.txt)</span><span class="sxs-lookup"><span data-stu-id="ea705-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="ea705-123">클러스터에서 실행 중인 Livy Spark 배치에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="ea705-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="ea705-124">**예제**:</span><span class="sxs-lookup"><span data-stu-id="ea705-124">**Examples**:</span></span>

* <span data-ttu-id="ea705-125">클러스터에서 실행 중인 모든 Livy Spark 배치를 검색하려는 경우:</span><span class="sxs-lookup"><span data-stu-id="ea705-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="ea705-126">지정된 batchId로 특정 배치를 검색하려는 경우</span><span class="sxs-lookup"><span data-stu-id="ea705-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="ea705-127">Livy Spark 배치 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="ea705-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="ea705-128">**예제**:</span><span class="sxs-lookup"><span data-stu-id="ea705-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="ea705-129">Livy Spark 및 고가용성</span><span class="sxs-lookup"><span data-stu-id="ea705-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="ea705-130">Livy는 클러스터에서 실행 중인 Spark 작업에 대해 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="ea705-131">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="ea705-132">Spark 클러스터에 원격으로 작업을 제출한 후에 Livy 서비스가 다운되면 작업은 백그라운드에서 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="ea705-133">Livy는 백업된 후 작업의 상태를 복원하고 다시 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="ea705-134">HDInsight용 Jupyter 노트북은 백 엔드에서 Livy를 통해 구동됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="ea705-135">노트북에서 Spark 작업이 실행되고 있으며 Livy 서비스가 다시 시작되면 해당 노트북은 코드 셀을 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="ea705-136">예제 보기</span><span class="sxs-lookup"><span data-stu-id="ea705-136">Show me an example</span></span>
<span data-ttu-id="ea705-137">이 섹션에서는 Livy Spark를 사용하여 배치 작업을 제출하고 작업의 진행 상황을 모니터링한 다음 작업을 삭제하기 위한 예제를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="ea705-138">이 예제에서 사용하는 응용 프로그램은 문서 [독립 실행형 Scala 응용 프로그램을 만들고 HDInsight Spark 클러스터에서 실행하기](hdinsight-apache-spark-create-standalone-application.md)에서 개발된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="ea705-139">여기에 나오는 단계는 다음 상태로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-139">The steps here assume that:</span></span>

* <span data-ttu-id="ea705-140">응용 프로그램 jar를 클러스터와 연결된 저장소 계정에 이미 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="ea705-141">이 단계를 시도하려는 컴퓨터에 CuRL을 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="ea705-142">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-142">Perform the following steps:</span></span>

1. <span data-ttu-id="ea705-143">먼저 Livy Spark가 클러스터에서 실행 중인지 확인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="ea705-144">실행 중인 배치 목록을 가져와서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="ea705-145">처음으로 Livy를 사용하여 작업을 실행하는 경우 출력은 0을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="ea705-146">다음 코드 조각과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="ea705-147">출력의 마지막 줄이 실행 중인 배치가 없는 것을 나타내는 **total:0**을 말하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="ea705-148">이제 배치 작업을 제출하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-148">Let us now submit a batch job.</span></span> <span data-ttu-id="ea705-149">다음 코드 조각은 입력 파일(input.txt)을 사용하여 매개 변수로 jar 이름 및 클래스 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="ea705-150">Windows 컴퓨터에서 이러한 단계를 실행하는 경우 입력 파일을 사용하는 것이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="ea705-151">파일 **input.txt** 에서 매개 변수는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="ea705-152">다음 코드 조각과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="ea705-153">출력의 마지막 줄이 **state:starting**을 말하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="ea705-154">또한 **id:0**을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-154">It also says, **id:0**.</span></span> <span data-ttu-id="ea705-155">여기서 **0**은 배치 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="ea705-156">이제 배치 ID를 사용하여 이 특정 배치의 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="ea705-157">다음 코드 조각과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="ea705-158">이제 출력은 작업이 성공적으로 완료됐음을 나타내는 **state:success**를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="ea705-159">원하는 경우 이제 배치를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="ea705-160">다음 코드 조각과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="ea705-161">출력의 마지막 줄은 배치가 성공적으로 삭제된 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="ea705-162">실행 중인 작업을 삭제하면 작업이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="ea705-163">성공적으로 완료됐거나 그렇지 않은 작업을 삭제하는 경우 작업 정보를 완전히 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="ea705-164">HDInsight 3.5 클러스터에서 Livy Spark 사용</span><span class="sxs-lookup"><span data-stu-id="ea705-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="ea705-165">기본적으로 HDInsight 3.5 클러스터는 로컬 파일 경로를 사용하여 샘플 데이터 파일이나 jar를 액세스하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="ea705-166">클러스터에서 jar 또는 샘플 데이터 파일에 액세스하는 대신 `wasb://` 경로를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="ea705-167">로컬 경로를 사용하려면 이에 따라 Ambari 구성을 적절하게 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="ea705-168">이렇게 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-168">To do so:</span></span>

1. <span data-ttu-id="ea705-169">클러스터에 대한 Ambari 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="ea705-170">Ambari 웹 UI는 https://**CLUSTERNAME**.azurehdidnsight.net의 HDInsight 클러스터에서 사용할 수 있습니다. 여기서 CLUSTERNAME은 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="ea705-171">왼쪽의 탐색 창에서 **Livy**를 클릭한 다음 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="ea705-172">**livy-default** 아래에서 `livy.file.local-dir-whitelist` 속성 이름을 추가하고 파일 시스템에 대한 전체 액세스를 허용하려면 값을 **"/"**(슬래시)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="ea705-173">특정 디렉터리에 대한 액세스만 허용하려면 해당 디렉터리에 대한 경로를 값으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="ea705-174">Azure Virtual Network 내에서 클러스터에 대한 Livy 작업 제출</span><span class="sxs-lookup"><span data-stu-id="ea705-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="ea705-175">Azure Virtual Network 내에서 HDInsight Spark 클러스터에 연결하는 경우 클러스터의 Livy에 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="ea705-176">이러한 경우 Livy 끝점의 URL은 `http://<IP address of the headnode>:8998/batches`입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="ea705-177">여기서 **8998**은 클러스터 헤드 노드에서 Livy가 실행되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="ea705-178">비공용 포트의 서비스 액세스에 대한 자세한 내용은 [HDInsight의 Hadoop 서비스에서 사용하는 포트](hdinsight-hadoop-port-settings-for-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea705-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ea705-179">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ea705-179">Troubleshooting</span></span>

<span data-ttu-id="ea705-180">다음에는 Spark 클러스터에 원격 작업 제출을 위해 Livy를 사용하는 동안에 발생할 수 있는 몇 가지 문제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="ea705-181">추가 저장소의 외부 jar 사용이 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="ea705-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="ea705-182">**문제:** Livy Spark 작업이 클러스터에 연결된 추가 저장소 계정의 외부 jar를 참조하는 경우 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="ea705-183">**해결 방법:** 사용하려는 jar가 HDInsight 클러스터와 연결된 기본 저장소에서 사용 가능한 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea705-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="ea705-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea705-184">Next step</span></span>

* [<span data-ttu-id="ea705-185">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="ea705-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ea705-186">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="ea705-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

