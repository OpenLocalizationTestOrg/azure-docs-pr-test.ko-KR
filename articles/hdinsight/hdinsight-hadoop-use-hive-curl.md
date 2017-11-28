---
title: "Azure HDInsight에 Curl와 Hadoop 하이브 aaaUse | Microsoft Docs"
description: "Tooremotely 전송 Pig tooHDInsight Curl을 사용 하 여 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="08143-103">REST를 사용하여 HDInsight에서 Hadoop으로 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="08143-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="08143-104">Azure HDInsight 클러스터에서 하이브 toouse hello WebHCat REST API toorun Hadoop으로 쿼리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="08143-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="08143-105">[Curl](http://curl.haxx.se/) 수의 상호 작용 HDInsight 원시 HTTP 요청을 사용 하 여 사용 되는 toodemonstrate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="08143-106">hello [jq](http://stedolan.github.io/jq/) 유틸리티는 REST 요청에서 반환 된 사용 되는 tooprocess hello JSON 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="08143-107">Linux 기반 Hadoop 서버를 사용 하 여 사용 하 던 해도 새 tooHDInsight는 경우 참조 hello [필요한 Linux 기반 HDInsight의 Hadoop에 대 한 tooknow](hdinsight-hadoop-linux-information.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="08143-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="08143-108"><a id="curl"></a>Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="08143-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="08143-109">CURL 또는 기타 REST 통신와 함께 사용할 경우 WebHCat hello 사용자 이름 및 관리자에 게 HDInsight 클러스터에 대 한 암호를 제공 하 여 hello 요청을 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="08143-110">이 섹션의 hello 명령에 대 한 대체 **USERNAME** 을 바꾸고 hello 사용자 tooauthenticate toohello 클러스터 **암호** hello hello 사용자 계정의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="08143-111">대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="08143-112">hello REST API는을 통해 보안 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="08143-113">toohelp 고 자격 증명이 안전 하 게 확인 보안 HTTP (HTTPS)을 사용 하 여 전송 된 toohello 서버 항상 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="08143-114">명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="08143-115">텍스트 다음 응답 비슷한 toohello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="08143-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="08143-116">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="08143-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="08143-117">**-u** -hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="08143-118">**-G** - 이 요청이 GET 작업임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="08143-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="08143-119">hello URL의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="08143-120">hello 경로 **/status**, hello 서버에 대 한 해당 hello 요청은 tooreturn WebHCat (Templeton이 라고도 함)의 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="08143-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="08143-121">Hello 다음 명령을 사용 하 여 하이브 hello 버전을 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08143-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="08143-122">이 요청에는 텍스트 다음 응답 비슷한 toohello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="08143-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="08143-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="08143-124">Toocreate 라는 테이블을 다음 사용 하 여 hello **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="08143-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="08143-125">이 요청과 함께 사용 되는 매개 변수 뒤 hello:</span><span class="sxs-lookup"><span data-stu-id="08143-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="08143-126">**-d** -이후 `-G` 을 사용 하지 않으면 hello 요청 toohello POST 메서드를 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="08143-127">`-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="08143-128">**user.name** -hello 명령을 실행 하는 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="08143-129">**실행** -HiveQL 문은 tooexecute hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="08143-130">**statusdir** -이 작업에 대 한 상태 hello hello 디렉터리에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="08143-131">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="08143-132">**DROP TABLE** -hello 테이블이 이미 있으면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="08143-133">**CREATE EXTERNAL TABLE** - Hive에서 새 ‘외부’ 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08143-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="08143-134">외부 테이블 하이브에 hello 테이블 정의 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="08143-135">hello 데이터는 hello 원래 위치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08143-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="08143-136">외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="08143-137">예를 들어 자동화된 데이터 업로드 프로세스 또는 다른 MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08143-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="08143-138">외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="08143-139">**행 형식** hello 데이터의 서식을 지정 하는 방법-합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="08143-140">각 로그에 hello 필드는 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="08143-141">**AS 텍스트 파일 저장 위치** -hello 데이터가 저장 되는 경우 (hello 예제/데이터 디렉터리) 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="08143-142">**선택** -모든 행의 개수를 선택 합니다. 여기서 열 **t4** hello 값이 포함 된 **[오류]**합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="08143-143">이 값이 포함된 행이 3개이므로 이 문은 **3** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="08143-144">Hello HiveQL 문은 사이 공백이 hello로 대체 됩니다 `+` Curl 함께 사용 하는 경우 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="08143-145">Hello 구분 기호 같이 공백을 포함 하는 따옴표로 묶인된 값으로 대체 되어야 하지 `+`합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="08143-146">**'%25.log'와 같은 INPUT__FILE__NAME** -이 문의 제한 hello 검색 tooonly 사용으로 끝나는 파일. 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="08143-147">hello `%25` hello URL로 인코딩된 형식의 %, 하는 hello 실제 상태 이므로 `like '%.log'`합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="08143-148">hello %의 toobe URL로 인코딩된, Url의 특수 문자로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08143-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="08143-149">이 명령은 hello 작업의 사용된 toocheck hello 상태가 될 수 있는 작업 ID를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="08143-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="08143-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="08143-151">다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태:</span><span class="sxs-lookup"><span data-stu-id="08143-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="08143-152">대체 **JOBID** hello 이전 단계에서 반환 된 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="08143-153">예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, 다음 **JOBID** 것 `job_1415651640909_0026`합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="08143-154">Hello 작업이 완료 되 면 hello 상태는 **SUCCEEDED**합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="08143-155">이 Curl 요청 hello 작업에 대 한 정보로 개체 JSON (JavaScript Notation) 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="08143-156">Jq 사용 되는 tooretrieve 상태 값을 hello만 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="08143-157">Hello 작업의 hello 상태가 너무 변경 되 면**SUCCEEDED**, Azure Blob 저장소에서 hello 작업의 hello 결과 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08143-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="08143-158">hello `statusdir` hello 출력 파일의;이 경우 hello 위치를 포함 하는 hello 쿼리와 함께 전달 된 매개 변수 **/예제/curl**합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="08143-159">이 주소 hello에 hello 출력 저장 **예제/curl** hello에 대 한 디렉터리는 기본 저장소를 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="08143-160">나열 하 고 hello를 사용 하 여 이러한 파일을 다운로드할 수 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="08143-161">Hello Azure CLI를 사용 하 여 Azure 저장소에 대 한 자세한 내용은 참조 hello [Azure 저장소와 Azure CLI 2.0 사용](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) 문서.</span><span class="sxs-lookup"><span data-stu-id="08143-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="08143-162">다음 문은 toocreate 라는 새 'internal' 테이블이 사용 하 여 hello **살펴볼**:</span><span class="sxs-lookup"><span data-stu-id="08143-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="08143-163">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="08143-164">**CREATE TABLE IF NOT EXISTS** - 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08143-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="08143-165">이 문은 hello 하이브 데이터 웨어하우스에 저장 된 Hive에서 완전히 관리 되 고 있는 한 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08143-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="08143-166">외부 테이블의 경우와 달리 hello 기본 데이터도 삭제 내부 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="08143-167">**AS ORC 저장** -hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="08143-168">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="08143-169">**덮어쓰기 삽입... 선택** -hello에서 행을 선택 **log4jLogs** 이 있는 테이블 **[오류]**, 삽입 hello에 데이터를 hello 다음 **살펴볼** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="08143-170">**선택** -새 hello에서 모든 행을 선택 **살펴볼** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="08143-171">Hello 작업의 toocheck hello 상태를 반환 하는 hello 작업 ID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="08143-172">처리가 성공 하면 일단 hello hello 결과 toodownload 및 보기 앞에서 설명한 대로 Azure CLI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="08143-173">hello 출력 모두 포함 하는 세 줄을 포함 해야 **[오류]**합니다.</span><span class="sxs-lookup"><span data-stu-id="08143-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="08143-174"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="08143-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="08143-175">HDInsight Hive에 대한 일반적인 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="08143-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="08143-176">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="08143-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="08143-177">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="08143-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="08143-178">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="08143-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="08143-179">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="08143-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="08143-180">Tez 하이브가 있는 사용 하는 경우 hello 다음 디버깅 정보에 대 한 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="08143-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="08143-181">Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="08143-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="08143-182">이 문서에 사용 된 REST API hello에 대 한 자세한 내용은 참조 hello [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) 문서.</span><span class="sxs-lookup"><span data-stu-id="08143-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


