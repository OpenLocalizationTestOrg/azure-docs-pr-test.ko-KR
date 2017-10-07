---
title: "Hadoop 클러스터-Azure에서 aaaUse 스크립트 동작 tooinstall Solr | Microsoft Docs"
description: "스크립트 동작을 사용 하 여 Solr 인 toocustomize HDInsight 클러스터를 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="993cf-103">Windows 기반 HDInsight 클러스터에서 Solr 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="993cf-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="993cf-104">스크립트 동작을 사용 하 여 Solr 인 toocustomize Windows 기반 HDInsight 클러스터를 방법 등에 대해 알아보기 toouse Solr toosearch 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="993cf-105">이 문서 에서만 작동 하는 Windows 기반 HDInsight 클러스터의에서 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="993cf-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="993cf-106">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="993cf-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="993cf-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="993cf-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="993cf-109">Linux 기반 클러스터와 함께 Solr을 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Solr 설치 및 사용(Linux)](hdinsight-hadoop-solr-install-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="993cf-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="993cf-110">*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 Solr을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="993cf-111">HDInsight 클러스터에서 샘플 스크립트 tooinstall Solr에서 읽기 전용 Azure 저장소 blob에서 사용할 수는 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="993cf-112">hello 샘플 스크립트는 HDInsight 클러스터 버전 3.1과만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="993cf-113">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="993cf-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="993cf-114">이 항목에 사용 된 hello 샘플 스크립트는 특정 구성으로 Windows 기반 Solr 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="993cf-115">Tooconfigure hello Solr 클러스터에 다른 컬렉션, 분할 된 데이터베이스, 스키마, 복제본 등을 사용 하도록 하려는 경우 수정 해야 hello 스크립트 및 Solr 이진 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="993cf-116">**관련된 문서**</span><span class="sxs-lookup"><span data-stu-id="993cf-116">**Related articles**</span></span>

* [<span data-ttu-id="993cf-117">HDInsight Hadoop 클러스터에서 Solr 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="993cf-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="993cf-118">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="993cf-119">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="993cf-120">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="993cf-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="993cf-121">Solr이란?</span><span class="sxs-lookup"><span data-stu-id="993cf-121">What is Solr?</span></span>
<span data-ttu-id="993cf-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a>은 데이터에 대한 강력한 전체 텍스트 검색을 가능하게 해주는 엔터프라이즈 검색 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="993cf-123">Hadoop에 저장 하 고 방대한 양의 데이터를 관리 있습니다, Apache Solr hello 검색 기능이 제공 tooquickly hello 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="993cf-124">포털을 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="993cf-124">Install Solr using portal</span></span>
1. <span data-ttu-id="993cf-125">Hello를 사용 하 여 클러스터를 만들기 시작 **사용자 지정 만들기** 옵션에 설명 된 대로 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-provision-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="993cf-126">Hello에 **스크립트 동작** 페이지 hello 마법사의 클릭 **스크립트 동작 추가** 아래와 같이 tooprovide hello 스크립트 동작에 대 한 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="993cf-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="993cf-127">![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")</span><span class="sxs-lookup"><span data-stu-id="993cf-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="993cf-128">속성</span><span class="sxs-lookup"><span data-stu-id="993cf-128">Property</span></span></th><th><span data-ttu-id="993cf-129">값</span><span class="sxs-lookup"><span data-stu-id="993cf-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="993cf-130">이름</span><span class="sxs-lookup"><span data-stu-id="993cf-130">Name</span></span></td>
            <td><span data-ttu-id="993cf-131">Hello 스크립트 동작에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-131">Specify a name for hello script action.</span></span> <span data-ttu-id="993cf-132">예를 들면 <b>Install Solr</b>과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="993cf-133">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="993cf-133">Script URI</span></span></td>
            <td><span data-ttu-id="993cf-134">호출 된 toocustomize hello 클러스터는 hello 식별자 URI (Uniform Resource) toohello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="993cf-135">예를 들면 <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="993cf-136">노드 유형</span><span class="sxs-lookup"><span data-stu-id="993cf-136">Node Type</span></span></td>
            <td><span data-ttu-id="993cf-137">Hello 사용자 지정 스크립트가 실행 되는 hello 노드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="993cf-138"><b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="993cf-139">매개 변수</span><span class="sxs-lookup"><span data-stu-id="993cf-139">Parameters</span></span></td>
            <td><span data-ttu-id="993cf-140">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="993cf-141">hello 스크립트 tooinstall Solr 모든 매개 변수를 필요 하지 않으므로이 비워 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="993cf-142">Hello 클러스터에서 둘 이상의 스크립트 동작 tooinstall 여러 구성 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="993cf-143">Hello 스크립트를 추가한 후 hello 확인 표시 toostart hello 클러스터 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="993cf-144">Solr 사용</span><span class="sxs-lookup"><span data-stu-id="993cf-144">Use Solr</span></span>
<span data-ttu-id="993cf-145">데이터 파일로 Solr을 인덱싱하는 것부터 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="993cf-146">Toorun 검색 쿼리 Solr hello 인덱싱된 데이터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="993cf-147">Hello 단계 toouse Solr HDInsight 클러스터에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="993cf-148">**Tooremote 프로토콜 RDP (원격 데스크톱)를 사용 하 여 설치 Solr와 hello HDInsight 클러스터에**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="993cf-149">Hello Azure 포털에서에서 Solr 설치 되어 있으며 다음 원격으로 hello 클러스터를 사용 하 여 만든 hello 클러스터에 대 한 원격 데스크톱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="993cf-150">자세한 내용은 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="993cf-151">**데이터 파일을 업로드하여 Solr을 인덱싱**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="993cf-152">Solr 인덱싱하면 기록 하는 모든 문서 toosearch에 필요할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="993cf-153">tooindex Solr 사용 하 여 RDP tooremote hello 클러스터로 이동 toohello 데스크톱 hello Hadoop 명령줄을 열고 너무 이동**C:\apps\dist\solr-4.7.2\example\exampledocs**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="993cf-154">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="993cf-155">Hello hello 콘솔에 출력 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="993cf-156">hello post.jar 유틸리티 두 예제 문서를 사용 하 여 Solr를 인덱스 **solr.xml** 및 **monitor.xml**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="993cf-157">hello post.jar 유틸리티 및 hello 샘플 문서는 Solr 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="993cf-158">**Hello 내에서 사용 하 여 hello Solr 대시보드 toosearch 인덱싱된 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="993cf-159">Hello RDP 세션 toohello HDInsight 클러스터, Internet Explorer를 열어 및 시작 시 hello Solr 대시보드 **http://headnodehost:8983/solr / #/**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="993cf-160">Hello 왼쪽 창의 hello에서 **코어 선택기** 드롭다운 목록에서 선택 **collection1**, 클릭 하 고 **쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="993cf-161">예, tooselect 및 반환 Solr에서 모든 hello docs hello 다음 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="993cf-162">Hello에 **q** 텍스트 상자에 입력  **\*:**\*합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="993cf-163">이렇게 하면 Solr에 인덱싱된 모든 hello 문서가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="993cf-164">Toosearch hello 문서 내에서 특정 문자열을 하려는 경우에 여기에 해당 문자열을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="993cf-165">Hello에 **wt** 텍스트 상자, 선택 hello 출력 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="993cf-166">기본값은 **json**입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-166">Default is **json**.</span></span> <span data-ttu-id="993cf-167">**Execute Query**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="993cf-168">![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "쿼리 Solr 대시보드에서 실행")</span><span class="sxs-lookup"><span data-stu-id="993cf-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="993cf-169">hello 출력 hello 인덱싱 Solr에 대해 두 명의 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="993cf-170">hello 출력 hello 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="993cf-171">**권장: hello 백업 Solr tooAzure hello HDInsight 클러스터와 연결 된 Blob 저장소에서에서 데이터를 인덱싱할**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="993cf-172">것이 좋습니다 Azure Blob 저장소에 hello Solr 클러스터 노드에서 hello 인덱싱된 데이터를 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="993cf-173">Hello 단계 toodo 되므로 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="993cf-174">Hello RDP 세션에서 Internet Explorer 및 지점 toohello url을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="993cf-175">다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="993cf-176">Hello 원격 세션에서 탐색 너무 {SOLR_HOME}\{컬렉션} \data 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="993cf-177">이 hello 샘플 스크립트를 통해 만든 hello 클러스터에 대 한 해야 **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="993cf-178">이 위치에서 사용 하 여 만든 이름을 비슷한 너무 스냅숏 폴더를 표시 되어야**스냅숏.* 타임 스탬프** *입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="993cf-179">TooAzure Blob 저장소에 업로드 하 고 hello 스냅숏 폴더를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="993cf-180">Hello Hadoop 명령줄에서 다음 명령을 hello를 사용 하 여 toohello hello 스냅숏 폴더 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="993cf-181">이 명령은 복사본 hello 스냅숏 너무/예제/데이터/hello 기본 저장소 내 hello 컨테이너에서 hello 클러스터와 연결 된 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="993cf-182">Aure PowerShell을 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="993cf-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="993cf-183">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="993cf-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="993cf-184">hello 샘플 방법을 tooinstall Azure PowerShell을 사용 하 여 Spark 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="993cf-185">Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="993cf-186">.NET SDK를 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="993cf-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="993cf-187">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="993cf-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="993cf-188">hello 샘플 방법을 tooinstall Spark.NET SDK hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="993cf-189">Toocustomize hello 스크립트 toouse 필요한 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="993cf-190">참고 항목</span><span class="sxs-lookup"><span data-stu-id="993cf-190">See also</span></span>
* [<span data-ttu-id="993cf-191">HDInsight Hadoop 클러스터에서 Solr 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="993cf-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="993cf-192">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="993cf-193">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="993cf-194">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="993cf-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="993cf-195">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="993cf-196">[HDInsight 클러스터에서 R 설치][hdinsight-install-r]: R 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="993cf-197">[HDInsight 클러스터에서 Giraph 설치](hdinsight-hadoop-giraph-install.md): Giraph 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="993cf-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
