---
title: "Azure HDInsight Hive 테이블의 데이터를 aaaSample | Microsoft Docs"
description: "Azure HDInsight(Hadopop) Hive 테이블에서 데이터 다운 샘플링"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="4d5cc-103">Azure HDInsight Hive 테이블에서 데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="4d5cc-104">이 문서에서는 하이브 쿼리를 사용 하 여 Azure HDInsight Hive 테이블에 저장 된 방법을 toodown 샘플 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="4d5cc-105">일반적으로 사용되는 세 가지 샘플링 방법인</span><span class="sxs-lookup"><span data-stu-id="4d5cc-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="4d5cc-106">균일한 무작위 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-106">Uniform random sampling</span></span>
* <span data-ttu-id="4d5cc-107">그룹별 무작위 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-107">Random sampling by groups</span></span>
* <span data-ttu-id="4d5cc-108">계층화된 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-108">Stratified sampling</span></span>

<span data-ttu-id="4d5cc-109">hello 다음 **메뉴** tootopics 설명 하는 연결 방법을 다양 한 저장소 환경에서 toosample 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="4d5cc-110">**데이터를 샘플링하는 이유**</span><span class="sxs-lookup"><span data-stu-id="4d5cc-110">**Why sample your data?**</span></span>
<span data-ttu-id="4d5cc-111">Tooanalyze 계획 hello 데이터 집합이 크면 경우 일반적으로 좋습니다 toodown 샘플 hello 데이터 tooreduce 것 tooa 있지만 대표 작고 더 관리 가능한 수치로 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="4d5cc-112">그러면 데이터 이해, 탐색 및 기능 엔지니어링이 용이해집니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="4d5cc-113">Hello 팀 데이터 과학 프로세스에서에서 해당 역할에는 데이터 처리 함수 hello 및 기계 학습 모델의 tooenable 빠르게 프로토타입을 만들입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="4d5cc-114">이 샘플링 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="4d5cc-115">어떻게 toosubmit 하이브 쿼리</span><span class="sxs-lookup"><span data-stu-id="4d5cc-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="4d5cc-116">Hello Hadoop 클러스터의 헤드 노드 hello hello Hadoop 명령줄 콘솔에서 하이브 쿼리를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="4d5cc-117">hello Hadoop 클러스터의 헤드 노드 hello에 로그인이 열고 toodo Hadoop 명령줄 콘솔 hello 및 여기에서 hello 하이브 쿼리를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="4d5cc-118">Hello Hadoop 명령줄 콘솔에서 하이브 쿼리를 제출 지침은 [어떻게 tooSubmit Hive 쿼리](machine-learning-data-science-move-hive-tables.md#submit)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="4d5cc-119"><a name="uniform"></a> 균일한 무작위 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="4d5cc-120">균일 한 무작위 샘플링 hello 데이터 집합의 각 행의 샘플링 되 고 있는 기회를 똑같이 가지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="4d5cc-121">이 hello 내부 "select" 쿼리에서 추가 필드 rand () toohello 데이터 집합을 추가 하 여 구현할 수 있으며에서 hello 외부 "선택" 쿼리 임의 해당 필드에 해당 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="4d5cc-122">다음은 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="4d5cc-123">여기서 `<sample rate, 0-1>` hello 사용자가 원하는 toosample 레코드의 hello 비율을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="4d5cc-124"><a name="group"></a> 그룹별 무작위 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="4d5cc-125">할 샘플링 범주 데이터 시기 tooeither 포함 하거나 모든 범주 변수 일부 특정 값의 hello 인스턴스를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="4d5cc-126">"그룹별 샘플링"의 의미가 바로 이것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="4d5cc-127">예를 들어 범주 변수 "State"를 사용 하는 경우 변수가 NY, MA, CA, NJ, PA 등을 값 레코드 hello의 같은 주 수 항상 함께 있는지 여부 또는 not을 이들은 샘플링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="4d5cc-128">다음은 그룹별로 샘플링하는 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="4d5cc-129"><a name="stratified"></a>계층화된 샘플링</span><span class="sxs-lookup"><span data-stu-id="4d5cc-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="4d5cc-130">무작위 샘플링은 존중 tooa 범주 변수와 함께 가져온 hello 예제를 범주의 값이 있는 경우 hello에 층 화 샘플은 hello에서 가져온 hello 부모 채우기와 같이 동일한 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="4d5cc-131">데이터에 하위 채우기 상태도, 예: NJ 100 관찰, NY가 60 관찰,이 많고 WA 300 관찰 가정 위와 동일한 예제 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="4d5cc-132">Hello 비율을 지정 하는 경우 샘플링 toobe 0.5 층 화 다음 hello 가져온 샘플 있어야 약 50, 30 및 NJ, NY, 및 WA 150 관찰 각각 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="4d5cc-133">다음은 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="4d5cc-134">Hive에서 사용할 수 있는 고급 샘플링 방법에 대한 자세한 내용은 [LanguageManual 샘플링](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d5cc-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

