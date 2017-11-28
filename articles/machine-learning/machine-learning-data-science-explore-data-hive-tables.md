---
title: "Hive 쿼리를 사용하여 Hive 테이블의 데이터 탐색 | Microsoft Docs"
description: "Hive 쿼리를 사용하여 Hive 테이블의 데이터를 탐색합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="0170d-103">Hive 쿼리를 사용하여 Hive 테이블의 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="0170d-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="0170d-104">이 문서는 HDInsight Hadoop 클러스터의 Hive 테이블에서 데이터를 탐색하는 데 사용된 샘플 Hive 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="0170d-105">다음 **메뉴** 는 다양한 저장소 환경에서 데이터를 탐색하기 위해 도구를 사용하는 방법을 설명하는 토픽에 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="0170d-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0170d-106">Prerequisites</span></span>
<span data-ttu-id="0170d-107">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-107">This article assumes that you have:</span></span>

* <span data-ttu-id="0170d-108">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-108">Created an Azure storage account.</span></span> <span data-ttu-id="0170d-109">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0170d-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="0170d-110">사용자 지정된 Hadoop 클러스터에 HDInsight 서비스를 프로비전했습니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="0170d-111">지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0170d-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="0170d-112">Azure HDInsight Hadoop 클러스터의 Hive 테이블에 데이터가 업로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0170d-113">업로드되지 않은 경우 [데이터를 만들어서 Hive 테이블에 로드](machine-learning-data-science-move-hive-tables.md) 의 지침에 따라 먼저 Hive 테이블에 데이터를 업로드하세요.</span><span class="sxs-lookup"><span data-stu-id="0170d-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="0170d-114">클러스터에 대한 원격 액세스가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="0170d-115">지침이 필요한 경우 [Hadoop 클러스터의 헤드 노드에 액세스](machine-learning-data-science-customize-hadoop-cluster.md#headnode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0170d-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="0170d-116">Hive 쿼리를 제출하는 방법에 대한 지침이 필요한 경우 [Hive 쿼리를 제출하는 방법](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="0170d-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="0170d-117">데이터 탐색에 대한 예제 Hive 쿼리 스크립트</span><span class="sxs-lookup"><span data-stu-id="0170d-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="0170d-118">파티션당 관찰 수 가져오기 `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="0170d-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="0170d-119">일별 관찰 수 가져오기 `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="0170d-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="0170d-120">범주 열의 수준 가져오기 </span><span class="sxs-lookup"><span data-stu-id="0170d-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="0170d-121">두 범주 열 조합의 수준 수 가져오기 `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="0170d-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="0170d-122">숫자 열의 분포 가져오기 </span><span class="sxs-lookup"><span data-stu-id="0170d-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="0170d-123">두 조인 테이블의 레코드 추출</span><span class="sxs-lookup"><span data-stu-id="0170d-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="0170d-124">택시 여정 데이터 시나리오에 대한 추가 쿼리 스크립트</span><span class="sxs-lookup"><span data-stu-id="0170d-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="0170d-125">또한 [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) 시나리오에 대한 쿼리 예제가 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="0170d-126">이러한 쿼리는 이미 데이터 스키마가 지정되어 있으며 바로 제출하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0170d-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

