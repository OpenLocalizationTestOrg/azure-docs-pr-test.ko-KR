---
title: "Azure Cosmos DB 및 HDInsight를 사용하여 Hadoop 작업 실행 | Microsoft Docs"
description: "단순 Hive, Pig 및 MapReduce 작업을 Azure Cosmos DB 및 Azure HDInsight에서 실행하는 방법을 알아봅니다."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="85cab-103"><a name="Azure Cosmos DB-HDInsight"></a>Azure Cosmos DB 및 HDInsight를 사용하여 Apache Hive, Pig 또는 Hadoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="85cab-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="85cab-104">이 자습서에서는 Cosmos DB의 Hadoop 커넥터를 사용하여 Azure HDInsight에서 [Apache Hive][apache-hive], [Apache Pig][apache-pig] 및 [Apache Hadoop][apache-hadoop] MapReduce 작업을 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="85cab-105">Cosmos DB의 Hadoop 커넥터를 사용하면 Cosmos DB가 Hive, Pig 및 MapReduce 작업에 대한 원본 및 싱크 둘 다로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="85cab-106">이 자습서에서는 Cosmos DB가 Hadoop 작업에 대한 데이터 원본 및 대상으로 모두 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="85cab-107">이 자습서를 완료하고 나면 다음을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="85cab-108">Hive, Pig 또는 MapReduce 작업을 사용하여 Cosmos DB에서 데이터를 로드하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="85cab-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="85cab-109">Hive, Pig 또는 MapReduce 작업을 사용하여 Cosmos DB에 데이터를 저장하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="85cab-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="85cab-110">먼저 Cosmos DB 및 HDInsight를 사용하여 Hive 작업을 실행하는 다음 동영상을 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="85cab-111">그런 다음 이 자습서로 돌아와서 Cosmos DB 데이터에 대해 분석 작업을 실행하는 방법을 자세히 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="85cab-112">이 자습서에서는 사용자가 이전에 Apache Hadoop, Hive 및/또는 Pig를 사용한 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="85cab-113">Apache Hadoop, Hive 및 Pig를 처음 사용하는 경우 [Apache Hadoop 설명서][apache-hadoop-doc]를 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="85cab-114">또한 이 자습서에서는 이전에 Cosmos DB를 사용한 경험이 있으며 Cosmos DB 계정이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="85cab-115">Cosmos DB를 처음 사용하거나 Cosmos DB 계정이 없는 경우 [시작][getting-started] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="85cab-116">자습서를 완료할 시간이 없고 Hive, Pig 및 MapReduce에 대한 전체 샘플 PowerShell 스크립트를 가져오려는 경우</span><span class="sxs-lookup"><span data-stu-id="85cab-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="85cab-117">[여기][hdinsight-samples]에서 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="85cab-118">이 다운로드에는 또한 해당 샘플에 대한 hql, pig 및 java 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="85cab-119"><a name="NewestVersion"></a>최신 버전</span><span class="sxs-lookup"><span data-stu-id="85cab-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="85cab-120">Hadoop 커넥터 버전</span><span class="sxs-lookup"><span data-stu-id="85cab-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="85cab-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="85cab-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="85cab-122">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="85cab-122">Script Uri</span></span></th>
        <td><span data-ttu-id="85cab-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="85cab-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="85cab-124">수정한 날짜</span><span class="sxs-lookup"><span data-stu-id="85cab-124">Date Modified</span></span></th>
        <td><span data-ttu-id="85cab-125">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="85cab-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="85cab-126">지원되는 HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="85cab-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="85cab-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="85cab-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="85cab-128">변경 로그</span><span class="sxs-lookup"><span data-stu-id="85cab-128">Change Log</span></span></th>
        <td><span data-ttu-id="85cab-129">Azure Cosmos DB Java SDK가 1.6.0으로 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="85cab-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="85cab-130">원본 및 싱크로 분할된 컬렉션에 대한 추가 지원</span><span class="sxs-lookup"><span data-stu-id="85cab-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="85cab-131"><a name="Prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="85cab-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="85cab-132">이 자습서의 지침을 따르기 전에 다음이 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="85cab-133">Cosmos DB 계정, 데이터베이스 및 내부 문서가 포함된 컬렉션.</span><span class="sxs-lookup"><span data-stu-id="85cab-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="85cab-134">자세한 내용은 [Cosmos DB 시작하기][getting-started]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="85cab-135">[Cosmos DB 가져오기 도구][import-data]를 사용하여 Cosmos DB 계정으로 샘플 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="85cab-136">처리량.</span><span class="sxs-lookup"><span data-stu-id="85cab-136">Throughput.</span></span> <span data-ttu-id="85cab-137">HDInsight에서의 읽기 및 쓰기는 해당 컬렉션에 할당된 요청 단위로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="85cab-138">각 출력 컬렉션 내의 추가 저장 프로시저 용량.</span><span class="sxs-lookup"><span data-stu-id="85cab-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="85cab-139">저장 프로시저는 결과 문서를 전송하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="85cab-140">Hive, Pig 또는 MapReduce 작업의 결과 문서 용량.</span><span class="sxs-lookup"><span data-stu-id="85cab-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="85cab-141">[*선택 사항*] 추가 컬렉션의 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="85cab-142">작업 중 새 컬렉션이 생성되지 않도록 하려면 결과를 stdout으로 출력하거나, 출력을 WASB 컨테이너로 출력하거나, 기존 컬렉션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="85cab-143">기존 컬렉션을 지정하는 경우에는 새 문서가 컬렉션 내에 만들어지고 기존 문서는 *id*에서 충돌이 있는 경우에만 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="85cab-144">**커넥터는 id가 충돌하는 기존 문서를 자동으로 덮어씁니다**.</span><span class="sxs-lookup"><span data-stu-id="85cab-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="85cab-145">이 기능은 upsert 옵션을 false로 설정해서 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="85cab-146">upsert가 false이고 충돌이 발생하면 Hadoop 작업이 실패하고 id 충돌 오류가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="85cab-147"><a name="ProvisionHDInsight"></a>1단계: 새 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="85cab-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="85cab-148">이 자습서에서는 Azure Portal의 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="85cab-149">이 자습서에서는 Azure Portal을 사용하여 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="85cab-150">PowerShell cmdlet 또는 HDInsight .NET SDK 사용 방법에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-custom-provision] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="85cab-151">[Azure Portal][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="85cab-152">왼쪽 탐색의 맨 위에 있는 **+ 새로 만들기**를 클릭하고 새 블레이드의 맨 위 검색 표시줄에서 **HDInsight**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="85cab-153">**Microsoft**에서 공개한 **HDInsight**는 결과의 위쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="85cab-154">클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="85cab-155">새 HDInsight 클러스터 만들기 블레이드에서 **클러스터 이름**을 입력하고 이 리소스를 프로비전하려는 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="85cab-156">클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="85cab-156">Cluster name</span></span></td><td><span data-ttu-id="85cab-157">클러스터의 이름</span><span class="sxs-lookup"><span data-stu-id="85cab-157">Name the cluster.</span></span><br/>
<span data-ttu-id="85cab-158">DNS 이름은 영숫자 문자로 시작 및 끝나야 하고 대시를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="85cab-159">이 필드는 3~63자 사이의 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="85cab-160">구독 이름</span><span class="sxs-lookup"><span data-stu-id="85cab-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="85cab-161">둘 이상의 Azure 구독이 있는 경우 HDInsight 클러스터를 호스팅할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="85cab-162">
5. **클러스터 유형 선택**을 클릭하고 다음 속성을 지정된 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="85cab-163">클러스터 유형</span><span class="sxs-lookup"><span data-stu-id="85cab-163">Cluster type</span></span></td><td><span data-ttu-id="85cab-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="85cab-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="85cab-165">클러스터 계층</span><span class="sxs-lookup"><span data-stu-id="85cab-165">Cluster tier</span></span></td><td><span data-ttu-id="85cab-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="85cab-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="85cab-167">운영 체제</span><span class="sxs-lookup"><span data-stu-id="85cab-167">Operating System</span></span></td><td><span data-ttu-id="85cab-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="85cab-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="85cab-169">버전</span><span class="sxs-lookup"><span data-stu-id="85cab-169">Version</span></span></td><td><span data-ttu-id="85cab-170">최신 버전</span><span class="sxs-lookup"><span data-stu-id="85cab-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="85cab-171">이제 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-171">Now, click **SELECT**.</span></span>

    ![Hadoop HDInsight 초기 클러스터 세부 정보 제공][image-customprovision-page1]
6. <span data-ttu-id="85cab-173">**자격 증명** 을 클릭하여 로그인 및 원격 액세스 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="85cab-174">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="85cab-175">클러스터를 원격으로 사용하려는 경우 블레이드 맨 아래에서 *예* 를 선택하고 사용자 이름 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="85cab-176">**데이터 원본** 을 클릭하여 데이터 액세스의 기본 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="85cab-177">**선택 방법** 을 선택하고 기존 저장소 계정을 지정하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="85cab-178">동일한 블레이드에서 **기본 컨테이너** 및 **위치**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="85cab-179">그리고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85cab-180">성능 향상을 위해 Cosmos DB 계정 지역에 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="85cab-181">**가격 책정** 을 클릭하여 노드의 수와 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="85cab-182">기본 구성을 유지하고 나중에 작업자 노드 수를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="85cab-183">선택적 구성 블레이드에서 **옵션 구성** 및 **스크립트 작업**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="85cab-184">스크립트 작업에서 다음 정보를 입력하여 HDInsight 클러스터 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="85cab-185">속성</span><span class="sxs-lookup"><span data-stu-id="85cab-185">Property</span></span></th><th><span data-ttu-id="85cab-186">값</span><span class="sxs-lookup"><span data-stu-id="85cab-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="85cab-187">이름</span><span class="sxs-lookup"><span data-stu-id="85cab-187">Name</span></span></td>
             <td><span data-ttu-id="85cab-188">스크립트 작업의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="85cab-189">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="85cab-189">Script URI</span></span></td>
             <td><span data-ttu-id="85cab-190">클러스터를 사용자 지정하기 위해 호출되는 스크립트에 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="85cab-191">다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-191">Please enter:</span></span> </br> <span data-ttu-id="85cab-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="85cab-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="85cab-193">헤드</span><span class="sxs-lookup"><span data-stu-id="85cab-193">Head</span></span></td>
             <td><span data-ttu-id="85cab-194">이 확인란을 클릭하여 헤드 노드에 대한 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="85cab-195">
             <strong>이 확인란을 선택합니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="85cab-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="85cab-196">작업자</span><span class="sxs-lookup"><span data-stu-id="85cab-196">Worker</span></span></td>
             <td><span data-ttu-id="85cab-197">이 확인란을 클릭하여 작업자 노드에 대한 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="85cab-198">
             <strong>이 확인란을 선택합니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="85cab-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="85cab-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="85cab-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="85cab-200">확인란을 클릭하여 Zookeeper에 대한 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="85cab-201">
             <strong>필요하지 않습니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="85cab-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="85cab-202">매개 변수</span><span class="sxs-lookup"><span data-stu-id="85cab-202">Parameters</span></span></td>
             <td><span data-ttu-id="85cab-203">스크립트에 필요한 경우 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="85cab-204">
             <strong>필요한 매개 변수가 없습니다</strong>.</span><span class="sxs-lookup"><span data-stu-id="85cab-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="85cab-205">
11. Azure 구독에서 새 **리소스 그룹**을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="85cab-206">12.</span><span class="sxs-lookup"><span data-stu-id="85cab-206">12.</span></span> <span data-ttu-id="85cab-207">이제 **대시보드에 고정**을 선택하여 배포를 추적하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="85cab-208"><a name="InstallCmdlets"></a>2단계: Azure PowerShell 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="85cab-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="85cab-209">Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-209">Install Azure PowerShell.</span></span> <span data-ttu-id="85cab-210">자세한 내용은 [여기][powershell-install-configure]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="85cab-211">또는 Hive 쿼리만 해당하는 경우 HDInsight의 온라인 Hive 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="85cab-212">이렇게 하려면 [Azure Portal][azure-portal]에 로그인하고 왼쪽 창에서 **HDInsight**를 클릭하여 HDInsight 클러스터 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="85cab-213">Hive 쿼리를 실행하려는 클러스터를 클릭한 후 **쿼리 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="85cab-214">Azure PowerShell 통합 스크립팅 환경을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="85cab-215">Windows 8 또는 Windows Server 2012 이상을 실행하는 컴퓨터에서는 기본 제공되는 검색 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="85cab-216">시작 화면에서 **powershell ise**를 입력하고 **Enter** 키를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="85cab-217">Windows 8 또는 Windows Server 2012 이전 버전을 실행하는 컴퓨터에서 시작 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="85cab-218">시작 메뉴에서 검색 상자에 **명령 프롬프트**를 입력한 후 결과 목록에서 **명령 프롬프트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="85cab-219">명령 프롬프트에서 **powershell_ise**를 입력하고 **Enter** 키를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="85cab-220">Azure 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="85cab-221">콘솔 창에서 **Add-AzureAccount**를 입력하고 **Enter** 키를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="85cab-222">Azure 구독과 연관된 메일 주소를 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="85cab-223">Azure 구독의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="85cab-224">**로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="85cab-225">다음 다이어그램은 Azure PowerShell 스크립팅 환경에서 중요한 부분을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Azure PowerShell에 대한 다이어그램][azure-powershell-diagram]

## <span data-ttu-id="85cab-227"><a name="RunHive"></a>3단계: Cosmos DB 및 HDInsight를 사용하여 Hive 작업 실행</span><span class="sxs-lookup"><span data-stu-id="85cab-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="85cab-228">< >로 표시된 모든 변수는 구성 설정을 사용하여 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="85cab-229">PowerShell 스크립트 창에서 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="85cab-230">쿼리 문자열 생성부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="85cab-231">여기에서는 모든 문서 시스템에서 생성된 타임스탬프(_ts) 및 고유 ID(_rid)를 Azure Cosmos DB 컬렉션에서 가져오고, 모든 문서에 해당 시간을 기록한 후 결과를 다시 새로운 Azure Cosmos DB 컬렉션에 저장하는 Hive 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="85cab-232">먼저 Azure Cosmos DB 컬렉션에서 Hive 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="85cab-233">PowerShell 스크립트 창에서 다음 코드 조각을 #1의 코드 조각 <strong>다음에</strong> 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="85cab-234">문서를 _ts 및 _rid로만 정리하려면 선택적인 DocumentDB.query 매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="85cab-235">**DocumentDB.inputCollections 이름 지정은 실수가 아니었습니다.**</span><span class="sxs-lookup"><span data-stu-id="85cab-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="85cab-236">입력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="85cab-237">그런 다음 출력 컬렉션에 대한 HIve 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="85cab-238">출력 문서 속성은 월, 일, 시간, 분 및 총 발생 횟수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85cab-239">**하지만 다시 DocumentDB.outputCollections 이름 지정은 실수가 아니었습니다.**</span><span class="sxs-lookup"><span data-stu-id="85cab-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="85cab-240">출력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="85cab-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB 출력 컬렉션 이름 1\>*,*\<DocumentDB 출력 컬렉션 이름 2\>*'</span><span class="sxs-lookup"><span data-stu-id="85cab-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="85cab-242">컬렉션 이름은 공백 없이 단일 쉼표만 사용해서 구분되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="85cab-243">문서는 여러 컬렉션 간에 라운드 로빈 방식으로 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="85cab-244">문서 일괄 처리는 하나의 컬렉션에 저장되며, 문서의 두 번째 일괄 처리는 그 다음 컬렉션에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="85cab-245">끝으로, 문서를 월, 일, 시간 및 분으로 표시하고 결과를 다시 출력 HIve 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="85cab-246">다음 스크립트 코드 조각을 추가해서 이전 쿼리로부터 HIve 작업 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="85cab-247">-File 스위치를 사용하여 HDFS에서 HiveQL 스크립트 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="85cab-248">다음 코드 조각을 추가해서 시작 시간을 저장하고 Hive 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="85cab-249">다음을 추가해서 Hive 작업이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="85cab-250">다음을 추가해서 표준 출력과 시작 및 종료 시간을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="85cab-251">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-251">**Run** your new script!</span></span> <span data-ttu-id="85cab-252">**왼쪽 탐색의 맨 위에 있는** 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="85cab-253">결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-253">Check the results.</span></span> <span data-ttu-id="85cab-254">[Azure Portal][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="85cab-255">왼쪽 패널에서 <strong>찾아보기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="85cab-256">찾아보기 패널의 오른쪽 상단에서 <strong>모두</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="85cab-257"><strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="85cab-258"><strong>Azure Cosmos DB 계정</strong>을 찾은 다음, Hive 쿼리에 지정된 출력 컬렉션과 연결된 <strong>Azure Cosmos DB 데이터베이스</strong> 및 <strong>Azure Cosmos DB 컬렉션</strong>을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="85cab-259">끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="85cab-260">Hive 쿼리 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-260">You will see the results of your Hive query.</span></span>

   ![Hive 쿼리 결과][image-hive-query-results]

## <span data-ttu-id="85cab-262"><a name="RunPig"></a>4단계: Cosmos DB 및 HDInsight를 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="85cab-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="85cab-263">< >로 표시된 모든 변수는 구성 설정을 사용하여 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="85cab-264">PowerShell 스크립트 창에서 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="85cab-265">쿼리 문자열 생성부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="85cab-266">여기에서는 모든 문서 시스템에서 생성된 타임스탬프(_ts) 및 고유 ID(_rid)를 Azure Cosmos DB 컬렉션에서 가져오고, 모든 문서에 해당 시간을 기록한 후 결과를 다시 새로운 Azure Cosmos DB 컬렉션에 저장하는 Pig 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="85cab-267">먼저 Cosmos DB의 문서를 HDInsight에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="85cab-268">PowerShell 스크립트 창에서 다음 코드 조각을 #1의 코드 조각 <strong>다음에</strong> 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="85cab-269">문서를 just _ts 및 _rid로만 정리하려면 DocumentDB 쿼리를 선택적인 DocumentDB 쿼리 매개 변수에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="85cab-270">입력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="85cab-271">'*\<DocumentDB 입력 컬렉션 이름 1\>*,*\<DocumentDB 입력 컬렉션 이름 2\>*'</span><span class="sxs-lookup"><span data-stu-id="85cab-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="85cab-272">컬렉션 이름은 공백 없이 단일 쉼표만 사용해서 구분되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="85cab-273">문서는 여러 컬렉션 간에 라운드 로빈 방식으로 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="85cab-274">문서 일괄 처리는 하나의 컬렉션에 저장되며, 문서의 두 번째 일괄 처리는 그 다음 컬렉션에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="85cab-275">그런 다음 문서에 월, 일, 시간, 분 및 총 발생 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="85cab-276">끝으로, 결과를 새 출력 컬렉션에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85cab-277">출력으로 여러 컬렉션을 추가할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="85cab-278">'\<DocumentDB 출력 컬렉션 이름 1\>,\<DocumentDB 출력 컬렉션 이름 2\>'</span><span class="sxs-lookup"><span data-stu-id="85cab-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="85cab-279">컬렉션 이름은 공백 없이 단일 쉼표만 사용해서 구분되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="85cab-280">문서는 여러 컬렉션 간에 라운드 로빈으로 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="85cab-281">문서 일괄 처리는 하나의 컬렉션에 저장되며, 문서의 두 번째 일괄 처리는 그 다음 컬렉션에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="85cab-282">다음 스크립트 코드 조각을 추가해서 이전 쿼리로부터 Pig 작업 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="85cab-283">-File 스위치를 사용하여 HDFS에서 Pig 스크립트 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="85cab-284">다음 코드 조각을 추가해서 시작 시간을 저장하고 Pig 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="85cab-285">다음을 추가해서 Pig 작업이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="85cab-286">다음을 추가해서 표준 출력과 시작 및 종료 시간을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="85cab-287">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-287">**Run** your new script!</span></span> <span data-ttu-id="85cab-288">**왼쪽 탐색의 맨 위에 있는** 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="85cab-289">결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-289">Check the results.</span></span> <span data-ttu-id="85cab-290">[Azure Portal][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="85cab-291">왼쪽 패널에서 <strong>찾아보기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="85cab-292">찾아보기 패널의 오른쪽 상단에서 <strong>모두</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="85cab-293"><strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="85cab-294"><strong>Azure Cosmos DB 계정</strong>을 찾은 다음, Pig 쿼리에 지정된 출력 컬렉션과 연결된 <strong>Azure Cosmos DB 데이터베이스</strong> 및 <strong>Azure Cosmos DB 컬렉션</strong>을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="85cab-295">끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="85cab-296">Pig 쿼리 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-296">You will see the results of your Pig query.</span></span>

    ![Pig 쿼리 결과][image-pig-query-results]

## <span data-ttu-id="85cab-298"><a name="RunMapReduce"></a>5단계: Azure Cosmos DB 및 HDInsight를 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="85cab-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="85cab-299">PowerShell 스크립트 창에서 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="85cab-300">여기에서는 Azure Cosmos DB 컬렉션에서 각 문서 속성의 발생 횟수를 기록하는 MapReduce 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="85cab-301">이 스크립트 코드 조각을 위 코드 조각 **다음에** 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="85cab-302">TallyProperties-v01.jar은 Cosmos DB Hadoop 커넥터의 사용자 지정 설치로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="85cab-303">다음 명령을 실행하여 MapReduce 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="85cab-304">MapReduce 작업 정의뿐 아니라 MapReduce 작업을 실행하려는 HDInsight 클러스터 이름 및 자격 증명도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="85cab-305">Start-AzureHDInsightJob은 비동기 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="85cab-306">작업 완료를 확인하려면 *Wait-AzureHDInsightJob* cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="85cab-307">다음 명령을 추가하여 MapReduce 작업 실행과 관련한 오류를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="85cab-308">**실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-308">**Run** your new script!</span></span> <span data-ttu-id="85cab-309">**왼쪽 탐색의 맨 위에 있는** 합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="85cab-310">결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-310">Check the results.</span></span> <span data-ttu-id="85cab-311">[Azure Portal][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="85cab-312">왼쪽 패널에서 <strong>찾아보기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="85cab-313">찾아보기 패널의 오른쪽 상단에서 <strong>모두</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="85cab-314"><strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="85cab-315"><strong>Azure Cosmos DB 계정</strong>을 찾은 다음, MapReduce 작업에 지정된 출력 컬렉션과 연결된 <strong>Azure Cosmos DB 데이터베이스</strong> 및 <strong>Azure Cosmos DB 컬렉션</strong>을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="85cab-316">끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="85cab-317">MapReduce 작업 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-317">You will see the results of your MapReduce job.</span></span>

      ![MapReduce 쿼리 결과][image-mapreduce-query-results]

## <span data-ttu-id="85cab-319"><a name="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="85cab-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="85cab-320">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-320">Congratulations!</span></span> <span data-ttu-id="85cab-321">지금까지 Azure Cosmos DB 및 HDInsight를 사용해서 첫 번째 Hive, Pig 및 MapReduce 작업을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="85cab-322">Hadoop 커넥터는 소스가 공개되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="85cab-323">관심이 있으면 [GitHub][github]에서 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85cab-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="85cab-324">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85cab-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="85cab-325">[Documentdb로 Java 응용 프로그램 개발][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="85cab-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="85cab-326">[HDInsight의 Hadoop용 Java MapReduce 프로그램 개발][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="85cab-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="85cab-327">[휴대폰 사용을 분석하기 위해 HDInsight에서 Hive와 함께 Hadoop 사용 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="85cab-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="85cab-328">[HDInsight와 함께 MapReduce 사용][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="85cab-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="85cab-329">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="85cab-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="85cab-330">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="85cab-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="85cab-331">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="85cab-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
