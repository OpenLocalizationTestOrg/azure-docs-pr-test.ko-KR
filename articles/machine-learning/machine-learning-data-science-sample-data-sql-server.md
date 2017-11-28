---
title: "Azure에서 SQL Server에서 데이터 aaaSample | Microsoft Docs"
description: "Azure의 SQL Server에서 데이터 샘플링"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="97c3e-103"><a name="heading"></a>Azure의 SQL Server에서 데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="97c3e-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="97c3e-104">이 문서 SQL 또는 hello Python 프로그래밍 언어 중 하나를 사용 하 여 Azure에서 SQL Server의 toosample 데이터가 저장 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="97c3e-105">또한 방법을 toomove 샘플링 된 데이터에 Azure 기계 학습 업로드 tooa 파일을 저장 하 여 Azure blob tooan 한 후 Azure 기계 학습 스튜디오로 읽는 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="97c3e-106">hello Python 샘플링 hello를 사용 하 여 [pyodbc](https://code.google.com/p/pyodbc/) ODBC 라이브러리 tooconnect tooSQL Azure의 hello 서버 [팬더](http://pandas.pydata.org/) 라이브러리 toodo hello 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="97c3e-107">이 문서에 hello 샘플 SQL 코드는 데이터는 Azure에서 SQL Server에 해당 hello를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="97c3e-108">그럴 경우 읽어보십시오 너무[Azure에서 데이터 tooSQL 서버 이동](machine-learning-data-science-move-sql-server-virtual-machine.md) 방법에 대 한 항목 toomove 사용자 데이터 tooSQL Azure에서 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="97c3e-109">hello 다음 **메뉴** tootopics 설명 하는 연결 방법을 다양 한 저장소 환경에서 toosample 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="97c3e-110">**데이터를 샘플링하는 이유**</span><span class="sxs-lookup"><span data-stu-id="97c3e-110">**Why sample your data?**</span></span>
<span data-ttu-id="97c3e-111">Tooanalyze 계획 hello 데이터 집합이 크면 경우 일반적으로 좋습니다 toodown 샘플 hello 데이터 tooreduce 것 tooa 있지만 대표 작고 더 관리 가능한 수치로 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="97c3e-112">그러면 데이터 이해, 탐색 및 기능 엔지니어링이 용이해집니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="97c3e-113">Hello에서의 역할 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) hello 데이터 처리 기능과 기계 학습 모델 tooenable 빠른 프로토타입 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="97c3e-114">이 샘플링 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="97c3e-115"><a name="SQL"></a>SQL 사용</span><span class="sxs-lookup"><span data-stu-id="97c3e-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="97c3e-116">이 섹션에서는 SQL tooperform 간단한 무작위 샘플링 hello 데이터에 대 한 hello 데이터베이스에서 사용 하 여 여러 가지 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="97c3e-117">데이터 크기 및 해당 분포에 따라 방법을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="97c3e-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="97c3e-118">hello 두 항목 아래에서 SQL Server tooperform toouse newid 샘플링 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="97c3e-119">hello 선택 하는 방법에 따라 얼마나 무작위적 hello 샘플 toobe (아래의 hello 샘플 코드에서 pk_id 가정 toobe 자동 생성 기본 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="97c3e-120">낮은 수준 무작위 샘플</span><span class="sxs-lookup"><span data-stu-id="97c3e-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="97c3e-121">높은 수준 무작위 샘플</span><span class="sxs-lookup"><span data-stu-id="97c3e-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="97c3e-122">아래 표시된 대로 Tablesample을 샘플링에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="97c3e-123">이 수 있습니다 더 나은 방법은 (있다고 가정할 경우 서로 다른 페이지에서 데이터를 상호 관련 되지 않은) 데이터 크기가 크면 쿼리 toocomplete hello에 대 한 적절 한 시간 안에.</span><span class="sxs-lookup"><span data-stu-id="97c3e-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="97c3e-124">이 샘플링된 데이터를 새 테이블에 저장하여 기능을 탐색하고 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="97c3e-125"><a name="sql-aml"></a>TooAzure 기계 학습 연결</span><span class="sxs-lookup"><span data-stu-id="97c3e-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="97c3e-126">Hello Azure 기계 학습에서에서 이후의 hello 샘플 쿼리를 직접 사용할 수 있습니다 [데이터 가져오기] [ import-data] hello 모듈 toodown 샘플 hello 데이터 고객이, Azure 기계 학습 실험으로 상태로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="97c3e-127">Hello 판독기 모듈 tooread hello 샘플링 된 데이터를 사용 하 여의 스크린 샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![판독기 sql][1]

## <span data-ttu-id="97c3e-129"><a name="python"></a>Hello Python 프로그래밍 언어를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="97c3e-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="97c3e-130">이 섹션에서는 hello를 사용 하 여 보여 줍니다. [pyodbc 라이브러리](https://code.google.com/p/pyodbc/) tooestablish ODBC Python에서 tooa SQL server 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="97c3e-131">hello 데이터베이스 연결 문자열은 다음과 같습니다. (구성 서버 이름, dbname, 사용자 이름 및 암호 바꾸기):</span><span class="sxs-lookup"><span data-stu-id="97c3e-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="97c3e-132">hello [팬더](http://pandas.pydata.org/) Python에서 라이브러리에서는 Python 프로그래밍에 대 한 데이터 조작에 대 한 다양 한 데이터 구조 및 데이터 분석 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="97c3e-133">아래 hello 코드 팬더 데이터를 Azure SQL 데이터베이스의 테이블에서 hello 데이터의 0.1% 샘플을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="97c3e-134">이제 hello 팬더 데이터 프레임에서 샘플링 하는 hello 데이터로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="97c3e-135"><a name="python-aml"></a>TooAzure 기계 학습 연결</span><span class="sxs-lookup"><span data-stu-id="97c3e-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="97c3e-136">다음 샘플 코드 toosave hello 축소 샘플링 데이터 tooa 파일 hello를 사용 하 여 및 tooan Azure blob를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="97c3e-137">hello 데이터 hello blob에 직접를 읽을 수는 Azure 컴퓨터 학습 실험으로 hello를 사용 하 여 [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="97c3e-138">hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="97c3e-139">Hello 팬더 데이터 프레임 tooa 로컬 파일 쓰기</span><span class="sxs-lookup"><span data-stu-id="97c3e-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="97c3e-140">로컬 파일 tooAzure blob 업로드</span><span class="sxs-lookup"><span data-stu-id="97c3e-140">Upload local file tooAzure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="97c3e-141">Azure 기계 학습을 사용 하 여 Azure blob에서 데이터를 읽을 [데이터 가져오기] [ import-data] hello 화면 잡기 아래와 같이 모듈:</span><span class="sxs-lookup"><span data-stu-id="97c3e-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![판독기 blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="97c3e-143">작업 예제에 hello 팀 데이터 과학 프로세스</span><span class="sxs-lookup"><span data-stu-id="97c3e-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="97c3e-144">Hello 팀 데이터 과학 프로세스의 종단 간 연습 예제를 보려면 사용 하 여 공용 데이터 집합 참조 [팀 데이터 과학 과정: SQL Sever를 사용 하 여](machine-learning-data-science-process-sql-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="97c3e-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
