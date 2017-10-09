---
title: "Hadoop Pig HDInsight-Azure의에서 남은 부분과 aaaUse | Microsoft Docs"
description: "Azure HDInsight의 Hadoop에 대 한 toouse REST toorun Pig 라틴 작업 클러스터 되는 방법을 알아봅니다."
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
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="ca596-103">REST를 사용하여 HDInsight에서 Hadoop과 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="ca596-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="ca596-104">Pig 라틴 toorun REST 요청 tooan Azure HDInsight 클러스터를 늘려 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="ca596-105">Curl에 사용 되는 toodemonstrate hello WebHCat REST API를 사용 하 여 HDInsight의 상호 작용 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="ca596-106">Linux 기반 Hadoop 서버를 사용 하 여 사용 하 던 해도 새 tooHDInsight는 경우 참조 [Linux 기반 HDInsight 팁](hdinsight-hadoop-linux-information.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="ca596-107"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="ca596-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ca596-108">Azure HDInsight(HDInsight의 Hadoop) 클러스터(Linux 기반 또는 Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="ca596-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ca596-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ca596-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca596-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="ca596-111">Curl</span><span class="sxs-lookup"><span data-stu-id="ca596-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="ca596-112">jq</span><span class="sxs-lookup"><span data-stu-id="ca596-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="ca596-113"><a id="curl"></a>Curl을 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="ca596-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="ca596-114">hello REST API는을 통해 보안 [기본 액세스 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="ca596-115">항상 보안 HTTP (HTTPS) tooensure 사용자 자격 증명을 안전 하 게 보냄을 toohello 서버를 사용 하 여 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="ca596-116">이 섹션의 hello 명령을 사용 하는 경우 대체 `USERNAME` 을 바꾸고 hello 사용자 tooauthenticate toohello 클러스터 `PASSWORD` hello hello 사용자 계정의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="ca596-117">대체 `CLUSTERNAME` 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="ca596-118">명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="ca596-119">Hello 다음 JSON 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="ca596-120">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="ca596-121">**-u**: hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청</span><span class="sxs-lookup"><span data-stu-id="ca596-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="ca596-122">**-G**: 이 요청이 GET 요청임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="ca596-123">hello URL의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="ca596-124">hello 경로 **/status**, hello 서버에 대 한 해당 hello 요청은 WebHCat (Templeton이 라고도 함)의 tooreturn hello 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="ca596-125">다음 코드 toosubmit Pig 라틴 작업 toohello 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="ca596-126">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="ca596-127">**-d**: 때문에 `-G` 을 사용 하지 않으면 hello 요청 toohello POST 메서드를 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="ca596-128">`-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="ca596-129">**user.name**: hello 명령을 실행 하는 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="ca596-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="ca596-130">**실행**: Pig 라틴 문을 tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="ca596-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="ca596-131">**statusdir**:이 작업에 대 한 상태 hello hello 디렉터리에 쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca596-132">Pig 라틴 문에서 hello 공간 hello로 대체 됩니다 `+` Curl 함께 사용 하는 경우 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="ca596-133">이 명령을 사용 하는 toocheck hello 상태 hello 작업의 예를 들어 일 수 있는 작업 ID를 반환 해야:</span><span class="sxs-lookup"><span data-stu-id="ca596-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="ca596-134">다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태</span><span class="sxs-lookup"><span data-stu-id="ca596-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="ca596-135">대체 `JOBID` hello 이전 단계에서 반환 된 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="ca596-136">예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, 다음 `JOBID` 은 `job_1415651640909_0026`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="ca596-137">Hello 작업이 완료 되 면 hello 상태는 **SUCCEEDED**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca596-138">JavaScript 개체 Object Notation (JSON) hello 작업과 jq에 대 한 정보를 사용 하 여 문서 반환은 사용 되는 tooretrieve이 Curl 요청 상태 값을만 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="ca596-139"><a id="results"></a>결과 보기</span><span class="sxs-lookup"><span data-stu-id="ca596-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="ca596-140">Hello 작업의 상태 hello 너무 변경 될 때**SUCCEEDED**, hello 작업의 hello 결과 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="ca596-141">hello `statusdir` hello 출력 파일의;이 경우 hello 위치를 포함 하는 hello 쿼리와 함께 전달 된 매개 변수 `/example/pigcurl`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="ca596-142">HDInsight은 hello 기본 데이터 저장소로 Azure 저장소 서비스 또는 Azure 데이터 레이크 저장소 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="ca596-143">사용 하는 어떤 것에 따라 hello 데이터에는 다양 한 방법으로 tooget이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="ca596-144">자세한 내용은 hello의 hello 저장소 섹션을 참조 하십시오. [Linux 기반 HDInsight 정보](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) 문서.</span><span class="sxs-lookup"><span data-stu-id="ca596-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="ca596-145"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="ca596-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="ca596-146">이 문서에서 볼 수 있듯이, HDInsight 클러스터에 원시 HTTP 요청 toorun, 모니터 및 보기 hello 결과 Pig 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="ca596-147">이 문서에서 사용 하는 hello REST 인터페이스에 대 한 자세한 내용은 참조 hello [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca596-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="ca596-148"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca596-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ca596-149">HDInsight의 Pig에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="ca596-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="ca596-150">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="ca596-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="ca596-151">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="ca596-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ca596-152">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="ca596-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ca596-153">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="ca596-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
