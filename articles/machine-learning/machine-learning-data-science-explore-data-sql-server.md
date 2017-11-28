---
title: "aaaExplore 데이터에서 SQL Server Azure에서 가상 컴퓨터 | Microsoft Docs"
description: "어떻게 tooexplore 데이터를 Azure에서 SQL Server VM에 저장 됩니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="276ab-103">Azure의 SQL Server 가상 컴퓨터에서 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="276ab-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="276ab-104">이 문서에서 다루는 방법을 tooexplore 데이터를 Azure에서 SQL Server VM에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="276ab-105">이렇게 하려면 SQL을 사용하여 데이터 랭글링을 수행하거나 Python과 같은 프로그래밍 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="276ab-106">hello 다음 **메뉴** tootopics toouse 도구 tooexplore 데이터 저장소, 다양 한 환경에서 하는 방법을 설명 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="276ab-107">이 작업은 hello Cortana 분석 프로세스 (CAP)의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="276ab-108">이 문서에 hello 샘플 SQL 문을 SQL Server에서 데이터를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="276ab-109">그렇지 않다면 참조 toohello 클라우드 데이터 과학 프로세스 지도 toolearn 어떻게 toomove 사용자 데이터 tooSQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="276ab-110"><a name="sql-dataexploration"></a>SQL 스크립트로 SQL 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="276ab-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="276ab-111">다음은 SQL Server의 데이터 저장소를 사용 하는 tooexplore 일 수 있는 몇 가지 예제 SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="276ab-112">하루 관찰 hello 개수</span><span class="sxs-lookup"><span data-stu-id="276ab-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="276ab-113">범주 열에서 hello 수준을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="276ab-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="276ab-114">두 개의 범주 열 조합에 수준의 hello 수 가져오기</span><span class="sxs-lookup"><span data-stu-id="276ab-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="276ab-115">숫자 열에 대 한 hello 분포 가져오기</span><span class="sxs-lookup"><span data-stu-id="276ab-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="276ab-116">실제 예에 대 한 hello를 사용할 수 있습니다 [NYC 택시 dataset](http://www.andresmh.com/nyctaxitrips/) toohello 이라는 IPNB 참조 및 [NYC 데이터 wrangling IPython 전자 필기장 및 SQL Server를 사용 하 여](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) 종단 간 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="276ab-117"><a name="python"></a>Python으로 SQL 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="276ab-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="276ab-118">Python tooexplore 데이터를 사용 하 고 SQL Server의 데이터는 hello 중인 경우 비슷한 tooprocessing 데이터 Python을 사용 하 여 Azure blob에 설명 된 대로 기능 생성 [프로세스 Azure Blob 데이터에 데이터 과학 환경](machine-learning-data-science-process-data-blob.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="276ab-119">hello 데이터 toobe hello 데이터베이스에서 팬더 데이터 프레임으로 로드 하며 다음 더 이상 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="276ab-120">Toohello 데이터베이스를 연결 하 고이 섹션의 데이터 프레임 hello hello 데이터 로드 hello 과정을 문서화 합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="276ab-121">연결 문자열 형식에 따라 hello pyodbc (서버 이름 바꾸기, dbname, 사용자 이름 및 특정 값으로 암호)를 사용 하 여 Python에서 사용 되는 tooconnect tooa SQL Server 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="276ab-122">hello [팬더 라이브러리](http://pandas.pydata.org/) Python에서는 Python 프로그래밍에 대 한 데이터 조작에 대 한 다양 한 데이터 구조 및 데이터 분석 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="276ab-123">hello 다음 코드 읽어 팬더 데이터 프레임으로 SQL Server 데이터베이스에서 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="276ab-124">작업할 수 있는 hello 팬더 데이터 프레임 hello 항목에서 살펴본 것 처럼 이제 [프로세스 Azure Blob 데이터에 데이터 과학 환경](machine-learning-data-science-process-data-blob.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="276ab-125">실행 중인 Cortana 분석 프로세스 예</span><span class="sxs-lookup"><span data-stu-id="276ab-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="276ab-126">공용 데이터 집합을 사용 하 여 Cortana 분석 프로세스 hello의 종단 간 연습 예제를 참조 하십시오. [팀 데이터 과학 프로세스 작업에 hello: SQL Server를 사용 하 여](machine-learning-data-science-process-sql-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="276ab-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

