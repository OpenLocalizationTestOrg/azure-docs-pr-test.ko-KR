---
title: "SQL 및 Python을 사용하여 SQL Server의 데이터에 대한 기능 만들기 | Microsoft Docs"
description: "SQL Azure에서 데이터 처리"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: f0ac2799e2d8f18b2dd5b633555bfca08a44ba27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="d2397-103">SQL 및 Python을 사용하여 SQL Server의 데이터에 대한 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="d2397-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="d2397-104">이 문서에서는 데이터에서 알고리즘을 효율적으로 학습할 수 있는 Azure의 SQL Server VM에 저장된 데이터에 대한 기능을 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span></span> <span data-ttu-id="d2397-105">이렇게 하려면 SQL을 사용하거나 Python과 같은 프로그래밍 언어를 사용하며, 둘 다 여기에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="d2397-106">이 **메뉴** 는 다양한 환경에서 데이터에 대한 기능을 만드는 방법을 설명하는 토픽으로 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="d2397-107">이 작업은 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="d2397-108">실용적인 예제로는 [NYC Taxi 데이터 집합](http://www.andresmh.com/nyctaxitrips/)을 참조할 수 있으며, 상세한 단계별 연습에는 [IPython Notebook 및 SQL Server를 사용한 NYC 데이터 랭글링](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)이라는 IPNB를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-108">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d2397-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2397-109">Prerequisites</span></span>
<span data-ttu-id="d2397-110">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-110">This article assumes that you have:</span></span>

* <span data-ttu-id="d2397-111">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-111">Created an Azure storage account.</span></span> <span data-ttu-id="d2397-112">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2397-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="d2397-113">데이터가 SQL Server에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="d2397-114">그렇지 않은 경우, 데이터를 이동하는 방법에 대한 지침은 [Azure 기계 학습을 위해 Azure SQL 데이터베이스로 데이터 이동](machine-learning-data-science-move-sql-azure.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2397-114">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how to move the data there.</span></span>

## <span data-ttu-id="d2397-115"><a name="sql-featuregen"></a>SQL로 기능 생성</span><span class="sxs-lookup"><span data-stu-id="d2397-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="d2397-116">이 섹션에서는 SQL을 사용하여 기능을 생성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="d2397-117">개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="d2397-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="d2397-118">범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="d2397-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="d2397-119">단일 열에서 기능 롤아웃</span><span class="sxs-lookup"><span data-stu-id="d2397-119">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="d2397-120">추가 기능을 생성한 후 이를 기존 테이블에 열로 추가하거나, 추가 기능 및 기본 키를 사용하여 새 테이블을 만들어 원래 테이블에 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-120">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span>
> 
> 

### <span data-ttu-id="d2397-121"><a name="sql-countfeature"></a>개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="d2397-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="d2397-122">이 문서에서는 개수 기능을 생성하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="d2397-123">첫 번째 방법에서는 조건부 합계를 사용하고, 두 번째 방법에서는 'where' 절을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-123">The first method uses conditional sum and the second method uses the 'where\` clause.</span></span> <span data-ttu-id="d2397-124">그런 다음 원래 데이터와 함께 개수 기능을 유지하도록 원래 테이블에 조인할 수 있습니다(기본 키 열 사용).</span><span class="sxs-lookup"><span data-stu-id="d2397-124">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="d2397-125"><a name="sql-binningfeature"></a>범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="d2397-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="d2397-126">다음 예제에서는 기능으로 사용할 수 있는 숫자 열을 범주화하여(5개의 bin 사용) 범주화된 기능을 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-126">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="d2397-127"><a name="sql-featurerollout"></a>단일 열에서 기능 롤아웃</span><span class="sxs-lookup"><span data-stu-id="d2397-127"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="d2397-128">이 섹션에서는 테이블의 단일 열을 롤아웃하여 추가 기능을 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-128">In this section, we demonstrate how to roll-out a single column in a table to generate additional features.</span></span> <span data-ttu-id="d2397-129">이 예제에서는 기능을 생성하려는 테이블에 위도 또는 경도 열이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-129">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="d2397-130">다음은 위도/경도 위치 데이터에 대한 간략한 기초 정보입니다(stackoverflow( `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`)에서 발췌).</span><span class="sxs-lookup"><span data-stu-id="d2397-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="d2397-131">위치 필드를 기능화하기 전에 이 정보를 이해하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-131">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="d2397-132">부호는 지구에서 현재 위치의 방위(북쪽, 남쪽, 동쪽 또는 서쪽)를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-132">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="d2397-133">0이 아닌 100자리수는 위도가 아니라 경도를 사용하고 있음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="d2397-134">10자리수는 약 1,000km까지의 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-134">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="d2397-135">현재 위치의 대륙 또는 대양에 대한 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="d2397-136">단위 자리수(하나의 도 단위)는 최대 111km(60해리, 약 69마일)까지의 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-136">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="d2397-137">이는 현재 위치의 주 또는 국가를 대략적으로 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="d2397-138">첫 번째 소수 자릿수는 11.1km까지 적용되며, 하나의 대도시를 인접한 대도시와 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-138">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="d2397-139">두 번째 소수 자릿수는 1.1km까지 적용되며, 하나의 마을을 다음 마을과 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-139">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="d2397-140">세 번째 소수 자릿수는 110m까지 적용되며, 대규모 농경지 또는 기업 부지를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-140">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="d2397-141">네 번째 소수 자릿수는 11m까지 적용되며, 하나의 필지를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-141">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="d2397-142">이는 간섭 없이 보정되지 않은 GPS 장치의 일반적인 정확도에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-142">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="d2397-143">다섯 번째 소수 자릿수는 1.1m까지 적용되며, 수목을 서로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-143">The fifth decimal place is worth up to 1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="d2397-144">상용 GPS 장치에서는 미분 보정을 통해서만 이 수준의 정확도를 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-144">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="d2397-145">여섯 번째 소수 자릿수는 0.11m까지 적용되며, 상세 구조물 배치, 조경 설계, 도로 건설 등에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-145">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="d2397-146">빙하 및 강의 이동을 추적하는 데 매우 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="d2397-147">미분 보정된 GPS와 같은 GPS로 세밀히 측정하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="d2397-148">위치 정보는 다음과 같이 지역, 위치 및 도시 정보를 구분하여 기능화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-148">The location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="d2397-149">또한 Bing Maps API( `https://msdn.microsoft.com/library/ff701710.aspx` )와 같은 REST 끝점을 호출하여 지역/구역 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span></span>

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

<span data-ttu-id="d2397-150">위의 위치 기반 기능을 사용하여 앞서 설명한 대로 추가 개수 기능을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-150">The above location based features can be further used to generate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="d2397-151">선택한 언어를 사용하여 프로그래밍 방식으로 레코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-151">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="d2397-152">쓰기 효율성을 개선하기 위해 청크에 데이터를 삽입해야 할 수도 있습니다. [pyodbc를 사용하여 이 작업을 수행하는 방법에 대한 예제는 여기를 참조하세요](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="d2397-152">You may need to insert the data in chunks to improve write efficiency [Check out the example of how to do this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="d2397-153">또 다른 방법은 [BCP 유틸리티](https://msdn.microsoft.com/library/ms162802.aspx)를 사용하여 데이터베이스에 데이터를 삽입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-153">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="d2397-154"><a name="sql-aml"></a>Azure 기계 학습에 연결</span><span class="sxs-lookup"><span data-stu-id="d2397-154"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="d2397-155">새로 생성한 기능을 기존 테이블에 열로 추가하거나, 새 테이블에 저장하여 기계 학습을 위해 원래 테이블과 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-155">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="d2397-156">Azure 기계 학습에서는 아래 표시된 대로 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 모듈을 사용하여 기능을 생성하거나 액세스(이미 만든 경우)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-156">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml 판독기](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="d2397-158"><a name="python"></a>Python과 같은 프로그래밍 언어 사용</span><span class="sxs-lookup"><span data-stu-id="d2397-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="d2397-159">데이터가 SQL Server에 있는 경우 Python을 사용하여 기능을 생성하는 작업은 [데이터 과학 환경에서 Azure Blob 데이터 처리](machine-learning-data-science-process-data-blob.md)에 설명된 대로 Python을 사용하여 Azure Blob의 데이터를 처리하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-159">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="d2397-160">데이터베이스에서 pandas 데이터 프레임으로 데이터를 로드해야 하며, 그런 다음 데이터를 추가로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-160">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="d2397-161">데이터베이스에 연결하여 데이터 프레임으로 데이터를 로드하는 프로세스는 이 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-161">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="d2397-162">다음 연결 문자열 형식은 pyodbc를 사용(servername, dbname, username 및 password를 특정 값으로 대체)하여 Python에서 SQL Server 데이터베이스 연결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-162">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="d2397-163">Python의 [Pandas 라이브러리](http://pandas.pydata.org/) 에서는 Python 프로그래밍용 데이터 조작을 위한 다양한 데이터 구조 및 데이터 분석 도구 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-163">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="d2397-164">아래 코드는 SQL Server 데이터베이스에서 Pandas 데이터 프레임으로 반환되는 결과를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-164">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="d2397-165">이제 [Panda를 사용하여 Azure blob 저장소 데이터에 대한 기능 만들기](machine-learning-data-science-create-features-blob.md)토픽에 설명된 대로 Pandas 데이터 프레임으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2397-165">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

