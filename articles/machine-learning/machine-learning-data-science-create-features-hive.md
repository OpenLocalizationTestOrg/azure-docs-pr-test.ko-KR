---
title: "Hive 쿼리를 사용하여 Hadoop 클러스터의 데이터에 대한 기능 만들기 | Microsoft Docs"
description: "Azure HDInsight Hadoop 클러스터에 저장된 데이터의 기능을 생성하는 Hive 쿼리의 예입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e027a6ffcb63868be13432870e484c5cbf2eef4b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="4e32b-103">Hive 쿼리를 사용하여 Hadoop 클러스터의 데이터에 대한 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="4e32b-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="4e32b-104">이 문서에는 Hive 쿼리를 사용하여 Azure HDInsight Hadoop 클러스터에 저장된 데이터에 대한 기능을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="4e32b-105">이러한 Hive 쿼리는 제공된 스크립트인 포함된 Hive UDF(사용자 정의 함수)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-105">These Hive queries use embedded Hive User Defined Functions (UDFs), the scripts for which are provided.</span></span>

<span data-ttu-id="4e32b-106">기능을 만드는 데 필요한 작업은 메모리 집약적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-106">The operations needed to create features can be memory intensive.</span></span> <span data-ttu-id="4e32b-107">이 경우 Hive 쿼리의 성능이 더욱 중요해지며 특정 매개 변수를 조정하여 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="4e32b-108">이러한 매개 변수를 조정하는 내용은 마지막 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-108">The tuning of these parameters is discussed in the final section.</span></span>

<span data-ttu-id="4e32b-109">또한 [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) 시나리오에 대해 제공되는 쿼리 예제가 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)에도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="4e32b-110">이러한 쿼리는 이미 데이터 스키마가 지정되어 있으며 바로 제출하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-110">These queries already have data schema specified and are ready to be submitted to run.</span></span> <span data-ttu-id="4e32b-111">마지막 섹션에서는 사용자가 조정하여 Hive 쿼리 성능을 높일 수 있는 매개 변수에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="4e32b-112">이 **메뉴** 는 다양한 환경에서 데이터에 대한 기능을 만드는 방법을 설명하는 토픽으로 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-112">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="4e32b-113">이 작업은 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e32b-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4e32b-114">Prerequisites</span></span>
<span data-ttu-id="4e32b-115">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-115">This article assumes that you have:</span></span>

* <span data-ttu-id="4e32b-116">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-116">Created an Azure storage account.</span></span> <span data-ttu-id="4e32b-117">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e32b-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="4e32b-118">사용자 지정된 Hadoop 클러스터에 HDInsight 서비스를 프로비전했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="4e32b-119">지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e32b-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="4e32b-120">Azure HDInsight Hadoop 클러스터의 Hive 테이블에 데이터가 업로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="4e32b-121">업로드되지 않은 경우 [데이터를 만들어서 Hive 테이블에 로드](machine-learning-data-science-move-hive-tables.md) 의 지침에 따라 먼저 Hive 테이블에 데이터를 업로드하세요.</span><span class="sxs-lookup"><span data-stu-id="4e32b-121">If it has not, please follow [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="4e32b-122">클러스터에 대한 원격 액세스가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-122">Enabled remote access to the cluster.</span></span> <span data-ttu-id="4e32b-123">지침이 필요한 경우 [Hadoop 클러스터의 헤드 노드에 액세스](machine-learning-data-science-customize-hadoop-cluster.md#headnode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e32b-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="4e32b-124"><a name="hive-featureengineering"></a>기능 생성</span><span class="sxs-lookup"><span data-stu-id="4e32b-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="4e32b-125">이 섹션에서는 Hive 쿼리를 사용하여 기능을 생성할 수 있는 방법의 몇 가지 예를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="4e32b-126">추가 기능을 생성한 후 기존 테이블에 열로 추가하거나 추가 기능 및 기본 키를 사용하여 새 테이블을 만들어서 원래 테이블과 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span></span> <span data-ttu-id="4e32b-127">제시된 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-127">Here are the examples presented:</span></span>

1. [<span data-ttu-id="4e32b-128">빈도 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="4e32b-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="4e32b-129">이진 분류에서 범주 변수의 위험</span><span class="sxs-lookup"><span data-stu-id="4e32b-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="4e32b-130">날짜/시간 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="4e32b-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="4e32b-131">텍스트 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="4e32b-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="4e32b-132">GPS 좌표 사이의 거리 계산</span><span class="sxs-lookup"><span data-stu-id="4e32b-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="4e32b-133"><a name="hive-frequencyfeature"></a>빈도 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="4e32b-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="4e32b-134">범주 변수의 빈도 수준 또는 여러 범주 변수로 구성된 특정 조합의 빈도 수준을 계산하는 것이 매우 유용한 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="4e32b-135">사용자는 다음 스크립트를 사용하여 빈도를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-135">Users can use the following script to calculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="4e32b-136"><a name="hive-riskfeature"></a>이진 분류에서 범주 변수의 위험</span><span class="sxs-lookup"><span data-stu-id="4e32b-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="4e32b-137">사용하는 모델에 숫자 기능만 허용되는 경우 이진 분류에서 숫자가 아닌 범주 변수를 숫자 기능으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-137">In binary classification, we need to convert non-numeric categorical variables into numeric features when the models being used only take numeric features.</span></span> <span data-ttu-id="4e32b-138">그러려면 숫자가 아닌 각 수준을 숫자 위험으로 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="4e32b-139">이 섹션에서는 범주 변수의 위험 값(로그 odd)을 계산하는 일반 Hive 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-139">In this section, we show some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="4e32b-140">이 예에서, 변수 `smooth_param1` 및 `smooth_param2`는 데이터에서 계산된 위험 값을 완화하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span></span> <span data-ttu-id="4e32b-141">위험 범위는 -Inf~Inf입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="4e32b-142">위험>0은 대상이 1일 확률이 0.5보다 크다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-142">A risks > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span></span>

<span data-ttu-id="4e32b-143">위험 테이블이 계산되면 사용자는 위험 값을 위험 테이블에 조인하여 위험 값을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span></span> <span data-ttu-id="4e32b-144">Hive 조인 쿼리는 이전 섹션에서 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-144">The Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="4e32b-145"><a name="hive-datefeatures"></a>날짜/시간 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="4e32b-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="4e32b-146">Hive는 날짜/시간 필드를 처리할 수 있는 UDF가 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="4e32b-147">Hive의 기본 날짜/시간 형식은 'yyyy-MM-dd 00:00:00'입니다(예: '1970-01-01 12:21:32').</span><span class="sxs-lookup"><span data-stu-id="4e32b-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="4e32b-148">이 섹션에서는 날짜/시간 필드에서 일 및 월을 추출하는 예제와 기본 형식이 아닌 다른 형식으로 된 날짜/시간 문자열을 기본 형식의 날짜/시간 문자열로 변환하는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-148">In this section, we show examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="4e32b-149">이 Hive 쿼리에서는 *&#60;datetime field>*가 기본 날짜/시간 형식으로 되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-149">This Hive query assumes that the *&#60;datetime field>* is in the default datetime format.</span></span>

<span data-ttu-id="4e32b-150">날짜/시간 필드가 기본 형식이 아닌 경우 먼저 날짜/시간 필드를 Unix 타임스탬프로 변환한 후 Unix 타임스탬프를 기본 형식의 날짜/시간 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span></span> <span data-ttu-id="4e32b-151">날짜/시간이 기본 형식으로 변환되면 포함된 날짜/시간 UDF를 적용하여 기능을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of the datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="4e32b-152">이 쿼리에서 *&#60;datetime field>*의 패턴이 *03/26/2015 12:04:39*와 같다면 *'&#60;pattern of the datetime field>'*는 `'MM/dd/yyyy HH:mm:ss'`입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-152">In this query, if the *&#60;datetime field>* has the pattern like *03/26/2015 12:04:39*, the *'&#60;pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="4e32b-153">이를 테스트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-153">To test it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="4e32b-154">이 쿼리에서 *hivesampletable* 은 기본적으로 클러스터가 프로비전될 때 모든 Azure HDInsight Hadoop 클러스터에 미리 설치된 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span></span>

### <span data-ttu-id="4e32b-155"><a name="hive-textfeatures"></a>텍스트 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="4e32b-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="4e32b-156">Hive 테이블에 텍스트 필드가 있고 이 텍스트 필드에 공백으로 구분된 단어 문자열이 포함되어 있으면 다음 쿼리는 문자열의 길이와 문자열에 포함된 단어 수를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="4e32b-157"><a name="hive-gpsdistance"></a>GPS 좌표 사이의 거리 계산</span><span class="sxs-lookup"><span data-stu-id="4e32b-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="4e32b-158">이 섹션에 제공된 쿼리를 뉴욕시 택시 여행 데이터에 바로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span></span> <span data-ttu-id="4e32b-159">Hive에 포함된 수학 함수를 적용하여 기능을 생성하는 방법을 보여 주는 것이 이 쿼리의 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-159">The purpose of this query is to show how to apply an embedded mathematical functions in Hive to generate features.</span></span>

<span data-ttu-id="4e32b-160">이 쿼리에 사용된 필드는 승차 위치와 하차 위치의 GPS 좌표이며 이름은 *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude* 및 *dropoff\_latitude*입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="4e32b-161">태우는 좌표와 내리는 좌표 사이의 직접 거리를 계산하는 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="4e32b-162">두 GPS 좌표 사이의 거리를 계산하는 수학 방정식은 <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> 사이트에서 찾을 수 있으며, 작성자는 Peter Lapisu입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="4e32b-163">그의 Javascript에서 `toRad()` 함수는 단지 도에서 라디안으로 변환하는 *lat_or_lon*pi/180*일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-163">In his Javascript, the function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees to radians.</span></span> <span data-ttu-id="4e32b-164">여기서 *lat_or_lon*은 위도 또는 경도입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-164">Here, *lat_or_lon* is the latitude or longitude.</span></span> <span data-ttu-id="4e32b-165">Hive에서 `atan2` 함수를 제공하지 않고 `atan` 함수를 제공하므로 위의 Hive 쿼리에서는 <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>에서 제공하는 정의를 사용하여 `atan` 함수가 `atan2` 함수를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="4e32b-167">Hive에 포함된 UDF 전체 목록은 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>의 **기본 제공 함수** 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="4e32b-168"><a name="tuning"></a> 고급 항목: Hive 매개 변수를 조정하여 쿼리 속도 개선</span><span class="sxs-lookup"><span data-stu-id="4e32b-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters to Improve Query Speed</span></span>
<span data-ttu-id="4e32b-169">Hive 클러스터의 기본 매개 변수 설정이 Hive 쿼리 및 쿼리에서 처리하는 데이터에 적합하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span></span> <span data-ttu-id="4e32b-170">이 섹션에서는 사용자가 조정하여 Hive 쿼리 성능을 개선할 수 있는 일부 매개 변수에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-170">In this section, we discuss some parameters that users can tune that improve the performance of Hive queries.</span></span> <span data-ttu-id="4e32b-171">사용자는 매개 변수 조정 쿼리를 먼저 추가한 후 데이터 처리 쿼리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-171">Users need to add the parameter tuning queries before the queries of processing data.</span></span>

1. <span data-ttu-id="4e32b-172">**Java 힙 공간**: 대용량 데이터 집합 조인 또는 긴 레코드 처리와 관련된 쿼리에서 가장 흔히 발생하는 오류는 **힙 공간 부족**입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common error.</span></span> <span data-ttu-id="4e32b-173">*mapreduce.map.java.opts* 및 *mapreduce.task.io.sort.mb* 매개 변수를 원하는 값으로 설정하여 이를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span></span> <span data-ttu-id="4e32b-174">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="4e32b-175">이 매개 변수는 Java 힙 공간에 4GB 메모리를 할당하고 정렬에 추가 메모리를 할당하여 정렬 작업의 효율성을 높입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="4e32b-176">힙 공간과 관련된 작업 실패 오류가 발생할 경우 이러한 할당 방법을 사용하면 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span></span>

1. <span data-ttu-id="4e32b-177">**DFS 블록 크기** : 이 매개 변수는 파일 시스템에서 저장하는 최소 데이터 단위를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-177">**DFS block size** : This parameter sets the smallest unit of data that the file system stores.</span></span> <span data-ttu-id="4e32b-178">예를 들어 DFS 블록 크기가 128MB이면 크기가 128MB 이하인 모든 데이터가 단일 블록에 저장되고 128MB보다 큰 데이터에는 추가 블록이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-178">As an example, if the DFS block size is 128MB, then any data of size less than and up to 128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="4e32b-179">블록 크기를 너무 작게 할 경우 이름 노드에서 해당 파일과 관련된 블록을 찾으려면 훨씬 많은 요청을 처리해야 하므로 Hadoop에서 큰 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-179">Choosing a very small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span></span> <span data-ttu-id="4e32b-180">기가바이트 단위(또는 그 이상) 데이터를 처리할 때 권장하는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="4e32b-181">**Hive에서 조인 작업 최적화** : 맵/감소 프레임워크의 조인 작업은 일반적으로 감소 단계에서 발생하지만 맵 단계("맵조인"이라고도 함)에서 조인 작업을 예약하여 엄청난 성과를 얻을 수 있는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-181">**Optimizing join operation in Hive** : While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span></span> <span data-ttu-id="4e32b-182">가능하면 Hive에서 이 작업을 수행하도록 하려면 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-182">To direct Hive to do this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="4e32b-183">**Hive에 대한 매퍼 수 지정**: Hadoop을 사용하면 사용자가 리듀서 수를 설정할 수 있지만 일반적으로 매퍼 수는 사용자가 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-183">**Specifying the number of mappers to Hive** : While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span></span> <span data-ttu-id="4e32b-184">한 가지 팁을 드리자면 Hadoop 변수인 *mapred.min.split.size* 및 *mapred.max.split.size*를 선택하여 매퍼 수를 어느 정도 조절할 수 있습니다. 각 맵 작업의 크기가 아래와 같은 방법으로 결정되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-184">A trick that allows some degree of control on this number is to choose the Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="4e32b-185">일반적으로 *mapred.min.split.size*의 기본값은 0, *mapred.max.split.size*의 기본값은 **Long.MAX**, *dfs.block.size*의 기본값은 64MB입니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-185">Typically, the default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="4e32b-186">보시는 것처럼 데이터 크기를 고려하려 이러한 매개 변수를 "설정"하면 사용되는 매퍼 수를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-186">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span></span>
4. <span data-ttu-id="4e32b-187">아래에 Hive 성능을 최적화하는 **고급 옵션** 몇 가지가 추가로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="4e32b-188">이러한 옵션을 사용하여 맵 및 감소 작업에 할당된 메모리를 설정할 수 있으며 성능 조정 시 유용하게 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-188">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="4e32b-189">주의할 사항으로, *mapreduce.reduce.memory.mb* 가 Hadoop 클러스터에 있는 각 작업자 노드의 실제 메모리 크기보다 크면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e32b-189">Please keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

