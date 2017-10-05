---
title: "HDInsight에서 Curl과 Hadoop Sqoop 사용 - Azure | Microsoft Docs"
description: "원격으로 Curl을 사용하여 HDInsight에 Sqoop 작업을 제출하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="1b69b-103">Curl을 사용하여 HDInsight에서 Hadoop으로 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="1b69b-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="1b69b-104">HDInsight의 Hadoop 클러스터에서 Curl을 사용하여 Sqoop 작업을 실행하는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="1b69b-105">Sqoop 작업을 실행하고 모니터링하며 결과를 검색하는 원시 HTTP 요청을 사용하여 HDInsight와 상호 작용하는 방법을 설명하는 데 Curl을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="1b69b-106">이 Curl은 HDInsight 클러스터에서 제공하는 WebHCat REST API(이전의 Templeton)를 사용하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1b69b-107">이미 익숙한 Linux 기반 Hadoop 서버를 사용하지만 HDInsight는 처음인 경우 [Linux에서 HDInsight 사용에 관한 정보](hdinsight-hadoop-linux-information.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b69b-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1b69b-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1b69b-108">Prerequisites</span></span>
<span data-ttu-id="1b69b-109">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="1b69b-110">HDInsight 클러스터에서 Hadoop(Linux 또는 Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="1b69b-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="1b69b-111">Curl</span><span class="sxs-lookup"><span data-stu-id="1b69b-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="1b69b-112">jq</span><span class="sxs-lookup"><span data-stu-id="1b69b-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="1b69b-113">Curl을 사용하여 Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1b69b-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="1b69b-114">WebHCat에서 Curl 또는 다른 모든 REST 통신을 사용하는 경우 HDInsight 클러스터 관리자의 사용자 이름 및 암호를 제공하여 요청을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="1b69b-115">또한 클러스터 이름을 서버로 요청을 보내는 데 사용되는 URI(Uniform Resource Identifier)의 일부로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="1b69b-116">이 섹션의 명령에서 **USERNAME**은 클러스터에 대해 인증할 사용자로 바꾸고 **PASSWORD**는 사용자 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="1b69b-117">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="1b69b-118">REST API는 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)을 통해 보안됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="1b69b-119">자격 증명이 안전하게 서버에 전송되도록 하려면 항상 보안 HTTP(HTTPS)를 사용하여 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="1b69b-120">명령줄에서 다음 명령을 사용하여 HDInsight 클러스터에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="1b69b-121">그러면 다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="1b69b-122">이 명령에서 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="1b69b-123">**-u** - 요청을 인증하는 데 사용되는 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="1b69b-124">**-G** - GET 요청임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="1b69b-125">URL 시작 부분인 **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**은 모든 요청에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="1b69b-126">**/status** 경로는 요청이 서버에 대한 WebHCat(Templeton라고도 함)의 상태를 반환하는 경우 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="1b69b-127">다음을 사용하여 Sqoop 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="1b69b-128">이 명령에서 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="1b69b-129">**-d** - `-G`가 사용되지 않으므로 요청은 POST 메서드로 기본 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="1b69b-130">`-d` 는 요청과 함께 전송되는 데이터 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="1b69b-131">**user.name** - 명령을 실행하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="1b69b-132">**명령** - 실행할 Sqoop 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="1b69b-133">**statusdir** - 이 작업의 상태를 기록할 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="1b69b-134">이 명령은 작업 상태를 확인하는데 사용할 수 있는 작업 ID를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="1b69b-135">작업 상태를 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="1b69b-136">**JOBID** 를 이전 단계에서 반환된 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="1b69b-137">예를 들어 반환 값이 `{"id":"job_1415651640909_0026"}`인 경우 **JOBID**는 `job_1415651640909_0026`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="1b69b-138">작업이 완료되면 상태는 **SUCCEEDED**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1b69b-139">이 Curl 요청은 작업에 관한 정보가 있는 JSON(JavaScript Object Notation) 문서를 반환합니다. jq는 상태 값을 검색하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="1b69b-140">작업 상태가 **SUCCEEDED**로 변경되면 Azure Blob Storage에서 작업 결과를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="1b69b-141">쿼리와 함께 전달된 `statusdir` 매개 변수에는 출력 파일의 위치(이 경우 **wasb:///example/curl**)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="1b69b-142">이 주소는 HDInsight 클러스터에서 사용하는 기본 저장소 컨테이너의 **example/curl** 디렉터리에 작업의 출력을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="1b69b-143">[Azure CLI](../cli-install-nodejs.md)를 사용하여 이러한 파일을 나열하고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="1b69b-144">예를 들어 **example/curl**에 파일을 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="1b69b-145">파일을 다운로드하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="1b69b-146">`-a` 및 `-k` 매개 변수를 사용하여 Blob을 포함하는 저장소 계정 이름을 지정하거나 **AZURE\_STORAGE\_ACCOUNT** 및 **AZURE\_STORAGE\_ACCESS\_KEY** 환경 변수를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="1b69b-147">자세한 내용은 <a href="hdinsight-upload-data.md" target="_blank"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b69b-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="1b69b-148">제한 사항</span><span class="sxs-lookup"><span data-stu-id="1b69b-148">Limitations</span></span>
* <span data-ttu-id="1b69b-149">대량 내보내기 - Linux 기반 HDInsight와 함께 Microsoft SQL Server 또는 Azure SQL 데이터베이스에 데이터를 내보내는 데 사용된 Sqoop 커넥터도 현재 대량 삽입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="1b69b-150">배치 - Linux 기반 HDInsight와 함께 삽입을 수행할 때 `-batch` 스위치를 사용하는 경우 Sqoop는 삽입 작업을 일괄 처리하는 대신 여러 삽입 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="1b69b-151">요약</span><span class="sxs-lookup"><span data-stu-id="1b69b-151">Summary</span></span>
<span data-ttu-id="1b69b-152">이 문서에서 볼 수 있듯이 원시 HTTP 요청을 사용하여 HDInsight 클러스터의 Sqoop 작업을 실행하고 모니터링하며 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="1b69b-153">이 문서에 사용된 REST 인터페이스에 대한 자세한 내용은 <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API 가이드</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b69b-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b69b-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b69b-154">Next steps</span></span>
<span data-ttu-id="1b69b-155">HDInsight Hive에 대한 일반적인 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="1b69b-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="1b69b-156">HDInsight에서 Hadoop과 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="1b69b-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="1b69b-157">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="1b69b-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1b69b-158">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="1b69b-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1b69b-159">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="1b69b-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1b69b-160">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="1b69b-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


