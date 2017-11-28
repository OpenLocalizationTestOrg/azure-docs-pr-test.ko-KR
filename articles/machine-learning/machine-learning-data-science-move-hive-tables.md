---
title: "aaaCreate 하이브 테이블 및 Azure Blob 저장소에서 데이터를 로드 합니다. | Microsoft Docs"
description: "Hive 테이블을 만들고 blob toohive 테이블의 데이터를 로드 합니다."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="0c280-103">Hive 테이블을 만들고 Azure Blob Storage에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="0c280-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="0c280-104">이 토픽에서는 Hive 테이블을 만들고 Azure blob 저장소의 데이터를 로드하는 일반 Hive 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="0c280-105">Hello에 최적화 된 행 열 형식 (ORC) 서식 tooimprove 쿼리 성능을 사용 하 여 및 Hive 테이블 분할에 지침이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="0c280-106">이 **메뉴** tootopics hello 데이터 저장 끌어다 하는 동안 처리할 수 있는 대상 환경으로 데이터 tooingest 팀 데이터 과학 프로세스 (TDSP) hello 하는 방법을 설명 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="0c280-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0c280-107">Prerequisites</span></span>
<span data-ttu-id="0c280-108">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-108">This article assumes that you have:</span></span>

* <span data-ttu-id="0c280-109">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-109">Created an Azure storage account.</span></span> <span data-ttu-id="0c280-110">지침이 필요한 경우 [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c280-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="0c280-111">Hello HDInsight 서비스를 사용 하 여 사용자 지정 된 Hadoop 클러스터 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="0c280-112">지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c280-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="0c280-113">사용 가능한 원격 액세스 toohello 클러스터 로그인 하 고 hello Hadoop 명령줄 콘솔을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="0c280-114">지침이 필요한 경우 참조 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="0c280-115">데이터 tooAzure blob 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="0c280-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="0c280-116">에 제공 된 hello 지침에 따라 Azure 가상 컴퓨터를 만든 경우 [고급 분석을 위해 Azure 가상 컴퓨터를 설정](machine-learning-data-science-setup-virtual-machine.md),이 스크립트 파일 되 었어야 다운로드 한 toohello *c:\\ 사용자가\\\<사용자 이름\>\\문서\\데이터 과학 스크립트* hello 가상 컴퓨터에 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="0c280-117">이러한 하이브 쿼리 데이터 스키마 및 hello 적절 한 필드 toobe 제출할 준비가에서 Azure blob 저장소 구성을 플러그 인만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="0c280-118">라고 가정 Hive 테이블에 대 한 hello 데이터에는 **압축 되지 않은** 테이블 형식 및 hello 데이터 되었음을 업로드 toohello 기본 (또는 추가 tooan) hello Hadoop 클러스터에서 사용 하는 hello 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="0c280-119">Hello에 toopractice 하려는 경우 **NYC 택시 여행 데이터**, 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="0c280-120">**다운로드** hello 24 [NYC 택시 여행 데이터](http://www.andresmh.com/nyctaxitrips) 파일 (12 개의 여행 파일 및 12 개의 요금 파일)</span><span class="sxs-lookup"><span data-stu-id="0c280-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="0c280-121">**압축을 풉니다** .</span><span class="sxs-lookup"><span data-stu-id="0c280-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="0c280-122">**업로드** 해당 toohello 기본 적절 한 컨테이너의 또는 hello hello에 설명 된 hello 프로시저에 의해 생성 된 Azure 저장소 계정 [고급 분석 프로세스 및 기술에 대 한 사용자 지정 Azure HDInsight Hadoop 클러스터 ](machine-learning-data-science-customize-hadoop-cluster.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="0c280-123">hello 프로세스 tooupload hello.csv 파일 toohello 기본 hello 저장소 계정에 있을 수 있습니다이 [페이지](machine-learning-data-science-process-hive-walkthrough.md#upload)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="0c280-124"><a name="submit"></a>어떻게 toosubmit 하이브 쿼리</span><span class="sxs-lookup"><span data-stu-id="0c280-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="0c280-125">다음을 사용하여 Hive 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="0c280-126">Hadoop 클러스터 헤드 노드의 Hadoop 명령줄을 통해 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="0c280-127">Hello 하이브 편집기로 하이브 쿼리를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="0c280-128">Azure PowerShell 명령을 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="0c280-129">Hive 쿼리는 SQL과 유사하므로,</span><span class="sxs-lookup"><span data-stu-id="0c280-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="0c280-130">SQL에 익숙한 경우 사용할 수 있습니다 hello [SQL 사용자 치트 시트에 대 한 하이브](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="0c280-131">하이브 쿼리를 전송할 때 hello 화면 또는 tooa 로컬 파일에 hello 헤드 노드 또는 Azure blob tooan에서 든 관계 없이 하이브 쿼리에서 hello 출력의 hello 대상을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="0c280-132"><a name="headnode"></a> 1. Hadoop 클러스터 헤드 노드의 Hadoop 명령줄을 통해 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="0c280-133">Hello 하이브 쿼리가 복잡 한 하이브 편집기 또는 Azure PowerShell 스크립트를 제출 하는 것 보다 toofaster 반환 일반적으로 인해 hello Hadoop 클러스터의 헤드 노드 hello에서 직접 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="0c280-134">Hello Hadoop 클러스터의 헤드 노드 toohello 로그인 hello Hadoop 명령줄 hello 헤드 노드의 hello 데스크톱에서 열고 명령을 입력 `cd %hive_home%\bin`합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="0c280-135">세 가지 방법으로 toosubmit 하이브 쿼리 hello Hadoop 명령줄 있습니다:</span><span class="sxs-lookup"><span data-stu-id="0c280-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="0c280-136">직접 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-136">directly</span></span>
* <span data-ttu-id="0c280-137">.hql 파일을 사용하여 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-137">using .hql files</span></span>
* <span data-ttu-id="0c280-138">hello로 하이브 명령 콘솔</span><span class="sxs-lookup"><span data-stu-id="0c280-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="0c280-139">Hadoop 명령줄에서 직접 Hive 쿼리를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="0c280-140">다음과 같은 명령을 실행할 수 있습니다 `hive -e "<your hive query>;` toosubmit 간단한 하이브 쿼리에서 직접에서 Hadoop 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="0c280-141">예를 들어 여기서 hello 빨간색 상자 윤곽선 hello 명령 hello 하이브 쿼리를 전송 하 고 hello 하이브 쿼리에서 녹색 상자 윤곽선 hello 출력 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="0c280-143">.hql 파일로 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="0c280-144">Hello 하이브 쿼리는 더 복잡 하 고 여러 줄에, 하이브 명령 콘솔 또는 명령줄에서 쿼리 편집은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="0c280-145">대신은 hello Hadoop 클러스터 toosave hello에서에서 하이브 쿼리에 hello 헤드 노드의 로컬 디렉터리에 있는.hql 파일의 헤드 노드 hello toouse 텍스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="0c280-146">Hello를 사용 하 여 hello.hql 파일에 hello 하이브 쿼리를 제출할 수 있습니다 다음 `-f` 다음과 같이 인수:</span><span class="sxs-lookup"><span data-stu-id="0c280-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="0c280-148">**Hive 쿼리의 진행 상태 화면 인쇄 숨기기**</span><span class="sxs-lookup"><span data-stu-id="0c280-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="0c280-149">기본적으로 Command Line Hadoop에서 하이브 쿼리 제출 hello Map/Reduce 작업의 진행률 hello에 인쇄 됩니다 화면.</span><span class="sxs-lookup"><span data-stu-id="0c280-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="0c280-150">toosuppress hello hello Map/Reduce 작업 진행률의 인쇄 화면, 인수를 사용할 수 있습니다 `-S` (대문자로 "S")의 hello 명령 줄 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="0c280-151">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-151">.</span></span>    <span data-ttu-id="0c280-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="0c280-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="0c280-153">Hive 명령 콘솔에서 Hive 쿼리를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="0c280-154">명령을 실행 하 여 먼저 hello 하이브 명령 콘솔을 입력할 수 있습니다 `hive` Hadoop 명령 줄에서 한 다음 하이브 명령 콘솔에서 하이브 쿼리를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="0c280-155">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-155">Here is an example.</span></span> <span data-ttu-id="0c280-156">이 예제에서는 hello 두 빨간 상자 강조 hello 사용 되는 명령 tooenter 하이브 명령 콘솔 hello 및 hello 각각 하이브 명령 콘솔에서 제출 하는 하이브 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="0c280-157">hello 녹색 상자 hello 하이브 쿼리에서 hello 출력 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-157">hello green box highlights hello output from hello Hive query.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="0c280-159">hello 앞의 예제는 hello 하이브 쿼리 결과 화면에 직접 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="0c280-160">Hello 출력 tooa hello 헤드 노드 또는 Azure blob tooan에 로컬 파일을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="0c280-161">그런 다음 다른 도구를 사용할 수 있습니다 toofurther 하이브 쿼리 hello 출력을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="0c280-162">**하이브 쿼리 결과 tooa 로컬 파일을 출력 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0c280-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="0c280-163">toooutput 하이브 쿼리 결과 tooa 로컬 디렉터리에 hello 헤드 노드를 해야 toosubmit hello 하이브 쿼리 hello Hadoop 명령줄에서에서 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="0c280-164">다음 예제는 hello, Hive 쿼리의 hello 출력 파일에 작성 된 `hivequeryoutput.txt` 디렉터리에 `C:\apps\temp`합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="0c280-166">**하이브 쿼리 결과 tooan Azure blob를 출력 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0c280-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="0c280-167">Hello 하이브 쿼리 결과 tooan hello Hadoop 클러스터의 hello 기본 컨테이너 내에서 Azure blob를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="0c280-168">이 대 한 hello 하이브 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="0c280-169">다음 예제는 hello, Hive 쿼리의 hello 출력 tooa blob 디렉터리 작성 된 `queryoutputdir` hello Hadoop 클러스터의 hello 기본 컨테이너 내에서.</span><span class="sxs-lookup"><span data-stu-id="0c280-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="0c280-170">여기에서는 tooprovide hello 디렉터리 이름이 hello blob 이름 없이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="0c280-171">`wasb:///queryoutputdir/queryoutput.txt`처럼 디렉터리 이름과 blob 이름을 모두 입력하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="0c280-173">Azure 저장소 탐색기를 사용 하 여 hello Hadoop 클러스터의 hello 기본 컨테이너를 열면 hello 다음 그림에에서 표시 된 대로 hello 하이브 쿼리의 hello 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="0c280-174">Hello (빨간색 상자 강조 표시) 필터 tooonly 검색 hello 사용 하 여 blob 이름 다음에 지정 된 문자를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="0c280-176"><a name="hive-editor"></a> 2. Hello 하이브 편집기로 하이브 쿼리를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="0c280-177">Hello 양식의 URL을 입력 하 여 hello 쿼리 콘솔 (하이브 편집기)를 사용할 수도 있습니다 *https://&#60; Hadoop 클러스터 이름 >.azurehdinsight.net/Home/HiveEditor* 웹 브라우저에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="0c280-178">있어야이 콘솔 hello 참조에 로그인 하 고 여기에 Hadoop 클러스터 자격 따라서 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="0c280-179"><a name="ps"></a> 3. Azure PowerShell 명령을 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="0c280-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="0c280-180">또한 PowerShell toosubmit 하이브 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="0c280-181">자세한 내용은 [PowerShell을 사용하여 Hive 작업 제출](../hdinsight/hdinsight-hadoop-use-hive-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c280-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="0c280-182"><a name="create-tables"></a>Hive 데이터베이스 및 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="0c280-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="0c280-183">hello 하이브 쿼리 공유 hello [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) 여기에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="0c280-184">하이브 테이블을 만드는 hello 하이브 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="0c280-185">tooplug 해야 하는 hello 필드 및 기타 구성 hello 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="0c280-186">**&#60; 데이터베이스 이름 >**: toocreate hello 데이터베이스의 이름을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="0c280-187">Toouse hello 기본 데이터베이스를 원하는 경우 hello 쿼리 *데이터베이스를 만드는 중...*  생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="0c280-188">**&#60; 테이블 이름 >**: hello 이름 hello 지정 된 데이터베이스 내에서 toocreate hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="0c280-189">Toouse hello 기본 데이터베이스를 원하는 경우 hello 테이블 참조 될 수 있습니다 직접 *&#60; 테이블 이름 >* 없이 &#60; 데이터베이스 이름 >.</span><span class="sxs-lookup"><span data-stu-id="0c280-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="0c280-190">**&#60; 필드 구분 >**: hello 데이터 파일 toobe의 필드를 구분 하는 hello 구분 기호 toohello Hive 테이블을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="0c280-191">**&#60; 선 구분 기호가 >**: hello 데이터 파일에 있는 줄을 구분 하는 hello 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="0c280-192">**&#60; 저장소 위치 >**: hello Azure 저장소 위치 toosave hello 하이브 테이블의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="0c280-193">지정 하지 않으면 *위치 &#60; 저장소 위치 >*, 데이터베이스 hello 및 hello 테이블에 저장 됩니다 *hive/웨어하우스/* 디렉터리에서 기본적으로 hello 하이브 클러스터의 hello 기본 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="0c280-194">Toospecify hello 저장소 위치를 원하는 경우 hello 저장소 위치 toobe hello 데이터베이스 및 테이블에 대 한 hello 기본 컨테이너 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="0c280-195">이 위치에 hello 형태로 표시의 hello 클러스터의 위치 상대 toohello 기본 컨테이너 라고 toobe *' wasb: / / / &#60; 1 디렉터리 > /'* 또는 *' wasb: / / / &#60; 1 디렉터리 > / &#60; 2 디렉터리 > /'*등입니다. Hello 쿼리를 실행 한 후에 hello 기본 컨테이너에서 hello 상대 디렉터리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="0c280-196">**TBLPROPERTIES("skip.header.line.count"="1")**: hello 데이터 파일에 헤더 줄을 있으면 tooadd이이 속성 **hello 끝** 의 hello *테이블을 만들* 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="0c280-197">그렇지 않으면 hello 헤더 줄은 레코드 toohello 테이블로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="0c280-198">Hello 데이터 파일에 헤더 줄이 없는 경우이 구성은 hello 쿼리에서 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="0c280-199"><a name="load-data"></a>데이터 tooHive 테이블 로드</span><span class="sxs-lookup"><span data-stu-id="0c280-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="0c280-200">Hive 테이블에 데이터를 로드 하는 hello 하이브 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="0c280-201">**&#60; 경로 tooblob 데이터 >**: hello blob 파일 업로드 toobe toohello Hive 테이블 hello HDInsight Hadoop 클러스터의 hello 기본 컨테이너 이면 hello *&#60; 경로 tooblob 데이터 >* hello 형식 이어야 합니다 *' wasb: / / / &#60;이 컨테이너에 디렉터리 > / &#60; blob 파일 이름 >'*합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="0c280-202">또한 hello HDInsight Hadoop 클러스터의 추가 컨테이너에서 hello blob 파일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="0c280-203">이 경우 *&#60; 경로 tooblob 데이터 >* hello 형식은 *' wasb: / / &#60; 컨테이너 이름 > @&#60; 저장소 계정 이름 >.blob.core.windows.net/ &#60; blob 파일 이름 >'*.</span><span class="sxs-lookup"><span data-stu-id="0c280-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0c280-204">hello blob 데이터 업로드 toobe tooHive 테이블에 toobe hello 기본 또는 hello Hadoop 클러스터에 대 한 hello 저장소 계정의 컨테이너를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="0c280-205">그렇지 않으면 hello *데이터 로드* hello 데이터를 액세스할 수 없다고 메시지가 쿼리가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="0c280-206"><a name="partition-orc"></a>고급 토픽: 분할된 테이블 및 ORC 형식으로 Hive 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="0c280-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="0c280-207">Hello 데이터가 클 경우 hello 테이블 분할은 tooscan hello 테이블의 몇 가지 파티션을 하기만 하는 쿼리에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="0c280-208">예를 들어, 날짜별으로 웹 사이트의 적절 한 toopartition hello 로그 데이터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="0c280-209">또한 toopartitioning에서 하이브 테이블, hello에 최적화 된 행 열 형식 (ORC) 형식에 유용한 toostore hello 하이브 데이터 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="0c280-210">ORC 형식에 대한 자세한 내용은 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">ORC 파일을 사용하면 Hive에서 데이터를 읽고, 쓰고, 처리할 때 성능 향상</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c280-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="0c280-211">분할된 테이블</span><span class="sxs-lookup"><span data-stu-id="0c280-211">Partitioned table</span></span>
<span data-ttu-id="0c280-212">분할된 된 테이블을 만들고 데이터를 로드 하는 hello 하이브 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="0c280-213">분할 된 테이블을 쿼리할 때 것이 좋습니다 hello에 tooadd hello 파티션 조건을 **시작** hello의 `where` 절이 크게 검색의 hello 효율성을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="0c280-214"><a name="orc"></a>ORC 형식으로 Hive 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="0c280-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="0c280-215">직접 hello ORC 형식에 저장 된 Hive 테이블에 blob 저장소에서 데이터를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="0c280-216">다음은 hello 단계 tootake tooload 데이터 Azure에서 유지 해야 하는 hello blob tooHive 테이블 ORC 형식으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="0c280-217">외부 테이블 만들기 **AS 텍스트 파일 저장** 및 blob 저장소 toohello 테이블에서 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="0c280-218">내부 테이블을 만듭니다 hello로 필드를 구분 기호가 동일 하 고 저장 하는 hello로 1 단계에서 hello 외부 테이블과 같은 스키마 hello 하이브 데이터 hello ORC 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="0c280-219">1 단계에서 hello 외부 테이블에서 데이터를 선택 하 고 hello ORC 테이블에 삽입</span><span class="sxs-lookup"><span data-stu-id="0c280-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="0c280-220">경우 hello 텍스트 파일 테이블 *&#60; 데이터베이스 이름 >. &#60; 텍스트 파일 외부 테이블 이름 >* 에 파티션이 3 단계에서에서 hello `SELECT * FROM <database name>.<external textfile table name>` 선택 hello에 필드가 데이터 집합을 반환 하는 대로 파티션 변수 hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="0c280-221">Hello에 삽입 *&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >* 이후 실패 *&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >* hello 파티션 변수로 없는 hello 테이블 스키마의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="0c280-222">Toospecifically 선택 hello 필드 toobe 너무 삽입이 경우 해야*&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >* 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="0c280-223">안전 toodrop hello *&#60; 텍스트 파일 외부 테이블 이름 >* 경우 모든 데이터 후 다음 쿼리는 hello를 사용 하 여 삽입 한 *&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >*:</span><span class="sxs-lookup"><span data-stu-id="0c280-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="0c280-224">이 절차를 수행 후 hello ORC 형식 준비 toouse에 데이터가 있는 테이블을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c280-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
