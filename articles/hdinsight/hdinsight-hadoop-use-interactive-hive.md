---
title: "HDInsight에서 대화형 Hive 사용 - Azure | Microsoft Docs"
description: "HDInsight에서 대화형 Hive(LLAP에서 Hive)를 사용 하는 방법에 대해 알아봅니다."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="9edbd-103">HDInsight에서 대화형 Hive 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="9edbd-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="9edbd-104">대화형 Hive(즉,</span><span class="sxs-lookup"><span data-stu-id="9edbd-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="9edbd-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP))는 새로운 HDInsight [클러스터 유형](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)입니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="9edbd-106">대화형 Hive에서는 메모리 내 캐싱이 가능하여 Hive 쿼리의 대화형 방식을 강화하고 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="9edbd-107">이 새로운 기능은 HDInsight를 세계에서 가장 효율적이고 유연하며, 메모리 내 캐시(Hive 및 Spark 사용) 및 R 서비스와 긴밀히 통합된 고급 분석을 갖춘 클라우드 기반의 개방된 빅 데이터 솔루션으로 만드는 요소 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="9edbd-108">대화형 Hive 클러스터는 Hadoop 클러스터와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="9edbd-109">Hive 서비스만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="9edbd-110">MapReduce, Pig, Sqoop, Oozie 및 기타 서비스는 이 클러스터 유형에서 곧 제거될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="9edbd-111">대화형 Hive 클러스터의 Hive 서비스는 Ambari Hive View, Beeline 및 Hive ODBC를 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="9edbd-112">Hive 콘솔, Templeton, Azure CLI 및 Azure PowerShell을 통해서는 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="9edbd-113">대화형 Hive 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9edbd-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="9edbd-114">대화형 Hive 클러스터는 Linux 기반 클러스터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="9edbd-115">HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9edbd-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="9edbd-116">대화형 Hive에서 Hive 실행</span><span class="sxs-lookup"><span data-stu-id="9edbd-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="9edbd-117">Hive 쿼리를 실행하는 방식에 대한 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="9edbd-118">Ambari Hive View를 사용하여 Hive 실행</span><span class="sxs-lookup"><span data-stu-id="9edbd-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="9edbd-119">Hive View 사용에 대한 자세한 내용은 [HDInsight에서 Hadoop과 Hive View 사용](hdinsight-hadoop-use-hive-ambari-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9edbd-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="9edbd-120">Beeline을 사용하여 Hive 실행</span><span class="sxs-lookup"><span data-stu-id="9edbd-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="9edbd-121">HDInsight에서 Beeline 사용에 대한 자세한 내용은 [Beeline을 사용하여 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-beeline.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9edbd-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="9edbd-122">헤드 노드 또는 빈 에지 노드에서 Beeline을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="9edbd-123">빈 에지 노드에서 Beeline을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="9edbd-124">빈 에지 노드로 HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9edbd-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="9edbd-125">Hive ODBC를 사용하여 Hive 실행</span><span class="sxs-lookup"><span data-stu-id="9edbd-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="9edbd-126">Hive ODBC 사용에 대한 자세한 내용은 [Microsoft Hive ODBC 드라이버로 Hadoop에 Excel 연결](hdinsight-connect-excel-hive-odbc-driver.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9edbd-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="9edbd-127">**JDBC 연결 문자열을 찾으려면:**</span><span class="sxs-lookup"><span data-stu-id="9edbd-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="9edbd-128">다음 URL을 사용하여 Ambari에 로그인합니다. https://<ClusterName>.AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="9edbd-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="9edbd-129">왼쪽 메뉴에서 **Hive** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="9edbd-130">강조 표시된 아이콘을 클릭하여 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![HDInsight Hadoop 대화형 Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="9edbd-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9edbd-132">See also</span></span>
* <span data-ttu-id="9edbd-133">[HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md): HDInsight에서 대화형 Hive 클러스터를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="9edbd-134">[Beeline를 사용하여 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-beeline.md): Beeline을 사용하여 Hive 쿼리를 제출하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="9edbd-135">[Microsoft Hive ODBC 드라이버로 Hadoop에 Excel 연결](hdinsight-connect-excel-hive-odbc-driver.md): Excel을 Hive에 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9edbd-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

