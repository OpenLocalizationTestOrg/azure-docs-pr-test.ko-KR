---
title: "웹 사이트 로그 분석-Azure HDInsight 하이브 Hadoop으로 aaaUse | Microsoft Docs"
description: "HDInsight tooanalyze 웹 사이트와 하이브 toouse 기록 하는 방법에 대해 알아봅니다. 로그 파일은 HDInsight 테이블에 대 한 입력으로 사용 하 고 HiveQL tooquery hello 데이터를 사용 합니다."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="a9dab-104">하이브를 사용 하 여 웹 사이트에서 Windows 기반 HDInsight tooanalyze 로그</span><span class="sxs-lookup"><span data-stu-id="a9dab-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="a9dab-105">웹 사이트에서 HDInsight tooanalyze와 toouse HiveQL을 기록 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="a9dab-106">웹 사이트의 로그 분석 유사한 작업에 따라 대상 그룹 사용된 toosegment 수, 인구 통계 및 toofind 볼 hello 콘텐츠,에서 온 hello 웹 사이트 등에 아웃 하 여 사이트 방문자를 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9dab-107">이 문서 에서만 작동 하는 Windows 기반 HDInsight 클러스터의에서 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="a9dab-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a9dab-108">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="a9dab-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a9dab-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9dab-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="a9dab-111">이 샘플에서는 하루에에서 HDInsight 클러스터 tooanalyze 웹 사이트 로그 파일 tooget 통찰력을 외부 웹 사이트에서에서 환자가 내 원 toohello 웹 사이트의 hello 빈도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="a9dab-112">또한 hello 발생 하는 웹 사이트 오류의 요약을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="a9dab-113">다음 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-113">You will learn how to:</span></span>

* <span data-ttu-id="a9dab-114">Tooa 웹 사이트의 로그 파일을 포함 하는 Azure Blob 저장소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="a9dab-115">만들기 하이브 테이블 tooquery 이러한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="a9dab-116">하이브 쿼리 tooanalyze hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="a9dab-117">Microsoft Excel tooconnect tooHDInsight (열려 있는 데이터베이스 연결 (ODBC) tooretrieve hello 분석 데이터를 사용 하 여 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a9dab-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="a9dab-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9dab-119">Prerequisites</span></span>
* <span data-ttu-id="a9dab-120">Azure HDInsight에서 Hadoop 클러스터를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="a9dab-121">관련 지침은 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9dab-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="a9dab-122">Microsoft Excel 2013 또는 Excel 2010을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="a9dab-123">있어야 [Microsoft ODBC Driver 하이브](http://www.microsoft.com/download/details.aspx?id=40886) Excel로 하이브에서 tooimport 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="a9dab-124">toorun hello 예제</span><span class="sxs-lookup"><span data-stu-id="a9dab-124">toorun hello sample</span></span>
1. <span data-ttu-id="a9dab-125">Hello에서 [Azure 포털](https://portal.azure.com/), hello (hello 클러스터에 없는 고정) 하는 경우 시작 보드에서에서 toorun hello 샘플 원하는 hello 클러스터 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="a9dab-126">Hello에서 블레이드에서 아래에서 클러스터 **빠른 링크**, 클릭 **클러스터 대시보드**, 한 다음 hello **클러스터 대시보드** 블레이드에서 클릭 **HDInsight 클러스터 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="a9dab-127">또는 url hello를 사용 하 여 직접 hello 대시보드를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="a9dab-128">메시지가 표시 되 면 hello 관리자 사용자 이름 및 hello 클러스터를 프로 비전 할 때 사용한 암호를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="a9dab-129">열리면 hello 웹 페이지에서 클릭 hello **시작 갤러리** 탭 hello 아래에서 **샘플 데이터를 사용 하 여 솔루션** 범주를 hello 클릭 **웹 로그 분석** 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="a9dab-130">Hello 웹 페이지 toofinish hello 샘플에서 제공 하는 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9dab-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9dab-131">Next steps</span></span>
<span data-ttu-id="a9dab-132">다음 예제는 hello 시도: [HDInsight Hive 사용 하 여 센서 데이터를 분석](hdinsight-hive-analyze-sensor-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9dab-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
