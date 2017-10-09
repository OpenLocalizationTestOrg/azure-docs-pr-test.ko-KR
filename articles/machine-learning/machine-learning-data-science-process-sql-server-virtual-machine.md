---
title: "Azure에서 SQL Server 가상 컴퓨터의 데이터를 aaaExplore | Microsoft Docs"
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
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="7f500-103"><a name="heading"></a>Azure의 SQL Server 가상 컴퓨터에서 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="7f500-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="7f500-104">이 문서에서 다루는 방법을 tooexplore 데이터 및 Azure에서 SQL Server VM에 저장 된 데이터에 대 한 기능을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="7f500-105">이렇게 하려면 SQL을 사용하여 데이터 랭글링을 수행하거나 Python과 같은 프로그래밍 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="7f500-106">이 문서에 hello 샘플 SQL 문을 SQL Server에서 데이터를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="7f500-107">그렇지 않다면 참조 toohello 클라우드 데이터 과학 프로세스 지도 toolearn 어떻게 toomove 사용자 데이터 tooSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="7f500-108"><a name="SQL"></a>SQL 사용</span><span class="sxs-lookup"><span data-stu-id="7f500-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="7f500-109">SQL을 사용 하 여이 섹션에서는 데이터 wrangling 작업을 수행 하는 hello 설명:</span><span class="sxs-lookup"><span data-stu-id="7f500-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="7f500-110">데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="7f500-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="7f500-111">기능 생성</span><span class="sxs-lookup"><span data-stu-id="7f500-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="7f500-112"><a name="sql-dataexploration"></a>데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="7f500-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="7f500-113">다음은 SQL Server의 데이터 저장소를 사용 하는 tooexplore 일 수 있는 몇 가지 예제 SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="7f500-114">실제 예에 대 한 hello를 사용할 수 있습니다 [NYC 택시 dataset](http://www.andresmh.com/nyctaxitrips/) toohello 이라는 IPNB 참조 및 [NYC 데이터 wrangling IPython 전자 필기장 및 SQL Server를 사용 하 여](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) 종단 간 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="7f500-115">하루 관찰 hello 개수</span><span class="sxs-lookup"><span data-stu-id="7f500-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="7f500-116">범주 열에서 hello 수준을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="7f500-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="7f500-117">두 개의 범주 열 조합에 수준의 hello 수 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f500-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="7f500-118">숫자 열에 대 한 hello 분포 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f500-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="7f500-119"><a name="sql-featuregen"></a>기능 생성</span><span class="sxs-lookup"><span data-stu-id="7f500-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="7f500-120">이 섹션에서는 SQL을 사용하여 기능을 생성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="7f500-121">개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="7f500-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="7f500-122">범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="7f500-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="7f500-123">하나의 열에서 hello 기능 출시</span><span class="sxs-lookup"><span data-stu-id="7f500-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="7f500-124">추가 기능을 생성 한 후 toohello 기존 테이블 열으로 추가 하거나 hello 추가 기능 및 hello 원래 테이블과 조인할 수 있는 기본 키를 사용 하 여 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="7f500-125"><a name="sql-countfeature"></a>개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="7f500-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="7f500-126">hello 다음 예제에서는 두 가지 방법을 보여 수 기능을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="7f500-127">hello 첫 번째 방법은 조건부 합계를 사용 하 고 hello 두 번째 방법을 사용 하 여 hello 'where' 절.</span><span class="sxs-lookup"><span data-stu-id="7f500-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="7f500-128">이러한 기능을 통해 hello 원래 (기본 키 열을 사용 하 여) 테이블 toohave count hello 원래 데이터와 함께 다음 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="7f500-129"><a name="sql-binningfeature"></a>범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="7f500-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="7f500-130">hello 다음 예제는 어떻게 toogenerate 범주화 기능 (다섯 개의 bin 사용)을 범주화 하 여 숫자 열을 기능으로 대신 사용할 수 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="7f500-131"><a name="sql-featurerollout"></a>하나의 열에서 hello 기능 출시</span><span class="sxs-lookup"><span data-stu-id="7f500-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="7f500-132">이 섹션에 대해서도 설명 방법을 tooroll 테이블 toogenerate 추가 기능에서 단일 열을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="7f500-133">hello 예제 toogenerate 기능 하려는 hello 표에 위도 또는 경도의 열 이라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="7f500-134">위도/경도 위치 데이터에 대 한 간략 한 입문서입니다 (stackoverflow에서 리소스 [어떻게 toomeasure 위도 및 경도의 정확도 hello?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="7f500-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="7f500-135">다음은 유용한 toounderstand featurizing hello 위치 필드 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="7f500-136">hello 로그인 여부는으로 북쪽 또는 남쪽, 동쪽 또는 서쪽 hello 전 세계의 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="7f500-137">0이 아닌 100자리수는 위도가 아니라 경도를 사용하고 있음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="7f500-138">hello 수십 자리는 1, 000 킬로미터 위치 tooabout를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="7f500-139">현재 위치의 대륙 또는 대양에 대한 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="7f500-140">hello 단위 자리 (하나의 10 진수 각도) too111 킬로미터 (60 해상 마일, 69 마일 약)를 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="7f500-141">이는 현재 위치의 주 또는 국가를 대략적으로 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="7f500-142">첫 번째 소수점 자리 hello 중일 가치가 too11.1 km: hello 인접 대도시에서 하나의 큰 도시 위치를 구별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="7f500-143">hello 2 소수 순위는 too1.1 km를: 하나의 village hello에서 다음 구분할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="7f500-144">hello 3 소수 순위는 too110 m:를 큰 agricultural 필드 또는 규격화 캠퍼스 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="7f500-145">hello 네 번째 소수 자릿수는 가치가 too11 m: 육지의 파 슬 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="7f500-146">비교 가능한 toohello 일반적인 정확도 간섭이 없는 GPS 단위의 수정 되지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="7f500-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="7f500-147">hello 다섯 번째 소수 순위는 too1.1 m:를 각 트리를 구별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="7f500-148">상용 GPS 단위와 정확도 toothis 수준은 차등 수정 내용과 함께 으로만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="7f500-149">hello 여섯 번째 소수점 자리 가치가 too0.11 m: 사용할 수 있습니다이 구조 지형의 디자인에 대 한 세부 정보를 배치 하기 위한로로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="7f500-150">빙하 및 강의 이동을 추적하는 데 매우 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="7f500-151">미분 보정된 GPS와 같은 GPS로 세밀히 측정하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="7f500-152">hello 위치 정보 수 들어가지 않고 기능화 될 다음과 같은 영역, 위치 및 도시 정보 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="7f500-153">Bing Maps API에서 사용할 수 있는 등 REST 끝점 호출 또한 수 [지점별 위치를 찾을](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello 지역/지역 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

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

<span data-ttu-id="7f500-154">이러한 위치 기반 기능이 될 수 있습니다 더 이상 사용 되는 toogenerate 추가 개수 기능 앞에서 설명한 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="7f500-155">프로그래밍 방식으로 선택한 언어를 사용 하 여 hello 레코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="7f500-156">데이터 청크 tooimprove 쓰기 효율성에 tooinsert hello를 할 수 있습니다 (방법의 예에 대 한 toodo이 pyodbc를 사용 하 여 참조 [python A HelloWorld 샘플 tooaccess SQLServer](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="7f500-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="7f500-157">다른 방법은 hello를 사용 하 여 hello 데이터베이스의 데이터를 tooinsert [BCP 유틸리티](https://msdn.microsoft.com/library/ms162802.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="7f500-158"><a name="sql-aml"></a>TooAzure 기계 학습 연결</span><span class="sxs-lookup"><span data-stu-id="7f500-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="7f500-159">새로 생성 하는 hello 기능을 열 tooan 기존 테이블로 추가 또는 새 테이블에 저장을 hello 기계 학습에 원래 테이블과 조인 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="7f500-160">기능을 생성 하거나 hello를 사용 하 여 이미 만든 경우 액세스할 수 [데이터 가져오기] [ import-data] 아래와 같이 Azure 기계 학습의 모듈:</span><span class="sxs-lookup"><span data-stu-id="7f500-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml 판독기][1] 

## <span data-ttu-id="7f500-162"><a name="python"></a>Python과 같은 프로그래밍 언어 사용</span><span class="sxs-lookup"><span data-stu-id="7f500-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="7f500-163">Python tooexplore 데이터를 사용 하 고 SQL Server의 데이터는 hello 비슷한 tooprocessing 데이터에 설명 된 대로 Python을 사용 하 여 Azure blob의 경우 기능 생성 [프로세스 Azure Blob 데이터에 데이터 과학 환경](machine-learning-data-science-process-data-blob.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="7f500-164">hello 데이터 toobe 팬더 데이터 프레임으로 hello 데이터베이스에서 로드 하며 다음 더 이상 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="7f500-165">Toohello 데이터베이스를 연결 하 고이 섹션의 hello 데이터 프레임으로 hello 데이터 로드 hello 과정을 문서화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="7f500-166">연결 문자열 형식에 따라 hello pyodbc (서버 이름 바꾸기, dbname, 사용자 이름 및 특정 값으로 암호)를 사용 하 여 Python에서 사용 되는 tooconnect tooa SQL Server 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="7f500-167">hello [팬더 라이브러리](http://pandas.pydata.org/) Python에서는 Python 프로그래밍에 대 한 데이터 조작에 대 한 다양 한 데이터 구조 및 데이터 분석 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="7f500-168">아래 hello 코드 팬더 데이터 프레임으로 SQL Server 데이터베이스에서 반환 된 hello 결과 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="7f500-169">Hello 문서에서 다루는 hello 팬더 데이터 프레임 작업할 수 이제 [프로세스 Azure Blob 데이터에 데이터 과학 환경](machine-learning-data-science-process-data-blob.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="7f500-170">Azure 데이터 과학 작동 예제</span><span class="sxs-lookup"><span data-stu-id="7f500-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="7f500-171">공용 데이터 집합을 사용 하 여 Azure 데이터 과학 프로세스 hello의 종단 간 연습 예제를 참조 하십시오. [Azure 데이터 과학 과정](machine-learning-data-science-process-sql-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f500-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

