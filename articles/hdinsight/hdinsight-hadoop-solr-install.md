---
title: "스크립트 작업을 사용하여 Hadoop 클러스터에 Solr 설치- Azure | Microsoft Docs"
description: "스크립트 작업을 사용하여 Solr로 HDInsight 클러스터를 사용자 지정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="81503-103">Windows 기반 HDInsight 클러스터에서 Solr 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="81503-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="81503-104">스크립트 작업을 사용하여 Solr로 Windows 기반 HDInsight 클러스터를 사용자 지정하는 방법 및 데이터를 검색하기 위해 Solr를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81503-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81503-105">이 문서의 단계는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81503-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="81503-106">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="81503-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="81503-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="81503-109">Linux 기반 클러스터와 함께 Solr을 사용한 작업에 대한 자세한 내용은 [HDInsight Hadoop 클러스터에 Solr 설치 및 사용(Linux)](hdinsight-hadoop-solr-install-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="81503-110">*스크립트 작업*을 사용하여 Azure HDInsight에서 모든 형식의 클러스터(Hadoop, Storm, HBase, Spark)에 Solr을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="81503-111">HDInsight 클러스터에 Solr을 설치하는 샘플 스크립트는 읽기 전용 Azure 저장소 Blob( [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1))에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="81503-112">샘플 스크립트는 HDInsight 클러스터 버전 3.1에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="81503-113">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="81503-114">이 항목에서 사용된 샘플 스크립트로는 특정 구성의 Windows 기반 Solr 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="81503-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="81503-115">서로 다른 컬렉션, 분할, 스키마, 복제 등으로 Solr 클러스터를 구성하려는 경우 그에 따라 이 스크립트와 Solr 바이너리를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="81503-116">**관련된 문서**</span><span class="sxs-lookup"><span data-stu-id="81503-116">**Related articles**</span></span>

* [<span data-ttu-id="81503-117">HDInsight Hadoop 클러스터에서 Solr 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="81503-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="81503-118">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="81503-119">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="81503-120">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="81503-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="81503-121">Solr이란?</span><span class="sxs-lookup"><span data-stu-id="81503-121">What is Solr?</span></span>
<span data-ttu-id="81503-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a>은 데이터에 대한 강력한 전체 텍스트 검색을 가능하게 해주는 엔터프라이즈 검색 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="81503-123">Hadoop는 막대한 양의 데이터를 저장 및 관리할 수 있도록 해주고 Apache Solr은 이 데이터를 신속하게 검색할 수 있는 검색 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="81503-124">포털을 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="81503-124">Install Solr using portal</span></span>
1. <span data-ttu-id="81503-125">**HDInsight에서 Hadoop 클러스터 만들기**에서 설명한 대로 [사용자 지정 만들기](hdinsight-provision-clusters.md) 옵션을 사용하여 클러스터를 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="81503-126">아래와 같이 마법사의 **스크립트 동작** 페이지에서 **스크립트 동작 추가**를 클릭하여 스크립트 동작에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="81503-127">![스크립트 작업을 사용하여 클러스터 사용자 지정](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "스크립트 작업을 사용하여 클러스터 사용자 지정")</span><span class="sxs-lookup"><span data-stu-id="81503-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="81503-128">속성</span><span class="sxs-lookup"><span data-stu-id="81503-128">Property</span></span></th><th><span data-ttu-id="81503-129">값</span><span class="sxs-lookup"><span data-stu-id="81503-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="81503-130">이름</span><span class="sxs-lookup"><span data-stu-id="81503-130">Name</span></span></td>
            <td><span data-ttu-id="81503-131">스크립트 작업의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-131">Specify a name for the script action.</span></span> <span data-ttu-id="81503-132">예를 들면 <b>Install Solr</b>과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="81503-133">스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="81503-133">Script URI</span></span></td>
            <td><span data-ttu-id="81503-134">클러스터를 사용자 지정하기 위해 호출되는 스크립트에 URI(Uniform Resource Identifier)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="81503-135">예를 들면 <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i>과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="81503-136">노드 유형</span><span class="sxs-lookup"><span data-stu-id="81503-136">Node Type</span></span></td>
            <td><span data-ttu-id="81503-137">사용자 지정 스크립트가 실행되는 노드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="81503-138"><b>모든 노드</b>, <b>헤드 노드만</b> 또는 <b>작업자 노드만</b>을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="81503-139">매개 변수</span><span class="sxs-lookup"><span data-stu-id="81503-139">Parameters</span></span></td>
            <td><span data-ttu-id="81503-140">스크립트에 필요한 경우 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="81503-141">Solr을 설치하는 스크립트에는 매개 변수가 필요하지 않으므로 비워 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="81503-142">두 개 이상의 스크립트 작업을 추가하여 클러스터에 여러 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="81503-143">스크립트를 추가한 후 확인 표시를 클릭하여 클러스터 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="81503-144">Solr 사용</span><span class="sxs-lookup"><span data-stu-id="81503-144">Use Solr</span></span>
<span data-ttu-id="81503-145">데이터 파일로 Solr을 인덱싱하는 것부터 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="81503-146">그런 다음 인덱싱한 데이터에 대해 Solr을 사용하여 검색 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="81503-147">HDInsight 클러스터에서 Solr을 사용하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="81503-148">**RDP(원격 데스크톱 프로토콜)를 사용하여 Solr이 설치된 HDInsight 클러스터에 원격으로 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="81503-149">Azure 포털에서 Solr을 설치하여 만든 클러스터에 대해 원격 데스크톱을 사용하도록 설정한 다음 클러스터에 원격으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="81503-150">지침은 [RDP를 사용하여 HDInsight 클러스터에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="81503-151">**데이터 파일을 업로드하여 Solr을 인덱싱**합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="81503-152">Solr을 인덱싱할 때 검색이 필요할 수 있는 문서를 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="81503-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="81503-153">Solr을 인덱싱하려면 RDP를 사용하여 클러스터에 원격으로 연결한 다음 Hadoop 명령줄을 열고 **C:\apps\dist\solr-4.7.2\example\exampledocs**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="81503-154">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="81503-155">콘솔에 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81503-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="81503-156">post.jar 유틸리티는 두 개의 샘플 문서, 즉 **solr.xml** 및 **monitor.xml**로 Solr을 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="81503-157">post.jar 유틸리티와 샘플 문서는 Solr 설치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="81503-158">**Solr 대시보드를 사용하여 인덱싱된 문서 내에서 검색합니다**.</span><span class="sxs-lookup"><span data-stu-id="81503-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="81503-159">HDInsight 클러스터에 대한 RDP 세션에서 Internet Explorer를 열고 **http://headnodehost:8983/solr/#/**에서 Solr 대시보드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="81503-160">왼쪽 창의 **코어 선택기** 드롭다운에서 **collection1**을 선택하고, 그 안에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="81503-161">한 예로, Solr의 모든 문서를 선택하고 반환하려면 다음 값을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="81503-162">**q** 텍스트 상자에서 **\*:**\*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="81503-163">이렇게 하면 Solr에서 인덱싱되는 문서는 모두 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="81503-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="81503-164">문서 내에서 특정 문자열을 검색하려는 경우 여기에 해당 문자열을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="81503-165">**wt** 텍스트 상자에서 출력 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="81503-166">기본값은 **json**입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-166">Default is **json**.</span></span> <span data-ttu-id="81503-167">**Execute Query**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="81503-168">![스크립트 작업을 사용하여 클러스터 사용자 지정](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Solr 대시보드에서 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="81503-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="81503-169">출력에는 Solr 인덱싱에 사용되는 두 문서가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="81503-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="81503-170">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
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
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
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
4. <span data-ttu-id="81503-171">**권장: Solr에서 인덱싱된 데이터를 HDInsight 클러스터와 연결된 Azure Blob 저장소에 백업합니다**.</span><span class="sxs-lookup"><span data-stu-id="81503-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="81503-172">Solr 클러스터 노드에서 인덱싱된 데이터를 Azure Blob 저장소에 백업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81503-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="81503-173">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="81503-174">RDP 세션에서 Internet Explorer를 열고 다음 URL을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="81503-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="81503-175">다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81503-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="81503-176">원격 세션에서 {SOLR_HOME}\{Collection}\data로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="81503-177">샘플 스크립트를 통해 만든 클러스터의 경우 이 경로는 **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="81503-178">이 위치에서 **snapshot.*timestamp***와 비슷한 이름으로 만든 스냅숏 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81503-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="81503-179">스냅숏 폴더를 압축하고 Azure Blob 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="81503-180">Hadoop 명령줄에서 다음 명령을 사용하여 스냅숏 폴더의 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="81503-181">이 명령은 스냅숏을 클러스터와 연결된 기본 저장소 계정 내의 컨테이너 아래에 있는 /example/data/에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="81503-182">Aure PowerShell을 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="81503-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="81503-183">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="81503-184">샘플은 Azure PowerShell을 사용하여 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="81503-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="81503-185">스크립트를 사용자 지정하여 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="81503-186">.NET SDK를 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="81503-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="81503-187">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81503-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="81503-188">샘플은 .NET SDK를 사용하여 Spark를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="81503-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="81503-189">스크립트를 사용자 지정하여 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81503-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="81503-190">참고 항목</span><span class="sxs-lookup"><span data-stu-id="81503-190">See also</span></span>
* [<span data-ttu-id="81503-191">HDInsight Hadoop 클러스터에서 Solr 설치 및 사용(Linux)</span><span class="sxs-lookup"><span data-stu-id="81503-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="81503-192">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-provision-clusters.md): HDInsight 클러스터를 만드는 방법에 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="81503-193">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]: 스크립트 작업을 사용하여 HDInsight 클러스터를 사용자 지정하는 데 대한 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="81503-194">[HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="81503-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="81503-195">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]: Spark 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="81503-196">[HDInsight 클러스터에서 R 설치][hdinsight-install-r]: R 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="81503-197">[HDInsight 클러스터에서 Giraph 설치](hdinsight-hadoop-giraph-install.md): Giraph 설치에 대한 스크립트 작업 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="81503-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
