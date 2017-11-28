---
title: "HDInsight에서 REST와 Hadoop Pig 사용 - Azure | Microsoft Docs"
description: "Azure HDInsight의 Hadoop 클러스터에서 REST를 사용하여 Pig Latin 작업을 실행하는 방법에 대해 배웁니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="f8472-103">REST를 사용하여 HDInsight에서 Hadoop과 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f8472-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="f8472-104">Azure HDInsight 클러스터에 대한 REST 요청을 만들어 Pig Latin 작업을 실행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="f8472-105">Curl은 WebHCat REST API를 사용하여 HDInsight와 상호 작용하는 방법을 보여 주는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="f8472-106">이미 익숙한 Linux 기반 Hadoop 서버를 사용하지만 HDInsight는 처음인 경우 [Linux 기반 HDInsight 팁](hdinsight-hadoop-linux-information.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8472-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="f8472-107"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="f8472-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="f8472-108">Azure HDInsight(HDInsight의 Hadoop) 클러스터(Linux 기반 또는 Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="f8472-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f8472-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f8472-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8472-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="f8472-111">Curl</span><span class="sxs-lookup"><span data-stu-id="f8472-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="f8472-112">jq</span><span class="sxs-lookup"><span data-stu-id="f8472-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="f8472-113"><a id="curl"></a>Curl을 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f8472-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="f8472-114">REST API는 [기본 액세스 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)을 통해 보안이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="f8472-115">자격 증명이 안전하게 서버에 전송되도록 하려면 항상 Secure HTTP(HTTPS)를 사용하여 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="f8472-116">이 섹션에서 명령을 사용하는 경우 `USERNAME`은 클러스터에 대해 인증할 사용자로 바꾸고 `PASSWORD`는 사용자 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="f8472-117">`CLUSTERNAME`을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="f8472-118">명령줄에서 다음 명령을 사용하여 HDInsight 클러스터에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="f8472-119">다음 JSON 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="f8472-120">이 명령에서 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="f8472-121">**-u**: 요청을 인증하는 데 사용되는 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="f8472-122">**-G**: 이 요청이 GET 요청임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="f8472-123">URL 시작 부분인 **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**은 모든 요청에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="f8472-124">**/status** 경로는 요청이 서버에 대한 WebHCat(Templeton라고도 함)의 상태를 반환하는 경우 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="f8472-125">다음 코드를 사용하여 클러스터에 Pig Latin 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="f8472-126">이 명령에서 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="f8472-127">**-d**: `-G`가 사용되지 않으므로 요청은 POST 메서드로 기본 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="f8472-128">`-d` 는 요청과 함께 전송되는 데이터 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="f8472-129">**user.name**: 명령을 실행하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="f8472-130">**execute**: 실행할 Pig Latin 문입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="f8472-131">**statusdir**: 이 작업의 상태를 기록할 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="f8472-132">Curl과 함께 사용할 경우 Pig Latin 문의 공백이 `+` 문자로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="f8472-133">이 명령은 작업 상태를 확인하는데 사용할 수 있는 작업 ID를 반환해야 합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="f8472-134">작업 상태를 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="f8472-135">`JOBID`를 이전 단계에서 반환된 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="f8472-136">예를 들어 반환 값이 `{"id":"job_1415651640909_0026"}`인 경우 `JOBID`는 `job_1415651640909_0026`입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="f8472-137">작업이 완료된 경우 상태는 **SUCCEEDED**입니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f8472-138">이 Curl 요청은 작업에 관한 정보가 있는 JSON(JavaScript Object Notation) 문서를 반환합니다. jq는 상태 값을 검색하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="f8472-139"><a id="results"></a>결과 보기</span><span class="sxs-lookup"><span data-stu-id="f8472-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="f8472-140">작업 상태가 **SUCCEEDED**로 변경되면 작업 결과를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="f8472-141">쿼리와 함께 전달된 `statusdir` 매개 변수에는 출력 파일의 위치(이 경우 `/example/pigcurl`)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="f8472-142">HDInsight는 Azure Storage 또는 Azure Data Lake Store를 기본 데이터 저장소로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="f8472-143">여러 가지 방법으로 사용하는 것에 따라 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="f8472-144">자세한 내용은 [Linux 기반 HDInsight 정보](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) 문서의 저장소 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8472-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="f8472-145"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="f8472-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="f8472-146">이 문서에 설명된 대로 원시 HTTP 요청을 사용하여 HDInsight 클러스터에서 Pig 작업을 실행하고 모니터링하며 그 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8472-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="f8472-147">이 문서에 사용된 REST 인터페이스에 대한 자세한 내용은 [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8472-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="f8472-148"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8472-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f8472-149">HDInsight의 Pig에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="f8472-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="f8472-150">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="f8472-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="f8472-151">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="f8472-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f8472-152">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="f8472-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f8472-153">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="f8472-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
