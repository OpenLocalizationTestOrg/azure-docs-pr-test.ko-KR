---
title: "Azure의 SQL Server 가상 컴퓨터에서 데이터 탐색 | Microsoft Docs"
description: "Azure에서 SQL Server VM에 저장된 데이터를 탐색하는 방법입니다."
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
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="9a39a-103">Azure의 SQL Server 가상 컴퓨터에서 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="9a39a-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="9a39a-104">이 문서에서는 Azure에서 SQL Server VM에 저장된 데이터를 탐색하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="9a39a-105">이렇게 하려면 SQL을 사용하여 데이터 랭글링을 수행하거나 Python과 같은 프로그래밍 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="9a39a-106">다음 **메뉴** 는 다양한 저장소 환경에서 데이터를 탐색하기 위해 도구를 사용하는 방법을 설명하는 토픽에 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="9a39a-107">이 작업은 Cortana 분석 프로세스(CAP)의 한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="9a39a-108">이 문서의 샘플 SQL 문에서는 데이터가 SQL Server에 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="9a39a-109">그렇지 않은 경우 데이터를 SQL Server로 이동하는 방법은 클라우드 데이터 과학 프로세스 맵을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a39a-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="9a39a-110"><a name="sql-dataexploration"></a>SQL 스크립트로 SQL 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="9a39a-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="9a39a-111">SQL Server에서 데이터 저장소를 탐색하는 데 사용할 수 있는 몇 가지 샘플 SQL 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="9a39a-112">일별 관찰 수 가져오기</span><span class="sxs-lookup"><span data-stu-id="9a39a-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="9a39a-113">범주 열의 수준 가져오기</span><span class="sxs-lookup"><span data-stu-id="9a39a-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="9a39a-114">두 범주 열 조합의 수준 수 가져오기</span><span class="sxs-lookup"><span data-stu-id="9a39a-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="9a39a-115">숫자 열의 분포 가져오기 </span><span class="sxs-lookup"><span data-stu-id="9a39a-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="9a39a-116">실용적인 예제에는 [NYC Taxi 데이터 집합](http://www.andresmh.com/nyctaxitrips/)을 사용할 수 있으며, 종단 간 연습에 [IPython Notebook 및 SQL Server를 사용한 NYC 데이터 랭글링](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb)이라는 IPNB를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="9a39a-117"><a name="python"></a>Python으로 SQL 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="9a39a-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="9a39a-118">데이터가 SQL Server에 있는 경우 Python을 사용하여 데이터를 탐색하고 기능을 생성하는 작업은 [데이터 과학 환경에서 Azure Blob 데이터 처리](machine-learning-data-science-process-data-blob.md)에 설명된 대로 Python을 사용하여 Azure Blob의 데이터를 처리하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="9a39a-119">데이터베이스에서 Pandas DataFrame으로 데이터를 로드해야 하며, 그런 다음 데이터를 추가로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="9a39a-120">데이터베이스에 연결하여 데이터 프레임으로 데이터를 로드하는 프로세스는 이 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="9a39a-121">다음 연결 문자열 형식은 pyodbc를 사용(servername, dbname, username 및 password를 특정 값으로 대체)하여 Python에서 SQL Server 데이터베이스 연결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="9a39a-122">Python의 [Pandas 라이브러리](http://pandas.pydata.org/) 에서는 Python 프로그래밍용 데이터 조작을 위한 다양한 데이터 구조 및 데이터 분석 도구 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="9a39a-123">다음 코드는 SQL Server 데이터베이스에서 Pandas 데이터 프레임으로 반환되는 결과를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="9a39a-124">이제 [데이터 과학 환경에서 Azure Blob 데이터 처리](machine-learning-data-science-process-data-blob.md)토픽에 설명된 대로 Pandas DataFrame으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a39a-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="9a39a-125">실행 중인 Cortana 분석 프로세스 예</span><span class="sxs-lookup"><span data-stu-id="9a39a-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="9a39a-126">공용 데이터 집합을 사용하여 Cortana 분석 프로세스의 종단 간 연습 예제는 [실행 중인 팀 데이터 과학 프로세스: SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a39a-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

