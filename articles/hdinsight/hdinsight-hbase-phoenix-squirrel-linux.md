---
title: "aaaUse Apache 피닉스 & HBase-Azure HDInsight를 스 쿼 럴 | Microsoft Docs"
description: "자세한 방법을 toouse, HDInsight의 Apache 피닉스 방법과 tooinstall 스 쿼 럴 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다."
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
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="408eb-103">HDInsight에서 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용</span><span class="sxs-lookup"><span data-stu-id="408eb-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="408eb-104">자세한 방법을 toouse [Apache 피닉스](http://phoenix.apache.org/) , HDInsight의 방법과 toouse SQLLine 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="408eb-105">Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="408eb-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="408eb-106">Hello 피닉스 문법에 대 한 참조 [피닉스 문법](http://phoenix.apache.org/language/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="408eb-107">HDInsight의 버전 정보 피닉스 hello에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="408eb-108">SQLLine 사용</span><span class="sxs-lookup"><span data-stu-id="408eb-108">Use SQLLine</span></span>
<span data-ttu-id="408eb-109">[SQLLine](http://sqlline.sourceforge.net/) 명령줄 유틸리티 tooexecute SQL 됩니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="408eb-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="408eb-110">Prerequisites</span></span>
<span data-ttu-id="408eb-111">SQLLine를 사용 하려면 먼저 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="408eb-112">**HDInsight의 HBase 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="408eb-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="408eb-113">HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="408eb-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="408eb-114">**Hello 원격 데스크톱 프로토콜을 통해 toohello HBase 클러스터를 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="408eb-115">자세한 내용은 [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello][hdinsight-manage-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="408eb-116">Tooan HBase 클러스터를 연결 하면 hello 사육의 tooconnect tooone가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="408eb-117">각 HDInsight 클러스터에는 3개의 Zookeeper가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="408eb-118">**toofind hello 사육 호스트 이름**</span><span class="sxs-lookup"><span data-stu-id="408eb-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="408eb-119">Ambari 너무 이동 하 여 열고**https://<ClusterName>. azurehdinsight.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="408eb-120">Hello HTTP (클러스터) toologin 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="408eb-121">클릭 **사육** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="408eb-122">나열된 **ZooKeeper 서버** 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="408eb-123">Hello 중 하나를 클릭 **사육 서버** 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="408eb-124">Hello 요약 창에서 찾을 hello **Hostname**합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="408eb-125">비슷합니다 너무*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="408eb-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="408eb-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="408eb-127">SSH를 사용 하 여 toohello 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="408eb-128">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="408eb-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="408eb-129">SSH에서 다음 명령을 toorun SQLLine hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="408eb-130">명령을 toocreate 다음 hello HBase 테이블을 실행 하 고 일부 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="408eb-131">자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="408eb-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="408eb-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="408eb-132">Next steps</span></span>
<span data-ttu-id="408eb-133">이 문서에서는 배웠습니다 어떻게 toouse HDInsight의 Apache 피닉스 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="408eb-134">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="408eb-134">toolearn more, see:</span></span>

* <span data-ttu-id="408eb-135">[HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="408eb-136">[Azure 가상 네트워크에서 HBase 클러스터를 프로 비전][hdinsight-hbase-provision-vnet]: 가상 네트워크 통합 HBase 클러스터 동일한 가상 네트워크로 응용 프로그램 이므로 배포 된 toohello 수 있는 응용 프로그램이 통신할 수 HBase에 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="408eb-137">[HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 자세한 방법 두 Azure 데이터 센터에서 tooconfigure HBase 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="408eb-138">[HDInsight에서 HBase와 Twitter 감성 분석][hbase-twitter-sentiment]: 자세한 방법을 toodo 실시간 [감성 분석](http://en.wikipedia.org/wiki/Sentiment_analysis) HDInsight의 Hadoop 클러스터의 HBase를 사용 하 여 빅 데이터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="408eb-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
