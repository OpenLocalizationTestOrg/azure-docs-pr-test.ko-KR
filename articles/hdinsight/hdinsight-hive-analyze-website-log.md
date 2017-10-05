---
title: "Hadoop에서 웹 사이트 로그 분석에 Hive 사용 - Azure HDInsight | Microsoft Docs"
description: "HDInsight와 함께 Hive를 사용하여 웹 사이트 로그를 분석하는 방법에 대해 알아봅니다. 로그 파일을 HDInsight 테이블에 대한 입력으로 사용하고 HiveQL을 사용해 데이터를 쿼리합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="2e951-104">Windows 기반 HDInsight와 함께 Hive를 사용하여 웹 사이트의 로그 분석</span><span class="sxs-lookup"><span data-stu-id="2e951-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="2e951-105">HDInsight와 함께 HiveQL을 사용하여 웹 사이트의 로그를 분석하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="2e951-106">웹 사이트 로그 분석을 통해 비슷한 활동을 기준으로 대상을 구분하고, 인구 통계별로 사이트 방문자를 분류하고, 방문자가 보는 콘텐츠와 이전에 방문했던 웹 사이트 등을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e951-107">이 문서의 단계는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2e951-108">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="2e951-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2e951-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e951-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="2e951-111">이 샘플에서는 HDInsight 클러스터를 사용하여 웹 사이트 로그 파일을 분석해 외부 웹 사이트로부터의 방문 빈도를 파악하고,</span><span class="sxs-lookup"><span data-stu-id="2e951-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="2e951-112">사용자에게 발생하는 웹 사이트 오류의 요약을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="2e951-113">다음 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-113">You will learn how to:</span></span>

* <span data-ttu-id="2e951-114">웹 사이트 로그 파일이 포함된 Azure Blob 저장소에 연결</span><span class="sxs-lookup"><span data-stu-id="2e951-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="2e951-115">HIVE 테이블을 만들어 이러한 로그 쿼리</span><span class="sxs-lookup"><span data-stu-id="2e951-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="2e951-116">HIVE 쿼리를 만들어 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="2e951-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="2e951-117">Microsoft Excel에서 ODBC(Open Database Connectivity)를 통해 HDInsight에 연결하여 분석된 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="2e951-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="2e951-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2e951-119">Prerequisites</span></span>
* <span data-ttu-id="2e951-120">Azure HDInsight에서 Hadoop 클러스터를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="2e951-121">관련 지침은 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e951-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="2e951-122">Microsoft Excel 2013 또는 Excel 2010을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="2e951-123">Hive에서 Excel로 데이터를 가져오려면 [Microsoft Hive ODBC 드라이버](http://www.microsoft.com/download/details.aspx?id=40886) 가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="2e951-124">샘플을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="2e951-124">To run the sample</span></span>
1. <span data-ttu-id="2e951-125">[Azure 포털](https://portal.azure.com/)의 시작 보드(클러스터를 여기에 고정한 경우)에서 샘플을 실행할 클러스터 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="2e951-126">클러스터 블레이드의 **빠른 링크** 아래에서 **클러스터 대시보드**를 클릭한 다음 **클러스터 대시보드** 블레이드에서 **HDInsight 클러스터 대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="2e951-127">다음 URL을 사용하여 대시보드를 직접 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="2e951-128">메시지가 표시되면 클러스터를 프로비전할 때 사용한 관리자 사용자 이름과 암호를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="2e951-129">웹 페이지가 열리면 **갤러리 시작** 탭을 클릭하고 **샘플 데이터가 있는 솔루션** 범주에서 **웹 사이트 데이터 분석** 샘플을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="2e951-130">웹 페이지에서 제공되는 지침에 따라 샘플을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e951-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e951-131">Next steps</span></span>
<span data-ttu-id="2e951-132">[HDInsight에서 Hive를 사용하여 센서 데이터 분석](hdinsight-hive-analyze-sensor-data.md)샘플을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e951-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
