---
title: "Azure HDInsight에 Curl와 Hadoop Sqoop aaaUse | Microsoft Docs"
description: "Tooremotely Sqoop 작업 tooHDInsight Curl을 사용 하 여 전송 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="11734-103">Curl을 사용하여 HDInsight에서 Hadoop으로 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="11734-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="11734-104">HDInsight에서 Hadoop에 대 한 toouse Curl toorun Sqoop 작업 클러스터링 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11734-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="11734-105">Curl 수의 상호 작용 HDInsight 원시 HTTP 요청 toorun, 모니터 및 hello 결과 Sqoop 작업의 검색을 사용 하 여 사용 되는 toodemonstrate입니다.</span><span class="sxs-lookup"><span data-stu-id="11734-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="11734-106">WebHCat REST API (이전의 Templeton) HDInsight 클러스터에 제공한 hello를 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="11734-107">Linux 기반 Hadoop 서버를 사용 하 여 사용 하 던 해도 새 tooHDInsight는 경우 참조 [Linux에서 HDInsight를 사용 하는 방법은](hdinsight-hadoop-linux-information.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="11734-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="11734-108">Prerequisites</span></span>
<span data-ttu-id="11734-109">이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="11734-110">HDInsight 클러스터에서 Hadoop(Linux 또는 Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="11734-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="11734-111">Curl</span><span class="sxs-lookup"><span data-stu-id="11734-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="11734-112">jq</span><span class="sxs-lookup"><span data-stu-id="11734-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="11734-113">Curl을 사용하여 Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="11734-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="11734-114">Curl 또는 기타 REST 통신와 함께 사용할 경우 WebHCat hello 사용자 이름 및 관리자에 게 HDInsight 클러스터에 대 한 암호를 제공 하 여 hello 요청을 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="11734-115">또한 hello 클러스터 이름을 사용 하 여 hello 식별자 URI (Uniform Resource)의 일부 toosend hello 요청 toohello 서버를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="11734-116">이 섹션의 hello 명령에 대 한 대체 **USERNAME** 을 바꾸고 hello 사용자 tooauthenticate toohello 클러스터 **암호** hello hello 사용자 계정의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="11734-117">대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="11734-118">hello REST API는을 통해 보안 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="11734-119">항상 보안 HTTP (HTTPS) toohelp 보내지도록 자격 증명은 안전 하 게 toohello 서버를 사용 하 여 요청을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="11734-120">명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="11734-121">응답 비슷한 toohello 다음을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11734-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="11734-122">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11734-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="11734-123">**-u** -hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="11734-124">**-G** - GET 요청임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="11734-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="11734-125">hello URL의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11734-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="11734-126">hello 경로 **/status**, hello 서버에 대 한 해당 hello 요청은 tooreturn WebHCat (Templeton이 라고도 함)의 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="11734-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="11734-127">Toosubmit sqoop 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="11734-128">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11734-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="11734-129">**-d** -이후 `-G` 을 사용 하지 않으면 hello 요청 toohello POST 메서드를 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="11734-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="11734-130">`-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="11734-131">**user.name** -hello 명령을 실행 하는 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="11734-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="11734-132">**명령** -Sqoop 명령 tooexecute hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="11734-133">**statusdir** -이 작업에 대 한 상태 hello hello 디렉터리에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11734-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="11734-134">이 명령은 hello 작업의 사용된 toocheck hello 상태가 될 수 있는 작업 ID를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="11734-135">다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="11734-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="11734-136">대체 **JOBID** hello 이전 단계에서 반환 된 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="11734-137">예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, 다음 **JOBID** 것 `job_1415651640909_0026`합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="11734-138">Hello 상태가 됩니다 hello 작업을 마친 경우 **SUCCEEDED**합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="11734-139">이 Curl 요청 hello 작업;에 대 한 정보로 개체 JSON (JavaScript Notation) 문서를 반환합니다. jq 사용 되는 tooretrieve 상태 값을 hello만 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="11734-140">Hello 작업의 hello 상태가 너무 변경 되 면**SUCCEEDED**, Azure Blob 저장소에서 hello 작업의 hello 결과 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11734-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="11734-141">hello `statusdir` hello 출력 파일의;이 경우 hello 위치를 포함 하는 hello 쿼리와 함께 전달 된 매개 변수 **wasb: / / / 예제/curl**합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="11734-142">이 주소 hello에 hello 작업의 출력 hello 저장 **예제/curl** 디렉터리 HDInsight 클러스터에서 사용 하는 hello 기본 저장소 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11734-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="11734-143">나열 하 고 hello를 사용 하 여 이러한 파일을 다운로드할 수 [Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="11734-144">예를 들어 toolist 파일에 **예제/curl**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="11734-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="11734-145">파일을 toodownload hello 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="11734-146">Hello hello를 사용 하 여 hello blob이 포함 된 저장소 계정 이름 지정 `-a` 및 `-k` 매개 변수 또는 집합 hello **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_액세스\_키** 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="11734-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="11734-147">자세한 내용은 <a href="hdinsight-upload-data.md" target="_blank"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11734-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="11734-148">제한 사항</span><span class="sxs-lookup"><span data-stu-id="11734-148">Limitations</span></span>
* <span data-ttu-id="11734-149">대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11734-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="11734-150">일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 삽입을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="11734-151">요약</span><span class="sxs-lookup"><span data-stu-id="11734-151">Summary</span></span>
<span data-ttu-id="11734-152">이 문서에서 볼 수 있듯이, HDInsight 클러스터에 원시 HTTP 요청 toorun, 모니터 및 보기 hello 결과 Sqoop 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11734-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="11734-153">이 문서에서 사용 하는 hello REST 인터페이스에 대 한 자세한 내용은 참조 hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API 가이드</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="11734-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11734-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11734-154">Next steps</span></span>
<span data-ttu-id="11734-155">HDInsight Hive에 대한 일반적인 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="11734-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="11734-156">HDInsight에서 Hadoop과 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="11734-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="11734-157">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="11734-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="11734-158">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="11734-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="11734-159">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="11734-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="11734-160">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="11734-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


