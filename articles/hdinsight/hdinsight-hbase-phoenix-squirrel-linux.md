---
title: "HBase에서 Apache Phoenix & SQuirreL 사용 - Azure HDInsight | Microsoft Docs"
description: "HDInsight에서 Apache Phoenix를 사용하는 방법 및 워크스테이션에서 SQuirreL을 설치 및 구성하여 HDInsight에서 HBase 클러스터에 연결하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="6b8a1-103">HDInsight에서 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용</span><span class="sxs-lookup"><span data-stu-id="6b8a1-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="6b8a1-104">HDInsight에서 [Apache Phoenix](http://phoenix.apache.org/) 를 사용하는 방법 및 SQLLine을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="6b8a1-105">Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="6b8a1-106">Phoenix 문법은 [피닉스 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="6b8a1-107">HDInsight의 Phoenix 버전 정보는 [HDInsight에서 제공하는 Hadoop 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="6b8a1-108">SQLLine 사용</span><span class="sxs-lookup"><span data-stu-id="6b8a1-108">Use SQLLine</span></span>
<span data-ttu-id="6b8a1-109">[SQLLine](http://sqlline.sourceforge.net/)은 SQL을 실행하는 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6b8a1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6b8a1-110">Prerequisites</span></span>
<span data-ttu-id="6b8a1-111">SQLLine을 시작하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="6b8a1-112">**HDInsight의 HBase 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="6b8a1-113">HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="6b8a1-114">**원격 데스크톱 프로토콜을 통해 HBase 클러스터에 연결**.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="6b8a1-115">지침의 경우 [Azure Portal을 사용하여 HDInsight에서 Hadoop 클러스터 관리][hdinsight-manage-portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="6b8a1-116">HBase 클러스터에 연결할 때 Zookeeper 중 하나에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="6b8a1-117">각 HDInsight 클러스터에는 3개의 Zookeeper가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="6b8a1-118">**Zookeeper 호스트 이름을 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="6b8a1-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="6b8a1-119">**https://<ClusterName>.azurehdinsight.net**으로 이동하여 Ambari를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="6b8a1-120">HTTP(클러스터) 사용자 이름 및 암호를 입력하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="6b8a1-121">왼쪽 메뉴에서 **Zookeeper** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="6b8a1-122">나열된 **ZooKeeper 서버** 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="6b8a1-123">나열된 **ZooKeeper 서버** 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="6b8a1-124">요약 창에서 **호스트 이름**을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="6b8a1-125">*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="6b8a1-126">**SQLLine을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="6b8a1-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="6b8a1-127">SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="6b8a1-128">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6b8a1-129">SSH에서 다음 명령을 실행하여 SQLLine을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="6b8a1-130">다음 명령을 실행하여 HBase 테이블을 만들고 일부 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="6b8a1-131">자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b8a1-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b8a1-132">Next steps</span></span>
<span data-ttu-id="6b8a1-133">이 문서에서는 HDInsight에서 Apache Phoenix를 사용하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="6b8a1-134">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-134">To learn more, see:</span></span>

* <span data-ttu-id="6b8a1-135">[HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="6b8a1-136">[Azure Virtual Network에서 HBase 클러스터 프로비전][hdinsight-hbase-provision-vnet]: Virtual Network 통합을 사용하면 응용 프로그램이 HBase와 직접 통신할 수 있도록 응용 프로그램과 동일한 Virtual Network에 HBase 클러스터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="6b8a1-137">[HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 두 Azure 데이터 센터에서 HBase 복제를 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="6b8a1-138">[HDInsight에서 HBase를 사용하여 Twitter 감정][hbase-twitter-sentiment]: HDInsight의 Hadoop 클러스터에서 HBase를 사용하여 빅 데이터에 대한 실시간 [감정 분석](http://en.wikipedia.org/wiki/Sentiment_analysis)을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b8a1-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
