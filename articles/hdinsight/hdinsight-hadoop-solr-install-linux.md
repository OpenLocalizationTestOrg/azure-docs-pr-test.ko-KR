---
title: "스크립트 작업을 사용하여 Linux 기반 HDInsight에 Solr 설치 - Azure | Microsoft Docs"
description: "스크립트 작업을 사용하여 Linux 기반 HDInsight Hadoop 클러스터에 Solr를 설치하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="994e1-103">HDInsight Hadoop 클러스터에서 Solr 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="994e1-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="994e1-104">스크립트 동작을 사용하여 Azure HDInsight에 Solr을 설치하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="994e1-105">Solr은 강력한 검색 플랫폼으로서 Hadoop에서 관리하는 데이터에 대한 엔터프라이즈 수준의 검색 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="994e1-106">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="994e1-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="994e1-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="994e1-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="994e1-109">이 문서에 사용된 샘플 스크립트는 특정 구성의 Solr 4.9를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="994e1-110">다른 컬렉션, 분할, 스키마, 복제 등으로 Solr 클러스터를 구성하려는 경우 이 스크립트와 Solr 바이너리를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="994e1-111"><a name="whatis"></a>Solr이란</span><span class="sxs-lookup"><span data-stu-id="994e1-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="994e1-112">[Apache Solr](http://lucene.apache.org/solr/features.html)은 데이터에 대한 강력한 전체 텍스트 검색을 가능하게 해주는 엔터프라이즈 검색 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="994e1-113">Hadoop는 막대한 양의 데이터를 저장 및 관리할 수 있도록 해주고 Apache Solr은 이 데이터를 신속하게 검색할 수 있는 검색 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="994e1-114">HDInsight 클러스터에 제공되는 구성 요소는 Microsoft에 완벽히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="994e1-115">Solr와 같은 사용자 지정 구성 요소는 문제 해결에 도움이 되는 합리적인 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="994e1-116">Microsoft 지원은 사용자 지정 구성 요소의 문제를 해결하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="994e1-117">도움을 받기 위해 오픈 소스 커뮤니티에 참여해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="994e1-118">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="994e1-119">Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="994e1-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="994e1-120">스크립트가 수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="994e1-120">What the script does</span></span>

<span data-ttu-id="994e1-121">이 스크립트는 HDInsight 클러스터에서 다음을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="994e1-122">`/usr/hdp/current/solr`에 Solr 4.9 설치</span><span class="sxs-lookup"><span data-stu-id="994e1-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="994e1-123">Solr 서비스를 실행하는 데 사용되는 사용자 **solrusr**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="994e1-124">**solruser**을 `/usr/hdp/current/solr`의 소유자로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="994e1-125">Solr을 자동으로 시작하는 [Upstart](http://upstart.ubuntu.com/) 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="994e1-126"><a name="install"></a>스크립트 동작을 사용하여 Solr 설치</span><span class="sxs-lookup"><span data-stu-id="994e1-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="994e1-127">HDInsight 클러스터에서 Solr을 설치하는 샘플 스크립트는 다음 위치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="994e1-128">Solr이 설치된 클러스터를 만들려면 [HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-portal.md) 문서의 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="994e1-129">생성 프로세스 중 다음 단계를 사용하여 Solr을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="994e1-130">__클러스터 요약__ 블레이드에서 __고급 설정__을 선택한 다음 __스크립트 작업__을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="994e1-131">양식에 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="994e1-132">**이름**: 스크립트 동작의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="994e1-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="994e1-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="994e1-134">**HEAD**: 이 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="994e1-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="994e1-135">**WORKER**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="994e1-136">**ZOOKEEPER**: Zookeeper 노드에 설치하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="994e1-137">**PARAMETERS**: 이 필드는 공백으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="994e1-138">**스크립트 동작** 블레이드의 아래쪽에서 **선택** 단추를 사용하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="994e1-139">마지막으로 **다음** 단추를 사용하여 __클러스터 요약__으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="994e1-140">__클러스터 요약__ 페이지에서 __생성__을 선택하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="994e1-141"><a name="usesolr"></a>HDInsight에서 Solr을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="994e1-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="994e1-142">이 섹션의 단계는 기본적 Solr 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="994e1-143">Solr에 대한 자세한 내용은 [Apache Solr 사이트](http://lucene.apache.org/solr/)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="994e1-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="994e1-144">데이터 인덱싱</span><span class="sxs-lookup"><span data-stu-id="994e1-144">Index data</span></span>

<span data-ttu-id="994e1-145">다음 단계를 사용하여 Solr에 예제 데이터를 추가한 다음 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="994e1-146">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="994e1-147">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="994e1-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="994e1-148">이 문서의 뒷부분에 나오는 단계에서 SSL 터널을 사용하여 Solr 웹 UI에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="994e1-149">이러한 단계를 사용하려면 SSL 터널을 설정하고 브라우저를 구성하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="994e1-150">자세한 내용은 [HDInsight와 SSH 터널 사용](hdinsight-linux-ambari-ssh-tunnel.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="994e1-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="994e1-151">다음 명령을 사용하여 Solr 인덱스 샘플 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="994e1-152">콘솔에 다음과 같은 출력이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="994e1-153">`post.jar` 유틸리티는 인덱스에 **solr.xml** 및 **monitor.xml** 문서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="994e1-154">다음 명령을 사용하여 Solr REST API에 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="994e1-155">이 명령은 **\*:\***(쿼리 문자열에서 \*%3A\*로 인코딩)와 일치하는 모든 문서에 대해 **collection1**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="994e1-156">다음 JSON 문서는 응답의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-156">The following JSON document is an example of the response:</span></span>

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

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="994e1-157">Solr 대시보드 사용</span><span class="sxs-lookup"><span data-stu-id="994e1-157">Using the Solr dashboard</span></span>

<span data-ttu-id="994e1-158">Solr 대시보드는  웹 브라우저를 통해 Solr로 작업할 수 있는 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="994e1-159">Solr 대시보드는 HDInsight 클러스터에서 인터넷에 직접 드러나지 않지만</span><span class="sxs-lookup"><span data-stu-id="994e1-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="994e1-160">SSH 터널을 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="994e1-161">SSH 터널 사용에 대한 자세한 내용은 [HDInsight와 SSH 터널 사용](hdinsight-linux-ambari-ssh-tunnel.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="994e1-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="994e1-162">SSH 터널을 설정하면 다음 단계를 수행하여 Solr 대시보드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="994e1-163">기본 헤드 노드의 호스트 이름을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="994e1-164">SSH를 사용하여 클러스터 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="994e1-165">예: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="994e1-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="994e1-166">SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="994e1-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="994e1-167">다음 명령을 사용하여 정규화된 호스트 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="994e1-168">이 명령은 다음 호스트 이름과 유사한 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="994e1-169">반환된 값은 나중에 사용하므로 저장해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="994e1-170">브라우저에서 **http://HOSTNAME:8983/solr/#/**에 연결하며, 여기서 **HOSTNAME**은 이전 단계에서 결정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="994e1-171">요청은 SSH 터널을 통해 클러스터의 Solr 웹 UI로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="994e1-172">다음 이미지와 유사한 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-172">The page appears similar to the following image:</span></span>

    ![Solr 대시보드의 이미지](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="994e1-174">왼쪽 창에서 **코어 선택기** 드롭다운을 사용하여 **collection1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="994e1-175">여러 항목이 **collection1** 아래에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="994e1-176">**collection1** 아래의 항목에서 **쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="994e1-177">검색 페이지를 채우려면 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="994e1-178">**q** 텍스트 상자에서 **\*:**\*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="994e1-179">이 쿼리는 Solr에 인덱싱되는 모든 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="994e1-180">문서 내에서 특정 문자열을 검색하려는 경우 여기에 해당 문자열을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="994e1-181">**wt** 텍스트 상자에서 출력 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="994e1-182">기본값은 **json**입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-182">Default is **json**.</span></span>

     <span data-ttu-id="994e1-183">마지막으로 검색 페이지의 아래쪽에서 **쿼리 실행** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![스크립트 작업을 사용하여 클러스터 사용자 지정](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="994e1-185">출력은 앞에서 인덱스에 추가한 두 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="994e1-186">다음 JSON 문서와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-186">The output is similar to the following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="994e1-187">Solr 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="994e1-187">Starting and stopping Solr</span></span>

<span data-ttu-id="994e1-188">다음 명령을 사용하여 Solr을 수동으로 중지하거나 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="994e1-189">인덱싱된 데이터 백업</span><span class="sxs-lookup"><span data-stu-id="994e1-189">Backup indexed data</span></span>

<span data-ttu-id="994e1-190">Solr 데이터를 클러스터의 기본 저장소로 백업하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="994e1-191">SSH를 사용하여 클러스터에 연결하고 다음 명령을 사용하여 헤드 노드에 호스트 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="994e1-192">다음 인덱싱된 데이터의 스냅샷을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="994e1-193">**HOSTNAME**은 이전 명령에서 반환한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="994e1-194">응답은 다음 XML과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="994e1-195">디렉터리를 `/usr/hdp/current/solr/example/solr`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="994e1-196">여기에 각 컬렉션에 대한 하위 디텍터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="994e1-197">각 컬렉션 디렉터리에는 컬렉션의 스냅샷이 포함된 `data` 디렉터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="994e1-198">스냅숏 폴더의 압축 보관 파일을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="994e1-199">`snapshot.20150806185338855` 값을 컬렉션의 스냅샷 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="994e1-200">이 명령을 실행하면 **snapshot.20150806185338855** 디렉터리의 내용이 포함된 **snapshot.20150806185338855.tgz** 보관 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="994e1-201">그러면 다음 명령을 사용하여 클러스터의 기본 저장소에 아카이브를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="994e1-202">Solr 백업 및 복원 작업에 대한 자세한 내용은 [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="994e1-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="994e1-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="994e1-203">Next steps</span></span>

* <span data-ttu-id="994e1-204">[HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="994e1-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="994e1-205">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에 Giraph를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="994e1-206">Giraph를 통해 Hadoop을 사용하여 그래프 처리를 수행할 수 있으며, Azure HDInsight에서 이를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="994e1-207">[HDInsight 클러스터에서 Hue를 설치](hdinsight-hadoop-hue-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="994e1-208">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에서 Hue를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="994e1-209">Hue는 Hadoop 클러스터와 상호 작용하는 데 사용되는 웹 응용 프로그램 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="994e1-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
