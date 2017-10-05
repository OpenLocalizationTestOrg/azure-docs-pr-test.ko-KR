---
title: "Hive 및 Hadoop을 사용하여 센서 데이터 분석 - Azure HDInsight | Microsoft Docs"
description: "HDInsight(Hadoop)에서 Hive 쿼리 콘솔을 사용하여 센서 데이터를 분석한 다음 Microsoft Excel에서 Power View를 사용하여 데이터를 시각화하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="db5d9-103">HDInsight의 Hadoop에서 Hive 쿼리 콘솔을 사용하여 센서 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="db5d9-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="db5d9-104">HDInsight(Hadoop)에서 Hive 쿼리 콘솔을 사용하여 센서 데이터를 분석한 다음 Microsoft Excel에서 Power View를 사용하여 데이터를 시각화하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db5d9-105">이 문서의 단계는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="db5d9-106">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="db5d9-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="db5d9-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5d9-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="db5d9-109">이 샘플에서는 Hive를 사용하여 기록 데이터를 처리하고 온방 및 냉방 시스템의 문제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="db5d9-110">특히 다음 작업을 실행하여 시스템이 설정된 온도를 안정적으로 유지할 수 없음을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="db5d9-111">HIVE 테이블을 만들어 CSV(쉼표로 구분된 값) 파일에 저장된 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="db5d9-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="db5d9-112">HIVE 쿼리를 만들어 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="db5d9-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="db5d9-113">Microsoft Excel로 HDInsight에 연결하여 분석된 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="db5d9-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="db5d9-114">Power View를 사용하여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="db5d9-114">To visualize the data, use Power View.</span></span>

![솔루션 아키텍처 다이어그램](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="db5d9-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db5d9-116">Prerequisites</span></span>

* <span data-ttu-id="db5d9-117">HDInsight(Hadoop) 클러스터: 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db5d9-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="db5d9-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="db5d9-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="db5d9-119">Microsoft Excel은 [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US)를 통한 데이터 시각화에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="db5d9-120">Microsoft Hive ODBC 드라이버</span><span class="sxs-lookup"><span data-stu-id="db5d9-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="db5d9-121">샘플을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="db5d9-121">To run the sample</span></span>

1. <span data-ttu-id="db5d9-122">웹 브라우저에서 다음 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="db5d9-123">`<clustername>` 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="db5d9-124">메시지가 표시되면 이 클러스터를 프로비전할 때 사용한 관리자 사용자 이름과 암호를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="db5d9-125">웹 페이지가 열리면 **시작 갤러리** 탭을 클릭하고 **샘플 데이터가 있는 솔루션** 범주에서**센서 데이터 분석** 샘플을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![갤러리 이미지 시작하기](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="db5d9-127">웹 페이지에서 제공되는 지침에 따라 샘플을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="db5d9-127">Follow the instructions provided on the web page to finish the sample.</span></span>
