---
title: "Hive 테이블을 만들고 Azure Blob Storage에서 데이터 로드 | Microsoft Docs"
description: "Hive 테이블을 만들어서 blob의 데이터를 Hive 테이블에 로드"
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
ms.openlocfilehash: eca4ecd8f639bb9816903f4b1d1f999755da819c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="1323b-103">Hive 테이블을 만들고 Azure Blob Storage에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="1323b-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="1323b-104">이 토픽에서는 Hive 테이블을 만들고 Azure blob 저장소의 데이터를 로드하는 일반 Hive 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="1323b-105">또한 Hive 테이블을 분할하고 ORC(Optimized Row Columnar) 형식을 사용하여 쿼리 성능을 개선하는 방법에 대한 지침도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="1323b-106">이 **메뉴** 는 TDSP(팀 데이터 과학 프로세스) 중 데이터를 저장하고 처리할 수 있는 대상 환경에 데이터를 수집하는 방법을 설명하는 토픽에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="1323b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1323b-107">Prerequisites</span></span>
<span data-ttu-id="1323b-108">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-108">This article assumes that you have:</span></span>

* <span data-ttu-id="1323b-109">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-109">Created an Azure storage account.</span></span> <span data-ttu-id="1323b-110">지침이 필요한 경우 [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1323b-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="1323b-111">사용자 지정된 Hadoop 클러스터에 HDInsight 서비스를 프로비전했습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="1323b-112">지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1323b-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="1323b-113">클러스터에 대한 원격 액세스를 설정하고, 로그인하고, Hadoop 명령줄 콘솔을 열었습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="1323b-114">지침이 필요한 경우 [Hadoop 클러스터의 헤드 노드에 액세스](machine-learning-data-science-customize-hadoop-cluster.md#headnode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1323b-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="1323b-115">Azure Blob 저장소에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="1323b-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="1323b-116">[고급 분석을 위한 Azure 가상 컴퓨터 설정](machine-learning-data-science-setup-virtual-machine.md)의 지침에 따라 Azure 가상 컴퓨터를 만드는 경우 이 스크립트 파일을 가상 컴퓨터의 *C:\\Users\\\<사용자 이름\>\\Documents\\Data Science Scripts* 디렉터리에 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="1323b-117">이러한 Hive 쿼리는 제출이 가능하도록 적절한 필드에서 사용자 데이터 스키마 및 Azure blob 저장소 구성을 연결하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="1323b-118">Hive 테이블의 데이터가 **압축되지 않은** 테이블 형식이고 Hadoop 클러스터에서 사용하는 저장소 계정의 기본 또는 추가 컨테이너에 데이터가 업로드된 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="1323b-119">**NYC Taxi Trip Data**로 연습하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="1323b-120">**NYC Taxi Trip Data** 파일(12개의 Trip 파일과 12개의 Fare 파일)을 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="1323b-121">**압축을 풉니다** .</span><span class="sxs-lookup"><span data-stu-id="1323b-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="1323b-122">**고급 분석 프로세스 및 기술을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정** 항목에 설명된 절차에 따라 생성된 기본(또는 해당 컨테이너) 위치로 [업로드](machine-learning-data-science-customize-hadoop-cluster.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="1323b-123">저장소 계정의 기본 컨테이너에 .csv 파일을 업로드하는 프로세스는 이 [페이지](machine-learning-data-science-process-hive-walkthrough.md#upload)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="1323b-124"><a name="submit"></a>Hive 쿼리를 제출하는 방법</span><span class="sxs-lookup"><span data-stu-id="1323b-124"><a name="submit"></a>How to submit Hive queries</span></span>
<span data-ttu-id="1323b-125">다음을 사용하여 Hive 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="1323b-126">Hadoop 클러스터 헤드 노드의 Hadoop 명령줄을 통해 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="1323b-127">Hive 편집기를 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="1323b-128">Azure PowerShell 명령을 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="1323b-129">Hive 쿼리는 SQL과 유사하므로,</span><span class="sxs-lookup"><span data-stu-id="1323b-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="1323b-130">SQL에 익숙한 사용자에게는 [SQL 사용자용 Hive 치트 시트](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf)가 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="1323b-131">또한 Hive 쿼리를 제출할 때 Hive 쿼리에서 화면, 헤드 노드의 로컬 파일, Azure blob 등의 출력 대상을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <span data-ttu-id="1323b-132"><a name="headnode"></a> 1. Hadoop 클러스터 헤드 노드의 Hadoop 명령줄을 통해 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="1323b-133">Hive 쿼리가 복잡한 경우 Hadoop 클러스터의 헤드 노드에서 바로 Hive 쿼리를 제출하면 일반적으로 Hive 편집기 또는 Azure PowerShell 스크립트를 사용하여 제출하는 것보다 반환 시간이 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="1323b-134">Hadoop 클러스터의 헤드 노드에 로그인하고, 헤드 노드 바탕 화면에서 Hadoop 명령줄을 열고, 명령을 입력합니다 `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="1323b-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="1323b-135">세 가지 방법으로 Hadoop 명령줄에서 Hive 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="1323b-136">직접 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-136">directly</span></span>
* <span data-ttu-id="1323b-137">.hql 파일을 사용하여 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-137">using .hql files</span></span>
* <span data-ttu-id="1323b-138">Hive 명령 콘솔을 사용하여 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="1323b-139">Hadoop 명령줄에서 직접 Hive 쿼리를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="1323b-140">`hive -e "<your hive query>;` 같은 명령을 실행하여 Hadoop 명령줄에서 바로 간단한 Hive 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="1323b-141">다음은 그 예제입니다. 빨간색 상자는 Hive 쿼리를 제출하는 명령을, 녹색 상자는 Hive 쿼리의 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="1323b-143">.hql 파일로 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="1323b-144">Hive 쿼리가 좀 더 복잡하고 줄이 여러 개인 경우 명령줄 또는 Hive 명령 콘솔에서 쿼리를 편집하는 방법은 실용적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="1323b-145">대신 Hadoop 클러스터의 헤드 노드에서 텍스트 편집기를 사용하여 헤드 노드의 로컬 디렉터리에 있는 .hql 파일에 Hive 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="1323b-146">그러면 다음과 같이 `-f` 인수를 사용하여 .hql 파일의 Hive 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="1323b-148">**Hive 쿼리의 진행 상태 화면 인쇄 숨기기**</span><span class="sxs-lookup"><span data-stu-id="1323b-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="1323b-149">기본적으로 Hadoop 명령줄에서 Hive 쿼리가 제출되면 맵/감소 작업의 진행 상태가 화면에 인쇄됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="1323b-150">맵/감소 작업의 진행 상태 화면 인쇄를 숨기려면 다음과 같이 명령줄에 `-S` 인수("S"는 대문자)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
<span data-ttu-id="1323b-151">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-151">.</span></span>    <span data-ttu-id="1323b-152">hive -S -e "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="1323b-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="1323b-153">Hive 명령 콘솔에서 Hive 쿼리를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="1323b-154">또한 Hadoop 명령줄에서 `hive` 명령을 실행하여 Hive 명령 콘솔을 먼저 입력한 후 Hive 명령 콘솔에서 Hive 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-154">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="1323b-155">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-155">Here is an example.</span></span> <span data-ttu-id="1323b-156">이 예제에서 두 빨간색 상자는 각각 Hive 명령 콘솔을 입력하는 데 사용된 명령과 Hive 명령 콘솔에서 제출된 Hive 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-156">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="1323b-157">녹색 상자는 Hive 쿼리의 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-157">The green box highlights the output from the Hive query.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="1323b-159">이전 예제에서는 Hive 쿼리 결과가 화면에 바로 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-159">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="1323b-160">또한 헤드 로드의 로컬 파일 또는 Azure blob에 출력을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-160">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="1323b-161">그런 다음 다른 도구를 사용하여 Hive 쿼리 출력을 추가로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-161">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="1323b-162">**Hive 쿼리 결과를 로컬 파일에 출력합니다.**</span><span class="sxs-lookup"><span data-stu-id="1323b-162">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="1323b-163">Hive 쿼리 결과를 헤드 노드의 로컬 디렉터리에 출력하려면 다음과 같이 Hadoop 명령줄에서 Hive 쿼리를 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-163">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="1323b-164">다음 예제에서 Hive 쿼리의 출력은 `C:\apps\temp` 디렉터리의 `hivequeryoutput.txt` 파일에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-164">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="1323b-166">**Azure blob에 Hive 쿼리 결과 출력**</span><span class="sxs-lookup"><span data-stu-id="1323b-166">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="1323b-167">Hadoop 클러스터의 기본 컨테이너 내에 있는 Azure blob에 Hive 쿼리 결과를 출력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-167">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="1323b-168">이 경우 관련 Hive 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-168">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="1323b-169">다음 예제에서 Hive 쿼리는 Hadoop 클러스터의 기본 컨테이너 내에 있는 blob 디렉터리 `queryoutputdir` 에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-169">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="1323b-170">이때 사용자는 blob 이름 없이 디렉터리 이름만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-170">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="1323b-171">`wasb:///queryoutputdir/queryoutput.txt`처럼 디렉터리 이름과 blob 이름을 모두 입력하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="1323b-173">Azure 저장소 탐색기를 사용하여 Hadoop 클러스터의 기본 컨테이너를 열면 다음과 같은 Hive 쿼리 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-173">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="1323b-174">필터(빨간색 상자로 강조 표시됨)를 적용하여 이름에 지정된 문자가 포함된 blob만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-174">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="1323b-176"><a name="hive-editor"></a> 2. Hive 편집기를 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-176"><a name="hive-editor"></a> 2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="1323b-177">양식의 URL *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor*를 웹 브라우저에 입력하여 쿼리 콘솔(Hive 편집기)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-177">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="1323b-178">이 콘솔을 보려면 로그인해야 하며, Hadoop 클러스터 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-178">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="1323b-179"><a name="ps"></a> 3. Azure PowerShell 명령을 사용하여 Hive 쿼리 제출</span><span class="sxs-lookup"><span data-stu-id="1323b-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="1323b-180">PowerShell을 사용하여 Hive 쿼리를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-180">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="1323b-181">자세한 내용은 [PowerShell을 사용하여 Hive 작업 제출](../hdinsight/hdinsight-hadoop-use-hive-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1323b-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="1323b-182"><a name="create-tables"></a>Hive 데이터베이스 및 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1323b-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="1323b-183">Hive 쿼리는 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql)에서 공유되며 여기에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-183">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="1323b-184">다음은 Hive 테이블을 만드는 Hive 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-184">Here is the Hive query that creates a Hive table.</span></span>

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

<span data-ttu-id="1323b-185">다음은 연결해야 하는 필드와 기타 구성에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-185">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="1323b-186">**&#60;database name>**: 만들려고 하는 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-186">**&#60;database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="1323b-187">기본 데이터베이스를 사용하려는 경우 *create database...* 쿼리를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-187">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="1323b-188">**&#60;table name>**: 지정된 데이터베이스 내에 만들려는 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-188">**&#60;table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="1323b-189">기본 데이터베이스를 사용하려는 경우 &#60;database name> 없이 *&#60;table name>*을 통해 직접 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-189">If you want to use the default database, the table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="1323b-190">**&#60;field separator>**: 데이터 파일에서 Hive 테이블에 업로드할 필드를 구분하는 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-190">**&#60;field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="1323b-191">**&#60;line separator>**: 데이터 파일의 줄을 구분하는 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-191">**&#60;line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="1323b-192">**&#60;storage location>**: Hive 테이블의 데이터를 저장할 Azure Storage 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-192">**&#60;storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="1323b-193">*LOCATION &#60;storage location>*을 지정하지 않으면 기본적으로 데이터베이스 및 테이블이 Hive 클러스터의 기본 컨테이너에 있는 *hive/warehouse/* 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-193">If you do not specify *LOCATION &#60;storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="1323b-194">저장소 위치를 지정하려면 저장소 위치가 데이터베이스 및 테이블의 기본 컨테이너 내부에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-194">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="1323b-195">이 위치는 *'wasb:///&#60;directory 1>/'* 또는 *'wasb:///&#60;directory 1>/&#60;directory 2>/'* 등의 형식으로 클러스터 기본 컨테이너에 대한 상대 위치로 참조해야 합니다. 쿼리가 실행된 후 기본 컨테이너 내에 상대 디렉터리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-195">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="1323b-196">**TBLPROPERTIES("skip.header.line.count"="1")**: 데이터 파일에 헤더 줄이 있으면 *create table* 쿼리의 **끝**에 이 속성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="1323b-197">그렇지 않으면 헤더 줄이 테이블의 레코드로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-197">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="1323b-198">데이터 파일에 헤더 줄이 없으면 쿼리에서 이 구성을 생략해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-198">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <span data-ttu-id="1323b-199"><a name="load-data"></a>Hive 테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="1323b-199"><a name="load-data"></a>Load data to Hive tables</span></span>
<span data-ttu-id="1323b-200">다음은 Hive 테이블에 데이터를 로드하는 Hive 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-200">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="1323b-201">**&#60;path to blob data>**: Hive 테이블에 업로드할 Blob 파일이 HDInsight Hadoop 클러스터의 기본 컨테이너에 있으면 *&#60;path to blob data>*가 *'wasb:///&#60;directory in this container>/&#60;blob file name>'* 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-201">**&#60;path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *&#60;path to blob data>* should be in the format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="1323b-202">blob 파일이 HDInsight Hadoop 클러스터의 추가 컨테이너에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-202">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1323b-203">이 경우 *&#60;path to blob data>*는 *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'* 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-203">In this case, *&#60;path to blob data>* should be in the format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1323b-204">Hive 테이블에 업로드할 blob 데이터가 Hadoop 클러스터에 대한 저장소 계정의 기본 또는 추가 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-204">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="1323b-205">그렇지 않으면 데이터에 액세스할 수 없기 때문에 *LOAD DATA* 쿼리가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-205">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <span data-ttu-id="1323b-206"><a name="partition-orc"></a>고급 토픽: 분할된 테이블 및 ORC 형식으로 Hive 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="1323b-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="1323b-207">데이터가 큰 경우 테이블을 분할하면 테이블의 파티션 몇 개만 검색하면 되는 쿼리의 속도가 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-207">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="1323b-208">예를 들어 웹 사이트의 로그 데이터를 날짜별로 분할하는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-208">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="1323b-209">Hive 테이블 분할 외에도 Hive 데이터를 ORC(Optimized Row Columnar) 형식으로 저장하는 방법 또한 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-209">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="1323b-210">ORC 형식에 대한 자세한 내용은 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">ORC 파일을 사용하면 Hive에서 데이터를 읽고, 쓰고, 처리할 때 성능 향상</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1323b-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="1323b-211">분할된 테이블</span><span class="sxs-lookup"><span data-stu-id="1323b-211">Partitioned table</span></span>
<span data-ttu-id="1323b-212">다음은 분할된 테이블을 만들고 그 테이블에 데이터를 로드하는 Hive 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-212">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="1323b-213">분할된 테이블에 쿼리할 때 `where` 절의 **시작 부분**에 파티션 조건을 추가하면 검색 효율성이 크게 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-213">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="1323b-214"><a name="orc"></a>ORC 형식으로 Hive 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="1323b-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="1323b-215">blob 저장소의 데이터를 ORC 형식으로 저장된 Hive 테이블에 바로 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-215">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="1323b-216">Azure blob의 데이터를 ORC 형식으로 저장된 Hive 테이블에 로드하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-216">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="1323b-217">외부 테이블 **STORED AS TEXTFILE** 을 만들고 blob 저장소의 데이터를 이 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

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

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="1323b-218">1단계의 외부 테이블과 동일한 스키마 및 필드 구분 기호를 사용하여 내부 테이블을 만들고 Hive 데이터를 ORC 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-218">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="1323b-219">1단계의 외부 테이블에서 데이터를 선택하여 ORC 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-219">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="1323b-220">TEXTFILE 테이블 *&#60;database name>.&#60;external textfile table name>*에 파티션이 있으면 3단계의 `SELECT * FROM <database name>.<external textfile table name>` 명령에서는 반환된 데이터 집합의 필드로 파티션 변수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-220">If the TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="1323b-221">*&#60;database name>.&#60;ORC table name>*에 삽입은 실패하는데, *&#60;database name>.&#60;ORC table name>*에는 테이블 스키마의 필드로 해당 파티션 변수가 포함되어 있지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-221">Inserting it into the *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="1323b-222">이 경우 *&#60;database name>.&#60;ORC table name>*에 삽입할 필드를 다음과 같이 구체적으로 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-222">In this case, you need to specifically select the fields to be inserted to *&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="1323b-223">모든 데이터가 *&#60;database name>.&#60;ORC table name>*에 삽입된 후에는 다음 쿼리를 사용할 때 *&#60;external textfile table name>*을 삭제하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-223">It is safe to drop the *&#60;external textfile table name>* when using the following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="1323b-224">이 절차를 모두 수행했다면 이제 ORC 형식의 데이터를 사용할 수 있는 테이블이 준비되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1323b-224">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
