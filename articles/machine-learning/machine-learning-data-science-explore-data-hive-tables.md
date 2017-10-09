---
title: "하이브 쿼리 인 하이브 테이블에서 데이터 aaaExplore | Microsoft Docs"
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
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="3492e-103">Hive 쿼리를 사용하여 Hive 테이블의 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="3492e-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="3492e-104">이 문서는 HDInsight Hadoop 클러스터의 Hive 테이블에 사용 되는 tooexplore 데이터 예제 하이브 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="3492e-105">hello 다음 **메뉴** tootopics toouse 도구 tooexplore 데이터 저장소, 다양 한 환경에서 하는 방법을 설명 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="3492e-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3492e-106">Prerequisites</span></span>
<span data-ttu-id="3492e-107">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-107">This article assumes that you have:</span></span>

* <span data-ttu-id="3492e-108">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-108">Created an Azure storage account.</span></span> <span data-ttu-id="3492e-109">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3492e-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="3492e-110">Hello HDInsight 서비스를 사용 하 여 사용자 지정 된 Hadoop 클러스터 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="3492e-111">지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3492e-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="3492e-112">hello 데이터가 Azure HDInsight Hadoop 클러스터에서 업로드 된 tooHive 테이블 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="3492e-113">그렇지 않은 경우 hello 지침에 따라 [데이터 tooHive 테이블을 만들고 부하](machine-learning-data-science-move-hive-tables.md) tooupload 데이터 tooHive 먼저 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="3492e-114">원격 액세스 toohello 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="3492e-115">지침이 필요한 경우 참조 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="3492e-116">방법에 대 한 지침이 필요한 경우 toosubmit 하이브 쿼리에서 참조 [어떻게 tooSubmit 하이브 쿼리](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="3492e-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="3492e-117">데이터 탐색에 대한 예제 Hive 쿼리 스크립트</span><span class="sxs-lookup"><span data-stu-id="3492e-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="3492e-118">파티션당 관찰 hello 개수`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="3492e-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="3492e-119">하루 관찰 hello 개수`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="3492e-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="3492e-120">범주 열에서 hello 수준을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="3492e-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="3492e-121">두 개의 범주 열 조합에 수준의 hello 수 가져오기`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="3492e-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="3492e-122">숫자 열에 대 한 hello 분포 가져오기</span><span class="sxs-lookup"><span data-stu-id="3492e-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="3492e-123">두 조인 테이블의 레코드 추출</span><span class="sxs-lookup"><span data-stu-id="3492e-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="3492e-124">택시 여정 데이터 시나리오에 대한 추가 쿼리 스크립트</span><span class="sxs-lookup"><span data-stu-id="3492e-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="3492e-125">너무 관련 된 쿼리 예제[NYC 택시 여행 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) 시나리오에도 제공 되어 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="3492e-126">이러한 쿼리 이미 지정 된 데이터 스키마 않으며 제출 준비 toobe toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="3492e-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

