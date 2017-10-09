---
title: "MapReduce aaaUse 및 Azure HDInsight에서 Hadoop으로 Curl | Microsoft Docs"
description: "어떻게 tooremotely MapReduce 작업으로 실행 Hadoop HDInsight에 Curl을 사용 하 여에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="ebc55-103">REST를 사용하여 HDInsight에서 Hadoop으로 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="ebc55-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="ebc55-104">HDInsight 클러스터에서 Hadoop에서 toouse hello WebHCat REST API toorun MapReduce 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="ebc55-105">Curl 수의 상호 작용 HDInsight 원시 HTTP 요청 toorun MapReduce 작업을 사용 하 여 사용 되는 toodemonstrate입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="ebc55-106">Linux 기반 Hadoop 서버를 사용 하 여 이미 익숙한 새 tooHDInsight는 표시 되지만 참조 hello [필요한 HDInsight의 Linux 기반 Hadoop에 대 한 tooknow](hdinsight-hadoop-linux-information.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ebc55-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="ebc55-107"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="ebc55-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ebc55-108">HDInsight 클러스터의 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ebc55-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="ebc55-109">Curl</span><span class="sxs-lookup"><span data-stu-id="ebc55-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="ebc55-110">jq</span><span class="sxs-lookup"><span data-stu-id="ebc55-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="ebc55-111"><a id="curl"></a>Curl을 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="ebc55-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="ebc55-112">WebHCat와 Curl 또는 기타 REST 통신을 사용할 경우 hello HDInsight 클러스터 관리자 사용자 이름 및 암호를 제공 하 여 hello 요청을 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="ebc55-113">URI 사용 하는 toosend hello 요청 toohello 서버 hello의 일환으로 hello 클러스터 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="ebc55-114">이 섹션의 hello 명령에 대 한 대체 **USERNAME** hello 사용자 tooauthenticate toohello 클러스터와 및 **암호** hello hello 사용자 계정의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="ebc55-115">대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="ebc55-116">hello REST API가 사용 하 여 보안 [기본 액세스 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="ebc55-117">항상 HTTPS tooensure 사용자 자격 증명을 안전 하 게 보냄을 toohello 서버를 사용 하 여 요청을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="ebc55-118">명령줄에서 명령 tooverify tooyour HDInsight 클러스터를 연결할 수 있는지에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="ebc55-119">다음 JSON 응답 비슷한 toohello을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="ebc55-120">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="ebc55-121">**-u**: hello 사용자 이름 및 암호 사용 tooauthenticate hello 요청을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="ebc55-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="ebc55-122">**-G**: 이 작업이 GET 요청임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="ebc55-123">hello URI의 시작 hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, 모든 요청에 대해 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="ebc55-124">MapReduce 작업 toosubmit hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="ebc55-125">hello (/ mapreduce/jar) URI의 hello 끝이이 요청 jar 파일의 클래스에서 MapReduce 작업을 시작 됨 WebHCat을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="ebc55-126">이 명령에 사용 되는 hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="ebc55-127">**-d**: `-G` 은 사용 되지 않으므로 hello 요청 toohello POST 메서드를 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="ebc55-128">`-d`hello 요청과 함께 전송 되는 hello 데이터 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="ebc55-129">**user.name**: hello 명령을 실행 하는 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="ebc55-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="ebc55-130">**jar**: hello 위치 toobe 클래스를 포함 하는 hello jar 파일의 실행</span><span class="sxs-lookup"><span data-stu-id="ebc55-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="ebc55-131">**클래스**: hello hello MapReduce 논리를 포함 하는 클래스</span><span class="sxs-lookup"><span data-stu-id="ebc55-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="ebc55-132">**arg**: hello 인수 toobe toohello MapReduce 작업을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="ebc55-133">이 경우 hello 입력 hello 출력에 사용 되는 텍스트 파일과 hello 디렉터리</span><span class="sxs-lookup"><span data-stu-id="ebc55-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="ebc55-134">이 명령은 hello 작업의 사용된 toocheck hello 상태가 될 수 있는 작업 ID를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="ebc55-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="ebc55-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="ebc55-136">다음 명령을 사용 하 여 hello, hello 작업의 toocheck hello 상태:</span><span class="sxs-lookup"><span data-stu-id="ebc55-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="ebc55-137">Hello 대체 **JOBID** hello 이전 단계에서 반환 된 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="ebc55-138">예를 들어 hello 반환 값이 `{"id":"job_1415651640909_0026"}`, JOBID 것 hello 다음 `job_1415651640909_0026`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="ebc55-139">Hello 작업이 완료 되 면 hello 상태는 반환 `SUCCEEDED`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ebc55-140">이 Curl 요청 hello 작업에 대 한 정보가 포함 된 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="ebc55-141">Jq 사용 되는 tooretrieve 상태 값을 hello만 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="ebc55-142">Hello 작업의 상태 hello 너무 변경 될 때`SUCCEEDED`, Azure Blob 저장소에서 hello 작업의 hello 결과 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="ebc55-143">hello `statusdir` hello 쿼리와 함께 전달 되는 매개 변수는 hello 출력 파일의 hello 위치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="ebc55-144">이 예제에서는 hello 위치가 `/example/curl`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="ebc55-145">이 주소는 hello 작업의 출력 hello hello 클러스터 기본 저장소 위치에 저장 `/example/curl`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="ebc55-146">나열 하 고 hello를 사용 하 여 이러한 파일을 다운로드할 수 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="ebc55-147">Hello Azure CLI에서에서 blob 사용한 작업에 대 한 자세한 내용은 참조 hello [hello를 사용 하 여 Azure 저장소와 Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs) 문서.</span><span class="sxs-lookup"><span data-stu-id="ebc55-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="ebc55-148"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="ebc55-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ebc55-149">HDInsight의 MapReduce 작업에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="ebc55-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="ebc55-150">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="ebc55-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ebc55-151">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="ebc55-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ebc55-152">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="ebc55-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ebc55-153">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="ebc55-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="ebc55-154">이 문서에서 사용 되는 REST 인터페이스를 hello에 대 한 자세한 내용은 참조 hello [WebHCat 참조](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc55-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
