---
title: "Azure의 SQL Server 가상 컴퓨터에서 데이터 탐색 | Microsoft Docs"
description: "Azure의 SQL Server 가상 컴퓨터에서 데이터를 탐색하고 기능 생성"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="bd878-103"><a name="heading"></a>Azure의 SQL Server 가상 컴퓨터에서 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="bd878-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="bd878-104">이 문서에서는 Azure의 SQL Server VM에 저장된 데이터를 탐색하고 데이터에 대한 기능을 생성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="bd878-105">이렇게 하려면 SQL을 사용하여 데이터 랭글링을 수행하거나 Python과 같은 프로그래밍 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="bd878-106">이 문서의 샘플 SQL 문에서는 데이터가 SQL Server에 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="bd878-107">그렇지 않은 경우 데이터를 SQL Server로 이동하는 방법은 클라우드 데이터 과학 프로세스 맵을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd878-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="bd878-108"><a name="SQL"></a>SQL 사용</span><span class="sxs-lookup"><span data-stu-id="bd878-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="bd878-109">이 섹션에서는 SQL을 사용하여 다음과 같은 데이터 랭글링 작업을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="bd878-110">데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="bd878-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="bd878-111">기능 생성</span><span class="sxs-lookup"><span data-stu-id="bd878-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="bd878-112"><a name="sql-dataexploration"></a>데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="bd878-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="bd878-113">SQL Server에서 데이터 저장소를 탐색하는 데 사용할 수 있는 몇 가지 샘플 SQL 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="bd878-114">실용적인 예제에는 [NYC Taxi 데이터 집합](http://www.andresmh.com/nyctaxitrips/)을 사용할 수 있으며, 종단 간 연습에 [IPython Notebook 및 SQL Server를 사용한 NYC 데이터 랭글링](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)이라는 IPNB를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="bd878-115">일별 관찰 수 가져오기</span><span class="sxs-lookup"><span data-stu-id="bd878-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="bd878-116">범주 열의 수준 가져오기</span><span class="sxs-lookup"><span data-stu-id="bd878-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="bd878-117">두 범주 열 조합의 수준 수 가져오기</span><span class="sxs-lookup"><span data-stu-id="bd878-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="bd878-118">숫자 열의 분포 가져오기</span><span class="sxs-lookup"><span data-stu-id="bd878-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="bd878-119"><a name="sql-featuregen"></a>기능 생성</span><span class="sxs-lookup"><span data-stu-id="bd878-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="bd878-120">이 섹션에서는 SQL을 사용하여 기능을 생성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="bd878-121">개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="bd878-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="bd878-122">범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="bd878-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="bd878-123">단일 열에서 기능 롤아웃</span><span class="sxs-lookup"><span data-stu-id="bd878-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="bd878-124">추가 기능을 생성한 후 이를 기존 테이블에 열로 추가하거나, 추가 기능 및 기본 키를 사용하여 새 테이블을 만들어 원래 테이블에 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="bd878-125"><a name="sql-countfeature"></a>개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="bd878-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="bd878-126">다음의 예제에서는 개수 기능을 생성하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="bd878-127">첫 번째 방법에서는 조건부 합계를 사용하고, 두 번째 방법에서는 'where' 절을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="bd878-128">그런 다음 원래 데이터와 함께 개수 기능을 유지하도록 원래 테이블에 조인할 수 있습니다(기본 키 열 사용).</span><span class="sxs-lookup"><span data-stu-id="bd878-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="bd878-129"><a name="sql-binningfeature"></a>범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="bd878-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="bd878-130">다음 예제에서는 기능으로 사용할 수 있는 숫자 열을 범주화하여(다섯 개의 bin 사용) 범주화된 기능을 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="bd878-131"><a name="sql-featurerollout"></a>단일 열에서 기능 롤아웃</span><span class="sxs-lookup"><span data-stu-id="bd878-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="bd878-132">이 섹션에서는 테이블의 단일 열을 롤아웃하여 추가 기능을 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="bd878-133">이 예제에서는 기능을 생성하려는 테이블에 위도 또는 경도 열이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="bd878-134">다음은 위도/경도 위치 데이터에 대한 간략한 기초 정보입니다(stackoverflow [위도 및 경도의 정확도를 측정하는 방법](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)에서 발췌).</span><span class="sxs-lookup"><span data-stu-id="bd878-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="bd878-135">위치 필드를 기능화하기 전에 이 정보를 이해하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="bd878-136">부호는 지구에서 현재 위치의 방위(북쪽, 남쪽, 동쪽 또는 서쪽)를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="bd878-137">0이 아닌 100자리수는 위도가 아니라 경도를 사용하고 있음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="bd878-138">10자리수는 약 1,000km까지의 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="bd878-139">현재 위치의 대륙 또는 대양에 대한 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="bd878-140">단위 자리수(하나의 도 단위)는 최대 111km(60해리, 약 69마일)까지의 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="bd878-141">이는 현재 위치의 주 또는 국가를 대략적으로 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="bd878-142">첫 번째 소수 자릿수는 11.1km까지 적용되며, 하나의 대도시를 인접한 대도시와 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="bd878-143">두 번째 소수 자릿수는 1.1km까지 적용되며, 하나의 마을을 다음 마을과 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="bd878-144">세 번째 소수 자릿수는 110m까지 적용되며, 대규모 농경지 또는 기업 부지를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="bd878-145">네 번째 소수 자릿수는 11m까지 적용되며, 하나의 필지를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="bd878-146">이는 간섭 없이 보정되지 않은 GPS 장치의 일반적인 정확도에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="bd878-147">다섯 번째 소수 자릿수는 1.1m까지 적용되며, 수목을 서로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="bd878-148">상용 GPS 장치에서는 미분 보정을 통해서만 이 수준의 정확도를 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="bd878-149">여섯 번째 소수 자릿수는 0.11m까지 적용되며, 상세 구조물 배치, 조경 설계, 도로 건설 등에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="bd878-150">빙하 및 강의 이동을 추적하는 데 매우 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="bd878-151">미분 보정된 GPS와 같은 GPS로 세밀히 측정하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="bd878-152">위치 정보는 다음과 같이 지역, 위치 및 도시 정보를 구분하여 기능화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="bd878-153">또한 Bing Maps API( [지점별 위치 찾기](https://msdn.microsoft.com/library/ff701710.aspx) )와 같은 REST 끝점을 호출하여 지역/구역 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="bd878-154">이러한 위치 기반 기능을 사용하여 앞서 설명한 대로 추가 개수 기능을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="bd878-155">선택한 언어를 사용하여 프로그래밍 방식으로 레코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="bd878-156">쓰기 효율성을 개선하기 위해 청크에 데이터를 삽입해야 할 수도 있습니다. pyodbc를 사용하여 이 작업을 수행하는 방법에 대한 예제는 [Python을 사용하여 SQL Server에 액세스하는 HelloWorld 샘플](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd878-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="bd878-157">또 다른 방법은 [BCP 유틸리티](https://msdn.microsoft.com/library/ms162802.aspx)를 사용하여 데이터베이스에 데이터를 삽입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="bd878-158"><a name="sql-aml"></a>Azure 기계 학습에 연결</span><span class="sxs-lookup"><span data-stu-id="bd878-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="bd878-159">새로 생성한 기능을 기존 테이블에 열로 추가하거나, 새 테이블에 저장하여 기계 학습을 위해 원래 테이블과 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="bd878-160">Azure 기계 학습에서는 아래 표시된 대로 [데이터 가져오기][import-data] 모듈을 사용하여 기능을 생성하거나 액세스(이미 만든 경우)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml 판독기][1] 

## <span data-ttu-id="bd878-162"><a name="python"></a>Python과 같은 프로그래밍 언어 사용</span><span class="sxs-lookup"><span data-stu-id="bd878-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="bd878-163">데이터가 SQL Server에 있는 경우 Python을 사용하여 데이터를 탐색하고 기능을 생성하는 작업은 [데이터 과학 환경에서 Azure Blob 데이터 처리](machine-learning-data-science-process-data-blob.md)에 설명된 대로 Python을 사용하여 Azure Blob의 데이터를 처리하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="bd878-164">데이터베이스에서 pandas 데이터 프레임으로 데이터를 로드해야 하며, 그런 다음 데이터를 추가로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="bd878-165">데이터베이스에 연결하여 데이터 프레임으로 데이터를 로드하는 프로세스는 이 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="bd878-166">다음 연결 문자열 형식은 pyodbc를 사용(servername, dbname, username 및 password를 특정 값으로 대체)하여 Python에서 SQL Server 데이터베이스 연결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="bd878-167">Python의 [Pandas 라이브러리](http://pandas.pydata.org/) 에서는 Python 프로그래밍용 데이터 조작을 위한 다양한 데이터 구조 및 데이터 분석 도구 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="bd878-168">아래 코드는 SQL Server 데이터베이스에서 Pandas 데이터 프레임으로 반환되는 결과를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="bd878-169">이제 [데이터 과학 환경에서 Azure Blob 데이터 처리](machine-learning-data-science-process-data-blob.md) 문서에 설명된 대로 Pandas 데이터 프레임으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd878-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="bd878-170">Azure 데이터 과학 작동 예제</span><span class="sxs-lookup"><span data-stu-id="bd878-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="bd878-171">공용 데이터 집합을 사용한 Azure 데이터 과학 프로세스의 종단 간 연습 예제는 [Azure에서 Azure 데이터 과학 프로세스](machine-learning-data-science-process-sql-walkthrough.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd878-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

