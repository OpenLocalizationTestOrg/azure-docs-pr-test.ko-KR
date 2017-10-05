---
title: "HDInsight에서 Curl을 통해 Hadoop Hive 사용 - Azure | Microsoft Docs"
description: "원격으로 Curl을 사용하여 HDInsight에 Pig 작업을 제출하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="7872a-103">REST를 사용하여 HDInsight에서 Hadoop으로 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7872a-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="7872a-104">WebHCat REST API를 사용하여 Azure HDInsight 클러스터에서 Hadoop으로 Hive 쿼리를 실행하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7872a-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="7872a-105">[Curl](http://curl.haxx.se/)은 원시 HTTP 요청을 사용하여 HDInsight와 상호 작용하는 방법을 보여주는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="7872a-106">[jq](http://stedolan.github.io/jq/) 유틸리티는 REST 요청에서 반환된 JSON 데이터를 처리하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="7872a-107">Linux 기반 Hadoop 서버를 익숙하게 사용하지만 HDInsight는 처음인 경우 [HDInsight의 Linux 기반 Hadoop에 대해 알아야 할 정보](hdinsight-hadoop-linux-information.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7872a-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="7872a-108"><a id="curl"></a>Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7872a-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="7872a-109">WebHCat에서 cURL 또는 다른 모든 REST 통신을 사용하는 경우 HDInsight 클러스터 관리자의 사용자 이름 및 암호를 제공하여 요청을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="7872a-110">이 섹션의 명령에서 **USERNAME**은 클러스터에 대해 인증할 사용자로 바꾸고 **PASSWORD**는 사용자 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="7872a-111">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="7872a-112">REST API는 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)을 통해 보안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="7872a-113">자격 증명이 안전하게 서버에 전송되도록 하려면 항상 Secure HTTP(HTTPS)를 사용하여 요청하십시오.</span><span class="sxs-lookup"><span data-stu-id="7872a-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="7872a-114">명령줄에서 다음 명령을 사용하여 HDInsight 클러스터에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="7872a-115">다음 텍스트와 유사한 응답이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="7872a-116">이 명령에서 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="7872a-117">**-u** - 요청을 인증하는 데 사용되는 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="7872a-118">**-G** - 이 요청이 GET 작업임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="7872a-119">URL 시작 부분인 **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**은 모든 요청에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="7872a-120">**/status** 경로는 요청이 서버에 대한 WebHCat(Templeton라고도 함)의 상태를 반환하는 경우 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="7872a-121">또한 다음 명령을 사용하여 Hive의 버전을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="7872a-122">이 요청은 다음 텍스트와 유사한 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="7872a-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="7872a-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="7872a-124">다음을 사용하여 **log4jLogs**라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="7872a-125">이 요청에는 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="7872a-126">**-d** - `-G`가 사용되지 않으므로 요청은 POST 메서드로 기본 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="7872a-127">`-d` 는 요청과 함께 전송되는 데이터 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="7872a-128">**user.name** - 명령을 실행하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="7872a-129">**execute** - 실행할 HiveQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="7872a-130">**statusdir** - 이 작업의 상태를 기록할 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="7872a-131">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="7872a-132">**DROP TABLE** - 이미 테이블이 있으면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="7872a-133">**CREATE EXTERNAL TABLE** - Hive에서 새 ‘외부’ 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="7872a-134">외부 테이블은 테이블 정의만 Hive에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="7872a-135">데이터는 원래 위치에 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7872a-136">외부 원본에서 기본 데이터를 업데이트하길 원하는 경우에는 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="7872a-137">예를 들어 자동화된 데이터 업로드 프로세스 또는 다른 MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="7872a-138">외부 테이블을 삭제하면 데이터는 삭제되지 **않고** 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="7872a-139">**ROW FORMAT** - 데이터의 형식을 지정하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="7872a-140">각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="7872a-141">**STORED AS TEXTFILE LOCATION** - 데이터가 저장되는 위치(example/data 디렉터리). 이 데이터는 텍스트로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="7872a-142">**SELECT** - **t4** 열에 **[ERROR]** 값이 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="7872a-143">이 값이 포함된 행이 3개이므로 이 문은 **3** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7872a-144">Curl과 함께 사용할 경우 HiveQL 문 사이의 공백이 `+` 문자로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="7872a-145">구분 기호와 같이 공백을 포함하는 따옴표로 묶인 값은 `+`로 바뀌지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="7872a-146">**INPUT__FILE__NAME LIKE '%25.log'** - 이 문은 .log로 끝나는 파일만 사용하기 위해 검색을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7872a-147">`%25`는 %의 URL 인코딩 형식이므로 실제 조건은 `like '%.log'`입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="7872a-148">%를 URL로 인코드해야 하므로 URL에서 특수 문자로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="7872a-149">이 명령은 작업 상태를 확인하는데 사용할 수 있는 작업 ID를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="7872a-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="7872a-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="7872a-151">작업 상태를 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="7872a-152">**JOBID** 를 이전 단계에서 반환된 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="7872a-153">예를 들어 반환 값이 `{"id":"job_1415651640909_0026"}`인 경우 **JOBID**는 `job_1415651640909_0026`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="7872a-154">작업이 완료된 경우 상태는 **SUCCEEDED**입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7872a-155">이 Curl 요청은 작업에 관한 정보가 있는 JSON(JavaScript Object Notation) 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="7872a-156">Jq는 상태 값을 검색하는 데에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="7872a-157">작업 상태가 **SUCCEEDED**로 변경되면 Azure Blob Storage에서 작업 결과를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="7872a-158">쿼리와 함께 전달된 `statusdir` 매개 변수에는 출력 파일의 위치(이 경우 **/example/curl**)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="7872a-159">이 주소는 클러스터 기본 저장소의 **example/curl** 디렉터리에 출력을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="7872a-160">[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 사용하여 이러한 파일을 나열하고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="7872a-161">Azure Storage에서 Azure CLI를 사용하는 방법에 대한 자세한 내용은 [Azure Storage에서 Azure CLI 2.0 사용](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7872a-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="7872a-162">다음 문을 사용하여 **errorLogs**라는 새 ‘내부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="7872a-163">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="7872a-164">**CREATE TABLE IF NOT EXISTS** - 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="7872a-165">이 문은 Hive 데이터 웨어하우스에 저장되며 Hive에서 완전히 관리하는 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7872a-166">외부 테이블과 달리 내부 테이블을 삭제하면 기본 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="7872a-167">**STORED AS ORC** - 데이터를 ORC(Optimized Row Columnar) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="7872a-168">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="7872a-169">**덮어쓰기 삽입... SELECT** - **[ERROR]**가 포함된 **log4jLogs** 테이블에서 행을 선택하고 데이터를 **errorLogs** 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="7872a-170">**SELECT** - 새 **errorLogs** 테이블에서 모든 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="7872a-171">작업 상태를 확인하려면 반환된 작업 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="7872a-172">작업이 성공하면 이전에 설명한 대로 Azure CLI를 사용하여 결과를 다운로드하고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="7872a-173">결과는 **[ERROR]**를 포함하여 모두 3줄이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="7872a-174"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="7872a-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7872a-175">HDInsight Hive에 대한 일반적인 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="7872a-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="7872a-176">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="7872a-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="7872a-177">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="7872a-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7872a-178">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="7872a-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7872a-179">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="7872a-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7872a-180">Hive와 함께 Tez를 사용하는 경우 디버깅 정보에 대한 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7872a-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="7872a-181">Linux 기반 HDInsight에서 Ambari Tez 보기 사용</span><span class="sxs-lookup"><span data-stu-id="7872a-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="7872a-182">이 문서에 사용된 REST API에 대한 자세한 내용은 [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7872a-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


