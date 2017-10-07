---
title: "하이브 쿼리를 사용 하 여 Hadoop 클러스터에는 데이터에 대 한 aaaCreate 기능 | Microsoft Docs"
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
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="50ebf-103">Hive 쿼리를 사용하여 Hadoop 클러스터의 데이터에 대한 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="50ebf-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="50ebf-104">이 문서에서는 toocreate 기능 데이터에 대 한 하이브 쿼리를 사용 하 여 Azure HDInsight Hadoop 클러스터에 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-104">This document shows how toocreate features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="50ebf-105">포함 된 하이브 사용자 정의 함수 (Udf)를 사용 하는 이러한 하이브 쿼리를 hello 스크립트 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-105">These Hive queries use embedded Hive User Defined Functions (UDFs), hello scripts for which are provided.</span></span>

<span data-ttu-id="50ebf-106">hello 필요한 작업 toocreate 기능이 메모리를 많이 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-106">hello operations needed toocreate features can be memory intensive.</span></span> <span data-ttu-id="50ebf-107">하이브 쿼리 성능을 hello 이러한 경우에 특히 중요 한 되며 특정 매개 변수를 조정 하 여 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-107">hello performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="50ebf-108">이러한 매개 변수 중 hello 튜닝 hello 마지막 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-108">hello tuning of these parameters is discussed in hello final section.</span></span>

<span data-ttu-id="50ebf-109">표시 되는 hello 쿼리의 예는 특정 toohello [NYC 택시 여행 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) 시나리오에도 제공 되어 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-109">Examples of hello queries that are presented are specific toohello [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="50ebf-110">이러한 쿼리 이미 지정 된 데이터 스키마 않으며 제출 준비 toobe toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-110">These queries already have data schema specified and are ready toobe submitted toorun.</span></span> <span data-ttu-id="50ebf-111">Hello 마지막 섹션에서 하이브 쿼리 hello 성능을 향상 시킬 수 있도록 사용자가 튜닝할 수 있는 매개 변수 에서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-111">In hello final section, parameters that users can tune so that hello performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="50ebf-112">이 **메뉴** tootopics toocreate 다양 한 환경에서 데이터에 대 한 기능 하는 방법을 설명 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-112">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="50ebf-113">이 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-113">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50ebf-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="50ebf-114">Prerequisites</span></span>
<span data-ttu-id="50ebf-115">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-115">This article assumes that you have:</span></span>

* <span data-ttu-id="50ebf-116">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-116">Created an Azure storage account.</span></span> <span data-ttu-id="50ebf-117">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50ebf-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="50ebf-118">Hello HDInsight 서비스를 사용 하 여 사용자 지정 된 Hadoop 클러스터 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-118">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="50ebf-119">지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50ebf-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="50ebf-120">hello 데이터가 Azure HDInsight Hadoop 클러스터에서 업로드 된 tooHive 테이블 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-120">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="50ebf-121">그렇지 않은 경우 따르십시오 [데이터 tooHive 테이블을 만들고 부하](machine-learning-data-science-move-hive-tables.md) tooupload 데이터 tooHive 먼저 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-121">If it has not, please follow [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="50ebf-122">원격 액세스 toohello 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-122">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="50ebf-123">지침이 필요한 경우 참조 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-123">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="50ebf-124"><a name="hive-featureengineering"></a>기능 생성</span><span class="sxs-lookup"><span data-stu-id="50ebf-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="50ebf-125">이 섹션에 있는 기능 수 생성 하이브 쿼리를 사용 하 여 hello 방법의 몇 가지 예가 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-125">In this section, several examples of hello ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="50ebf-126">추가 기능을 생성 한 후 toohello 기존 테이블 열으로 추가 하거나 hello 추가 기능 및 hello 원래 테이블과 조인할 수 있는 기본 키를 사용 하 여 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-126">Once you have generated additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, which can then be joined with hello original table.</span></span> <span data-ttu-id="50ebf-127">에 소개 된 hello 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-127">Here are hello examples presented:</span></span>

1. [<span data-ttu-id="50ebf-128">빈도 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="50ebf-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="50ebf-129">이진 분류에서 범주 변수의 위험</span><span class="sxs-lookup"><span data-stu-id="50ebf-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="50ebf-130">날짜/시간 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="50ebf-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="50ebf-131">텍스트 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="50ebf-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="50ebf-132">GPS 좌표 사이의 거리 계산</span><span class="sxs-lookup"><span data-stu-id="50ebf-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="50ebf-133"><a name="hive-frequencyfeature"></a>빈도 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="50ebf-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="50ebf-134">것이 유용한 toocalculate hello 주파수 범주 변수의 hello 수준 또는 수준 여러 범주 변수에서의 특정 조합은의 hello 빈도.</span><span class="sxs-lookup"><span data-stu-id="50ebf-134">It is often useful toocalculate hello frequencies of hello levels of a categorical variable, or hello frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="50ebf-135">사용자 이러한 주파수 스크립트 toocalculate 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-135">Users can use hello following script toocalculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="50ebf-136"><a name="hive-riskfeature"></a>이진 분류에서 범주 변수의 위험</span><span class="sxs-lookup"><span data-stu-id="50ebf-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="50ebf-137">이진 분류에 hello 모델에만 사용 되 고 숫자 기능을 수행 하는 경우 숫자 기능으로 tooconvert 숫자가 아닌 범주 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-137">In binary classification, we need tooconvert non-numeric categorical variables into numeric features when hello models being used only take numeric features.</span></span> <span data-ttu-id="50ebf-138">그러려면 숫자가 아닌 각 수준을 숫자 위험으로 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="50ebf-139">이 섹션에서는 범주 변수 hello 위험 값 (로그 확률)을 계산 하는 일부 제네릭 하이브 쿼리를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-139">In this section, we show some generic Hive queries that calculate hello risk values (log odds) of a categorical variable.</span></span>

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

<span data-ttu-id="50ebf-140">이 예에서는 변수 `smooth_param1` 및 `smooth_param2` hello 데이터에서 계산 된 toosmooth hello 위험 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-140">In this example, variables `smooth_param1` and `smooth_param2` are set toosmooth hello risk values calculated from hello data.</span></span> <span data-ttu-id="50ebf-141">위험 범위는 -Inf~Inf입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="50ebf-142">위험 > 0 hello 대상으로 하는 같은 too1 hello 확률 0.5 보다 큰 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-142">A risks > 0 indicates that hello probability that hello target is equal too1 is greater than 0.5.</span></span>

<span data-ttu-id="50ebf-143">Hello 위험 테이블이 계산 된 후 hello 위험 테이블과 조인 하 여 위험 tooa 표를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-143">After hello risk table is calculated, users can assign risk values tooa table by joining it with hello risk table.</span></span> <span data-ttu-id="50ebf-144">hello 하이브 조인 쿼리는 이전 섹션에서 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-144">hello Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="50ebf-145"><a name="hive-datefeatures"></a>날짜/시간 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="50ebf-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="50ebf-146">Hive는 날짜/시간 필드를 처리할 수 있는 UDF가 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="50ebf-147">하이브에, hello 기본 날짜/시간 형식은 ' yyyy-월-일 00시: 00' ('1970-01-01 12시 21분: 32' 예를 들어).</span><span class="sxs-lookup"><span data-stu-id="50ebf-147">In Hive, hello default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="50ebf-148">이 섹션에서는 hello 일, 월, 날짜/시간 필드에서 hello 월을 추출 하는 예제 및 hello 기본 형식 tooa datetime 문자열 기본 형식 이외의 형식으로 날짜/시간 문자열을 변환 하는 다른 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-148">In this section, we show examples that extract hello day of a month, hello month from a datetime field, and other examples that convert a datetime string in a format other than hello default format tooa datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="50ebf-149">이 하이브 쿼리 가정 해당 hello *&#60; datetime 필드 >* hello 기본 날짜/시간 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-149">This Hive query assumes that hello *&#60;datetime field>* is in hello default datetime format.</span></span>

<span data-ttu-id="50ebf-150">날짜/시간 필드가 hello 기본 형식에 없으면, 해야 tooconvert hello datetime 필드 Unix 타임 스탬프에 먼저, 다음 convert hello Unix 시간 스탬프 tooa datetime 문자열에 있고 hello 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-150">If a datetime field is not in hello default format, you need tooconvert hello datetime field into Unix time stamp first, and then convert hello Unix time stamp tooa datetime string that is in hello default format.</span></span> <span data-ttu-id="50ebf-151">Hello 날짜/시간 형식 기본 이면 hello 포함 된 datetime Udf tooextract 기능 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-151">When hello datetime is in default format, users can apply hello embedded datetime UDFs tooextract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="50ebf-152">이 쿼리에서 경우 hello *&#60; datetime 필드 >* 같은 hello 패턴이 *03/26/2015 12시 04분: 39*, hello *' &#60; hello 날짜/시간 필드의 패턴 >'* 이어야 합니다 `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="50ebf-152">In this query, if hello *&#60;datetime field>* has hello pattern like *03/26/2015 12:04:39*, hello *'&#60;pattern of hello datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="50ebf-153">tootest 사용자가 실행할 수</span><span class="sxs-lookup"><span data-stu-id="50ebf-153">tootest it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="50ebf-154">hello *hivesampletable* 이 쿼리의 미리 설치 된 모든 Azure HDInsight Hadoop 클러스터에서 기본적으로 때 도착 hello 클러스터 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-154">hello *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when hello clusters are provisioned.</span></span>

### <span data-ttu-id="50ebf-155"><a name="hive-textfeatures"></a>텍스트 필드에서 기능 추출</span><span class="sxs-lookup"><span data-stu-id="50ebf-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="50ebf-156">Hello Hive 테이블에 공백으로 구분 되는 단어의 문자열이 포함 된 텍스트 필드가 hello 다음 쿼리를 추출 hello 길이 hello 문자열 및 hello 문자열에서 단어 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-156">When hello Hive table has a text field that contains a string of words that are delimited by spaces, hello following query extracts hello length of hello string, and hello number of words in hello string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="50ebf-157"><a name="hive-gpsdistance"></a>GPS 좌표 사이의 거리 계산</span><span class="sxs-lookup"><span data-stu-id="50ebf-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="50ebf-158">이 섹션에 지정 된 hello 쿼리 직접 적용 된 toohello NYC 택시 여행 데이터 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-158">hello query given in this section can be directly applied toohello NYC Taxi Trip Data.</span></span> <span data-ttu-id="50ebf-159">hello이이 쿼리는 tooshow 어떻게 tooapply 포함 된 하이브 toogenerate 기능의 수치 연산 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-159">hello purpose of this query is tooshow how tooapply an embedded mathematical functions in Hive toogenerate features.</span></span>

<span data-ttu-id="50ebf-160">hello이 쿼리에 사용 되는 필드는 명명 된 픽업 및 dropoff 위치 hello GPS 좌표 *픽업\_경도*, *픽업\_위도*,  *dropoff\_경도*, 및 *dropoff\_위도*합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-160">hello fields that are used in this query are hello GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="50ebf-161">hello 픽업 및 dropoff 좌표 간의 hello 직접 거리를 계산 하는 hello 쿼리가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-161">hello queries that calculate hello direct distance between hello pickup and dropoff coordinates are:</span></span>

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

<span data-ttu-id="50ebf-162">hello에 두 GPS 좌표 사이의 hello 거리를 계산 하는 hello 수식이 있습니다 <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">이동 유형 스크립트</a> Peter Lapisu가 만든 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-162">hello mathematical equations that calculate hello distance between two GPS coordinates can be found on hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="50ebf-163">그의 javascript 함수 hello `toRad()` 단지 *lat_or_lon*pi/180 *도 tooradians로 변환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-163">In his Javascript, hello function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees tooradians.</span></span> <span data-ttu-id="50ebf-164">여기에서 *lat_or_lon* hello 위도 또는 경도의 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-164">Here, *lat_or_lon* is hello latitude or longitude.</span></span> <span data-ttu-id="50ebf-165">하이브 hello 함수를 제공 하지 않는 `atan2`, hello 함수를 제공 하지만 `atan`, hello `atan2` 함수를 구현 하 여 `atan` 함수에 제공 된 hello 정의 사용 하는 하이브 쿼리 위에 hello에 <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-165">Since Hive does not provide hello function `atan2`, but provides hello function `atan`, hello `atan2` function is implemented by `atan` function in hello above Hive query using hello definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="50ebf-167">Hello에 포함 된 Udf 있습니다 하이브의 전체 목록은 **기본 제공 함수** hello 섹션 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span><span class="sxs-lookup"><span data-stu-id="50ebf-167">A full list of Hive embedded UDFs can be found in hello **Built-in Functions** section on hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="50ebf-168"><a name="tuning"></a>고급 항목: 하이브 매개 변수 조정 tooImprove 쿼리 속도</span><span class="sxs-lookup"><span data-stu-id="50ebf-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters tooImprove Query Speed</span></span>
<span data-ttu-id="50ebf-169">hello 하이브 클러스터의 설정을 맞지 않을 hello 하이브 쿼리 및 처리 하는 hello 쿼리 hello 데이터에 대 한 기본 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-169">hello default parameter settings of Hive cluster might not be suitable for hello Hive queries and hello data that hello queries are processing.</span></span> <span data-ttu-id="50ebf-170">이 섹션에서는 hello 하이브 쿼리 성능을 개선 하는 사용자가 조정할 수 있는 몇 가지 매개에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-170">In this section, we discuss some parameters that users can tune that improve hello performance of Hive queries.</span></span> <span data-ttu-id="50ebf-171">사용자는 hello 쿼리 데이터를 처리 하기 전에 쿼리를 튜닝 tooadd hello 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-171">Users need tooadd hello parameter tuning queries before hello queries of processing data.</span></span>

1. <span data-ttu-id="50ebf-172">**Java의 힙 공간이**: 큰 데이터 집합 조인 또는 긴 레코드를 처리 하는 쿼리에 대해 **힙 공간이 부족** hello에서 발생 하는 일반적인 오류 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of hello common error.</span></span> <span data-ttu-id="50ebf-173">이 매개 변수를 설정 하 여 튜닝할 수 *mapreduce.map.java.opts* 및 *mapreduce.task.io.sort.mb* toodesired 값입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* toodesired values.</span></span> <span data-ttu-id="50ebf-174">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="50ebf-175">이 매개 변수 4GB 메모리 tooJava 힙 공간을 할당 하 고 또한 하면 정렬 보다 효율적으로 더 많은 메모리를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-175">This parameter allocates 4GB memory tooJava heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="50ebf-176">이러한 할당이 포함 된 것이 좋습니다 tooplay는 하는 경우에 포함 된 작업 실패 오류 관련된 tooheap 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-176">It is a good idea tooplay with these allocations if there are any job failure errors related tooheap space.</span></span>

1. <span data-ttu-id="50ebf-177">**DFS 블록 크기** :이 매개 변수는 hello hello 파일 시스템 저장소는 데이터의 가장 작은 단위를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-177">**DFS block size** : This parameter sets hello smallest unit of data that hello file system stores.</span></span> <span data-ttu-id="50ebf-178">예를 들어 hello DFS 블록 크기는 128mb로, 않으면 크기의 모든 데이터 미만 및 too128MB 드릴업은 저장 하는 동안 추가 블록 할당 128MB 보다 큰 데이터는 단일 블록에서입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-178">As an example, if hello DFS block size is 128MB, then any data of size less than and up too128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="50ebf-179">Hello 이름 노드에서 tooprocess 많은 더 많은 요청 toofind hello 관련 블록 toohello 파일 관련 되어 있으므로 Hadoop에서 큰 오버 헤드가 발생 매우 작은 블록 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-179">Choosing a very small block size causes large overheads in Hadoop since hello name node has tooprocess many more requests toofind hello relevant block pertaining toohello file.</span></span> <span data-ttu-id="50ebf-180">기가바이트 단위(또는 그 이상) 데이터를 처리할 때 권장하는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="50ebf-181">**하이브 join 연산의 최적화** : hello 맵/감소 프레임 워크에서 조인 작업 hello에서 일반적으로 수행 하는 동안 경우에 따라 단계를 줄이려면, 조인 hello 매핑 단계 ("mapjoins" 라고도 함)에 예약 하 여 엄청난 향상이 이루어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-181">**Optimizing join operation in Hive** : While join operations in hello map/reduce framework typically take place in hello reduce phase, sometimes, enormous gains can be achieved by scheduling joins in hello map phase (also called "mapjoins").</span></span> <span data-ttu-id="50ebf-182">toodirect 하이브 toodo이 가능 하다 면 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-182">toodirect Hive toodo this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="50ebf-183">**매퍼 tooHive hello 개수를 지정 하면** : 동안 Hadoop hello 사용자 tooset hello의 허용 이경소켓, 매퍼 hello 수는 대개 hello 사용자가 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-183">**Specifying hello number of mappers tooHive** : While Hadoop allows hello user tooset hello number of reducers, hello number of mappers is typically not be set by hello user.</span></span> <span data-ttu-id="50ebf-184">이 숫자에는 컨트롤의 어느 정도 허용 하는 트릭은 toochoose hello Hadoop 변수 *mapred.min.split.size* 및 *mapred.max.split.size* 각 맵의 hello 크기와 작업에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-184">A trick that allows some degree of control on this number is toochoose hello Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as hello size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="50ebf-185">기본값을 일반적으로 hello *mapred.min.split.size* 은 0으로의 *mapred.max.split.size* 은 **Long.MAX** 요구 사항과 *dfs.block.size* 는 64MB입니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-185">Typically, hello default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="50ebf-186">볼 수 있듯이, 주어진된 hello 데이터 크기 "설정" 하 여 이러한 매개 변수를 튜닝을 통해 tootune hello 수가 매퍼 사용 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-186">As we can see, given hello data size, tuning these parameters by "setting" them allows us tootune hello number of mappers used.</span></span>
4. <span data-ttu-id="50ebf-187">아래에 Hive 성능을 최적화하는 **고급 옵션** 몇 가지가 추가로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="50ebf-188">이러한 tooset hello 할당 된 메모리 toomap를 허용 하 고 작업을 줄여 및 작업은 성능 조정 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-188">These allow you tooset hello memory allocated toomap and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="50ebf-189">명심 하십시오 해당 hello *mapreduce.reduce.memory.mb* hello Hadoop 클러스터의 각 작업자 노드의 hello 실제 메모리 크기 보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50ebf-189">Please keep in mind that hello *mapreduce.reduce.memory.mb* cannot be greater than hello physical memory size of each worker node in hello Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

