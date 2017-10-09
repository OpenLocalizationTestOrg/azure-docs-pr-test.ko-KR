---
title: "SQL 및 Python을 사용 하 여 SQL Server에서 데이터에 대 한 aaaCreate 기능 | Microsoft Docs"
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
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="f0ea1-103">SQL 및 Python을 사용하여 SQL Server의 데이터에 대한 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="f0ea1-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="f0ea1-104">이 문서에서는 알아보려면 어떻게 해야 알고리즘 데 도움이 되는 Azure에서 SQL Server VM에 저장 된 데이터에 대 한 toogenerate 기능 보다 효율적으로 hello 데이터에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="f0ea1-105">이렇게 하려면 SQL을 사용하거나 Python과 같은 프로그래밍 언어를 사용하며, 둘 다 여기에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="f0ea1-106">이 **메뉴** tootopics toocreate 다양 한 환경에서 데이터에 대 한 기능 하는 방법을 설명 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="f0ea1-107">이 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="f0ea1-108">실제 예에 대 한 hello를 참조할 수 있습니다 [NYC 택시 dataset](http://www.andresmh.com/nyctaxitrips/) toohello 이라는 IPNB 참조 및 [NYC 데이터 wrangling IPython 전자 필기장 및 SQL Server를 사용 하 여](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) 종단 간 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f0ea1-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f0ea1-109">Prerequisites</span></span>
<span data-ttu-id="f0ea1-110">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-110">This article assumes that you have:</span></span>

* <span data-ttu-id="f0ea1-111">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-111">Created an Azure storage account.</span></span> <span data-ttu-id="f0ea1-112">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="f0ea1-113">데이터가 SQL Server에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="f0ea1-114">참조 하지 않은 경우 [Azure 기계 학습에 대 한 데이터 tooan Azure SQL 데이터베이스를 이동](machine-learning-data-science-move-sql-azure.md) toomove 데이터 hello 하는 방법에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="f0ea1-115"><a name="sql-featuregen"></a>SQL로 기능 생성</span><span class="sxs-lookup"><span data-stu-id="f0ea1-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="f0ea1-116">이 섹션에서는 SQL을 사용하여 기능을 생성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="f0ea1-117">개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="f0ea1-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="f0ea1-118">범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="f0ea1-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="f0ea1-119">하나의 열에서 hello 기능 출시</span><span class="sxs-lookup"><span data-stu-id="f0ea1-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="f0ea1-120">추가 기능을 생성 한 후 toohello 기존 테이블 열으로 추가 하거나 hello 추가 기능 및 hello 원래 테이블과 조인할 수 있는 기본 키를 사용 하 여 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="f0ea1-121"><a name="sql-countfeature"></a>개수 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="f0ea1-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="f0ea1-122">이 문서에서는 개수 기능을 생성하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="f0ea1-123">hello 첫 번째 방법은 조건부 합계를 사용 하 고 hello 두 번째 방법을 사용 하 여 hello 'where' 절.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="f0ea1-124">이러한 기능을 통해 hello 원래 (기본 키 열을 사용 하 여) 테이블 toohave count hello 원래 데이터와 함께 다음 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="f0ea1-125"><a name="sql-binningfeature"></a>범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="f0ea1-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="f0ea1-126">hello 다음 예제는 어떻게 toogenerate 범주화 기능 (5 bin 사용)을 범주화 하 여 숫자 열을 기능으로 대신 사용할 수 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="f0ea1-127"><a name="sql-featurerollout"></a>하나의 열에서 hello 기능 출시</span><span class="sxs-lookup"><span data-stu-id="f0ea1-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="f0ea1-128">이 섹션에서는 어떻게 tooroll 아웃 테이블 toogenerate 추가 기능에서 단일 열 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="f0ea1-129">hello 예제 toogenerate 기능 하려는 hello 표에 위도 또는 경도의 열 이라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="f0ea1-130">다음은 위도/경도 위치 데이터에 대한 간략한 기초 정보입니다(stackoverflow( `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`)에서 발췌).</span><span class="sxs-lookup"><span data-stu-id="f0ea1-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="f0ea1-131">다음은 유용한 toounderstand featurizing hello 위치 필드 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="f0ea1-132">hello 로그인 여부는으로 북쪽 또는 남쪽, 동쪽 또는 서쪽 hello 전 세계의 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="f0ea1-133">0이 아닌 100자리수는 위도가 아니라 경도를 사용하고 있음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="f0ea1-134">hello 수십 자리는 1, 000 킬로미터 위치 tooabout를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="f0ea1-135">현재 위치의 대륙 또는 대양에 대한 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="f0ea1-136">hello 단위 자리 (하나의 10 진수 각도) too111 킬로미터 (60 해상 마일, 69 마일 약)를 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="f0ea1-137">이는 현재 위치의 주 또는 국가를 대략적으로 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="f0ea1-138">첫 번째 소수점 자리 hello 중일 가치가 too11.1 km: hello 인접 대도시에서 하나의 큰 도시 위치를 구별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="f0ea1-139">hello 2 소수 순위는 too1.1 km를: 하나의 village hello에서 다음 구분할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="f0ea1-140">hello 3 소수 순위는 too110 m:를 큰 agricultural 필드 또는 규격화 캠퍼스 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="f0ea1-141">hello 네 번째 소수 자릿수는 가치가 too11 m: 육지의 파 슬 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="f0ea1-142">비교 가능한 toohello 일반적인 정확도 간섭이 없는 GPS 단위의 수정 되지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="f0ea1-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="f0ea1-143">hello 다섯 번째 소수 순위는 too1.1 m:를이 트리를 서로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="f0ea1-144">상용 GPS 단위와 정확도 toothis 수준은 차등 수정 내용과 함께 으로만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="f0ea1-145">hello 여섯 번째 소수점 자리 가치가 too0.11 m: 사용할 수 있습니다이 구조 지형의 디자인에 대 한 세부 정보를 배치 하기 위한로로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="f0ea1-146">빙하 및 강의 이동을 추적하는 데 매우 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="f0ea1-147">미분 보정된 GPS와 같은 GPS로 세밀히 측정하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="f0ea1-148">hello 위치 정보 수 들어가지 않고 기능화 다음과 같을 수 있습니다, 지역, 위치 및 도시 정보 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="f0ea1-149">한 번 Bing Maps API에서 사용할 수 있는 등 REST 끝점을 호출할 수도 있습니다는 `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello 지역/지역 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

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

<span data-ttu-id="f0ea1-150">앞에서 설명한 대로 toogenerate count 추가 기능을 사용 하는 hello 위의 위치 기반된 기능이 추가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="f0ea1-151">프로그래밍 방식으로 선택한 언어를 사용 하 여 hello 레코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="f0ea1-152">데이터 청크 tooimprove 쓰기 효율성에 tooinsert hello를 할 수 있습니다 [방법의 예 hello 확인해 보세요 toodo이 여기 pyodbc를 사용 하 여](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="f0ea1-153">또 다른 방법은 더 tooinsert 데이터를 사용 하 여 hello 데이터베이스에서 [BCP 유틸리티](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="f0ea1-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="f0ea1-154"><a name="sql-aml"></a>TooAzure 기계 학습 연결</span><span class="sxs-lookup"><span data-stu-id="f0ea1-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="f0ea1-155">새로 생성 하는 hello 기능을 열 tooan 기존 테이블로 추가 또는 새 테이블에 저장을 hello 기계 학습에 원래 테이블과 조인 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="f0ea1-156">기능을 생성 하거나 hello를 사용 하 여 이미 만든 경우 액세스할 수 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 아래와 같이 Azure 기계 학습의 모듈:</span><span class="sxs-lookup"><span data-stu-id="f0ea1-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml 판독기](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="f0ea1-158"><a name="python"></a>Python과 같은 프로그래밍 언어 사용</span><span class="sxs-lookup"><span data-stu-id="f0ea1-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="f0ea1-159">에 설명 된 대로 Python을 사용 하 여 Azure blob에는 비슷한 tooprocessing 데이터 hello 데이터가 SQL Server의 경우 Python toogenerate 기능을 사용 하 여 [프로세스 Azure Blob 데이터에 데이터 과학 환경](machine-learning-data-science-process-data-blob.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="f0ea1-160">hello 데이터 toobe 팬더 데이터 프레임으로 hello 데이터베이스에서 로드 하며 다음 더 이상 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="f0ea1-161">Toohello 데이터베이스를 연결 하 고이 섹션의 hello 데이터 프레임으로 hello 데이터 로드 hello 과정을 문서화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="f0ea1-162">연결 문자열 형식에 따라 hello pyodbc (서버 이름 바꾸기, dbname, 사용자 이름 및 특정 값으로 암호)를 사용 하 여 Python에서 사용 되는 tooconnect tooa SQL Server 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="f0ea1-163">hello [팬더 라이브러리](http://pandas.pydata.org/) Python에서는 Python 프로그래밍에 대 한 데이터 조작에 대 한 다양 한 데이터 구조 및 데이터 분석 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="f0ea1-164">아래 hello 코드 팬더 데이터 프레임으로 SQL Server 데이터베이스에서 반환 된 hello 결과 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="f0ea1-165">에서 설명 하는 hello 팬더 데이터 프레임 작업할 수 이제 [팬더를 사용 하 여 Azure blob 저장소 데이터에 대 한 기능을 만드는](machine-learning-data-science-create-features-blob.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ea1-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

