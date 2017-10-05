---
title: "Azure Data Lake를 사용한 확장성 있는 데이터 과학: 종단 간 연습 | Microsoft Docs"
description: "Azure Data Lake를 사용하여 데이터 집합에 대해 데이터 탐색 및 이진 분류 작업을 수행하는 방법입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 34fbe99572b4a6cee73de6ae5412a0ec09dd1ccc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="36ae0-103">Azure Data Lake를 사용한 확장성 있는 데이터 과학: 종단 간 연습</span><span class="sxs-lookup"><span data-stu-id="36ae0-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="36ae0-104">이 연습에서는 팁을 요금으로 지급할지 여부를 예측하기 위해 NYC Taxi Trip 및 요금 데이터 집합 샘플에서 데이터 탐색 및 이진 분류 작업을 수행하는 데 Azure Data Lake를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-104">This walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi trip and fare dataset to predict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="36ae0-105">[팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess), 종단 간, 데이터 획득에서 모델 학습 후 모델을 게시하는 웹 서비스 배포 단계까지 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-105">It walks you through the steps of the [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition to model training, and then to the deployment of a web service that publishes the model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="36ae0-106">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="36ae0-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="36ae0-107">[Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) 는 데이터 과학자가 임의 크기, 모양 및 속도로 데이터를 저장하고 데이터 처리, 고급 분석 및 기계 학습 모델링을 높은 확장성과 함께 비용 효율적으로 수행하는 데 필요한 모든 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-107">The [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all the capabilities required to make it easy for data scientists to store data of any size, shape and speed, and to conduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="36ae0-108">데이터가 실제로 처리되는 경우에만 작업 단위로 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="36ae0-109">Azure Data Lake 분석에는 SQL의 선언적 특성을 C#의 표현 능력으로 혼합하여 확장성 있는 분산 쿼리 기능을 제공하는 언어인 U-SQL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-109">Azure Data Lake Analytics includes U-SQL, a language that blends the declarative nature of SQL with the expressive power of C# to provide scalable distributed query capability.</span></span> <span data-ttu-id="36ae0-110">이를 통해, 읽기에 스키마를 적용하여 구조화되지 않은 데이터를 처리하고, 사용자 지정 논리 및 UDF(사용자 정의 함수)를 삽입하고, 대규모 실행 방법을 정교하게 세분화하여 제어할 수 있도록 확장성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-110">It enables you to process unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility to enable fine grained control over how to execute at scale.</span></span> <span data-ttu-id="36ae0-111">U-SQL의 디자인 원리에 대해 자세히 알아보려면 [Visual Studio 블로그 게시물](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-111">To learn more about the design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="36ae0-112">Data Lake 분석은 또한 Cortana Analytics Suite에서 핵심적인 부분으로, Azure SQL 데이터 웨어하우스, Power BI 및 Data Factory와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="36ae0-113">이렇게 전체 클라우드 빅 데이터 및 고급 분석 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="36ae0-114">이 연습에서는 데이터 과학 프로세스를 구성하는 Data Lake 분석에서 작업을 완료하는 데 필요한 필수 조건 및 리소스와 이를 설치하는 방법을 설명하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-114">This walkthrough begins by describing the prerequisites and resources that are needed to complete the tasks with Data Lake Analytics that form the data science process and how to install them.</span></span> <span data-ttu-id="36ae0-115">그런 후 U-SQL을 사용하여 데이터 처리 단계를 요약하고, 마지막으로 Azure 기계 학습 스튜디오에서 Python 및 Hive를 사용하여 예측 모델을 빌드하고 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-115">Then it outlines the data processing steps using U-SQL and concludes by showing how to use Python and Hive with Azure Machine Learning Studio to build and deploy the predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="36ae0-116">U-SQL 및 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36ae0-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="36ae0-117">이 연습에서는 Visual Studio를 사용하여 데이터 집합을 처리하도록 U-SQL 스크립트를 편집할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-117">This walkthrough recommends using Visual Studio to edit U-SQL scripts to process the dataset.</span></span> <span data-ttu-id="36ae0-118">U-SQL 스크립트는 여기서 설명하고 별도의 파일로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-118">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="36ae0-119">이 프로세스에는 데이터 수집, 탐색 및 샘플링이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-119">The process includes ingesting, exploring, and sampling the data.</span></span> <span data-ttu-id="36ae0-120">또한 Azure 포털에서 U-SQL 스크립트 작업을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-120">It also shows how to run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="36ae0-121">Azure 기계 학습 스튜디오에서 이진 분류 모델의 빌드 및 배포를 용이하게 하기 위해 연결된 HDInsight 클러스터에 데이터에 대한 Hive 테이블이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-121">Hive tables are created for the data in an associated HDInsight cluster to facilitate the building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="36ae0-122">Python</span><span class="sxs-lookup"><span data-stu-id="36ae0-122">Python</span></span>
<span data-ttu-id="36ae0-123">이 연습에는 Azure 기계 학습 스튜디오에서 Python을 사용하여 예측 모델을 빌드 및 배포하는 방법을 보여 주는 섹션도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-123">This walkthrough also contains a section that shows how to build and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="36ae0-124">이 프로세스의 이러한 단계에 대해 Python 스크립트와 함께 Jupyter Notebook을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-124">We provide a Jupyter notebook with the Python scripts for these steps in this process.</span></span> <span data-ttu-id="36ae0-125">Notebook에는 여기에 설명된 이진 분류 모델 외에도 다중 클래스 분류 및 회귀 모델링과 같은 추가 기능 엔지니어링 단계 및 모델 생성을 위한 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-125">The notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition to the binary classification model outlined here.</span></span> <span data-ttu-id="36ae0-126">회귀 작업은 다른 팁 기능을 기반으로 하는 팁의 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-126">The regression task is to predict the amount of the tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="36ae0-127">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="36ae0-127">Azure Machine Learning</span></span>
<span data-ttu-id="36ae0-128">Azure 기계 학습 스튜디오는 예측 모델을 빌드 및 배포하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-128">Azure Machine Learning Studio is used to build and deploy the predictive models.</span></span> <span data-ttu-id="36ae0-129">이러한 작업은 먼저 Python 스크립트를 사용한 다음 HDInsight(Hadoop) 클러스터의 Hive 테이블을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="36ae0-130">스크립트</span><span class="sxs-lookup"><span data-stu-id="36ae0-130">Scripts</span></span>
<span data-ttu-id="36ae0-131">이 연습에는 주요 단계만 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-131">Only the principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="36ae0-132">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)에서 전체 **U-SQL 스크립트** 및 **Jupyter Notebook**을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-132">You can download the full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36ae0-133">필수 조건</span><span class="sxs-lookup"><span data-stu-id="36ae0-133">Prerequisites</span></span>
<span data-ttu-id="36ae0-134">이 토픽을 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-134">Before you begin these topics, you must have the following:</span></span>

* <span data-ttu-id="36ae0-135">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="36ae0-135">An Azure subscription.</span></span> <span data-ttu-id="36ae0-136">아직 가지고 있지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="36ae0-137">[권장] Visual Studio 2013 이상.</span><span class="sxs-lookup"><span data-stu-id="36ae0-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="36ae0-138">아직 이러한 버전이 설치되지 않은 경우 [Visual Studio Community](https://www.visualstudio.com/vs/community/)에서 무료로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="36ae0-139">Visual Studio 대신 Azure 포털을 사용하여 Azure Data Lake 쿼리를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-139">Instead of Visual Studio, you can also use the Azure Portal to submit Azure Data Lake queries.</span></span> <span data-ttu-id="36ae0-140">Visual Studio 및 포털에서 이 작업을 수행하는 방법에 대한 지침은 **U-SQL로 데이터 처리**섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-140">We will provide instructions on how to do so both with Visual Studio and on the portal in the section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="36ae0-141">Azure Data Lake에 대한 데이터 과학 환경 준비</span><span class="sxs-lookup"><span data-stu-id="36ae0-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="36ae0-142">이 연습에 대한 데이터 과학 환경을 준비하려면 다음 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-142">To prepare the data science environment for this walkthrough, create the following resources:</span></span>

* <span data-ttu-id="36ae0-143">Azure Data Lake 저장소(ADLS)</span><span class="sxs-lookup"><span data-stu-id="36ae0-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="36ae0-144">Azure Data Lake 분석(ADLA)</span><span class="sxs-lookup"><span data-stu-id="36ae0-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="36ae0-145">Azure Blob 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="36ae0-145">Azure Blob storage account</span></span>
* <span data-ttu-id="36ae0-146">Azure 기계 학습 스튜디오 계정</span><span class="sxs-lookup"><span data-stu-id="36ae0-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="36ae0-147">Visual Studio용 Azure Data Lake 도구(권장)</span><span class="sxs-lookup"><span data-stu-id="36ae0-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="36ae0-148">이 섹션에서는 이러한 각 리소스를 만드는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-148">This section provides instructions on how to create each of these resources.</span></span> <span data-ttu-id="36ae0-149">Azure 기계 학습에서 Python 대신 Hive 테이블을 사용하여 모델을 작성하려는 경우 HDInsight(Hadoop) 클러스터를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-149">If you choose to use Hive tables with Azure Machine Learning, instead of Python, to build a model,you will also need to provision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="36ae0-150">이러한 대체 절차는 아래의 해당 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-150">This alternative procedure in described in the appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="36ae0-151">**Azure Data Lake Store**는 별도로 만들거나 **Azure Data Lake Analytics**을 만들 때 기본 저장소로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-151">The **Azure Data Lake Store** can be created either separately or when you create the **Azure Data Lake Analytics** as the default storage.</span></span> <span data-ttu-id="36ae0-152">아래에서는 이러한 각 리소스를 만들기 위한 지침이 별도로 참조되지만 Data Lake 저장소 계정을 별도의 단계로 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-152">Instructions are referenced for creating each of these resources separately below, but the Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="36ae0-153">Azure 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="36ae0-154">[Azure 포털](http://portal.azure.com)에서 ADLS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-154">Create an ADLS from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="36ae0-155">자세한 내용은 [Azure 포털을 사용하여 Data Lake 저장소로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="36ae0-156">여기 설명된 **옵션 구성** 블레이드의 **DataSource** 블레이드에서 클러스터 AAD ID를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-156">Be sure to set up the Cluster AAD Identity in the **DataSource** blade of the **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="36ae0-158">Azure Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="36ae0-159">[Azure 포털](http://portal.azure.com)에서 ADLA 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-159">Create an ADLA account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="36ae0-160">자세한 내용은 [자습서: Azure 포털을 사용하여 Azure Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="36ae0-162">Azure Blob 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="36ae0-163">[Azure 포털](http://portal.azure.com)에서 Azure Blob 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-163">Create an Azure Blob storage account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="36ae0-164">자세한 내용은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)의 저장소 계정 만들기 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-164">For details, see the Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="36ae0-166">Azure 기계 학습 스튜디오 계정 설정</span><span class="sxs-lookup"><span data-stu-id="36ae0-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="36ae0-167">[Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 페이지에서 Azure 기계 학습 스튜디오를 등록/로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-167">Sign up/into Azure Machine Learning Studio from the [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="36ae0-168">**지금 시작** 단추를 클릭한 후 "무료 작업 영역" 또는 "표준 작업 영역"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-168">Click on the **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="36ae0-169">그런 다음 Azure 기계 학습 스튜디오에서 실험을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-169">After this you will be able to create experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="36ae0-170">Azure Data Lake 도구 설치[권장]</span><span class="sxs-lookup"><span data-stu-id="36ae0-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="36ae0-171">[Visual Studio용 Azure Data Lake 도구](https://www.microsoft.com/download/details.aspx?id=49504)에서 사용 중인 Visual Studio 버전에 대한 Azure Data Lake 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="36ae0-173">설치가 성공적으로 완료되었으면 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-173">After the installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="36ae0-174">위쪽 메뉴에 Data Lake 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-174">You should see the Data Lake tab the menu at the top.</span></span> <span data-ttu-id="36ae0-175">Azure 리소스는 Azure 계정에 로그인하면 왼쪽 패널에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-175">Your Azure resources should appear in the left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="the-nyc-taxi-trips-dataset"></a><span data-ttu-id="36ae0-177">NYC Taxi Trips 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="36ae0-177">The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="36ae0-178">여기에 사용된 데이터 집합은 공개적으로 제공되는 데이터 집합인 [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/)데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-178">The data set we used here is a publicly available dataset -- the [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="36ae0-179">NYC Taxi Trip 데이터는 1억 7,300만 개가 넘는 개별 여정 및 각 여정의 요금으로 기록된 약 20GB의 압축된 CSV 파일(압축되지 않은 경우 약 48GB)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-179">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="36ae0-180">각 여정 레코드는 승차 및 하차 위치, 익명 처리된 hack(기사) 면허증 번호 및 medallion(택시의 고유 ID) 번호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-180">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="36ae0-181">데이터는 2013년의 모든 여정을 포괄하며, 매월 다음 두 개의 데이터 집합으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-181">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

* <span data-ttu-id="36ae0-182">'trip_data' CSV는 승객 수, 승차 및 하차 지점, 여정 기간, 여정 거리 등 여정 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-182">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="36ae0-183">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="36ae0-184">'trip_fare' CSV는 지불 유형, 금액, 추가 요금 및 세금, 팁 및 통행료, 총 지불 금액 등 각 여정의 요금에 대한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-184">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="36ae0-185">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="36ae0-186">trip\_data와 trip\_fare를 조인할 고유 키는 medallion, hack\_licence 및 pickup\_datetime이라는 세 가지 필드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-186">The unique key to join trip\_data and trip\_fare is composed of the following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="36ae0-187">공용 Azure 저장소 Blob에서 원시 CSV 파일을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-187">The raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="36ae0-188">이 조인에 대한 U-SQL 스크립트는 [trip 및 fare 테이블 조인](#join) 섹션에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-188">The U-SQL script for this join is in the [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="36ae0-189">U-SQL로 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="36ae0-189">Process data with U-SQL</span></span>
<span data-ttu-id="36ae0-190">이 섹션에서 설명하는 데이터 처리 작업에는 데이터 수집, 품질 검사, 탐색 및 샘플링이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-190">The data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling the data.</span></span> <span data-ttu-id="36ae0-191">또한 trip 및 fare 테이블을 조인하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-191">We also show how to join trip and fare tables.</span></span> <span data-ttu-id="36ae0-192">마지막 섹션에서는 Azure 포털에서 U-SQL 스크립트 작업을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-192">The final section shows run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="36ae0-193">각 하위 섹션에 대한 링크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-193">Here are links to each subsection:</span></span>

* [<span data-ttu-id="36ae0-194">데이터 수집: 공용 Blob에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="36ae0-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="36ae0-195">데이터 품질 검사</span><span class="sxs-lookup"><span data-stu-id="36ae0-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="36ae0-196">데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="36ae0-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="36ae0-197">trip 및 fare 테이블 조인</span><span class="sxs-lookup"><span data-stu-id="36ae0-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="36ae0-198">데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="36ae0-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="36ae0-199">U-SQL 작업 실행</span><span class="sxs-lookup"><span data-stu-id="36ae0-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="36ae0-200">U-SQL 스크립트는 여기서 설명하고 별도의 파일로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-200">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="36ae0-201">**GitHub** 에서 전체 [U-SQL 스크립트](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-201">You can download the full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="36ae0-202">U-SQL을 실행하려면 Visual Studio를 열고 **파일 --> 새로 만들기 --> 프로젝트**를 클릭한 후 **U-SQL 프로젝트**를 선택하고 이름을 지정하고 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-202">To execute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it to a folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="36ae0-204">Visual Studio 대신 Azure 포털을 사용하여 U-SQL을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-204">It is possible to use the Azure Portal to execute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="36ae0-205">포털에서 Azure Data Lake 분석 리소스로 이동한 후 다음 그림과 같이 쿼리를 직접 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-205">You can navigate to the Azure Data Lake Analytics resource on the portal and submit queries directly as illustrated in the following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="36ae0-207"><a name="ingest"></a>데이터 수집: 공용 Blob에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="36ae0-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="36ae0-208">Azure Blob에서 데이터 위치는 **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**으로 참조되고 **Extractors.Csv()**를 사용하여 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-208">The location of the data in the Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="36ae0-209">다음 스크립트에서 wasb 주소의 container_name@blob_storage_account_name에 대한 사용자 고유 컨테이너 이름과 저장소 계정 이름을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in the wasb address.</span></span> <span data-ttu-id="36ae0-210">파일 이름은 같은 형식이므로 12개 trip 파일을 모두 읽는 데 **trip\_data_{\*\}.csv**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-210">Since the file names are in same format, we can use **trip\_data_{\*\}.csv** to read in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="36ae0-211">첫 번째 행에 헤더가 있으므로 헤더를 제거하고 열 형식을 적절하게 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-211">Since there are headers in the first row, we need to remove the headers and change column types into appropriate ones.</span></span> <span data-ttu-id="36ae0-212">처리된 데이터를 **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_를 사용하여 Azure Data Lake 저장소에 저장하거나 **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**를 사용하여 Azure Blob Storage 계정에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-212">We can either save the processed data to Azure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or to Azure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data to ADL
    OUTPUT @trip   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data to blob
    OUTPUT @trip   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="36ae0-213">마찬가지로 fare 데이터 집합에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-213">Similarly we can read in the fare data sets.</span></span> <span data-ttu-id="36ae0-214">Azure Data Lake Store를 마우스 오른쪽 단추로 클릭하고 **Azure Portal --> 데이터 탐색기** 또는 Visual Studio 내 **파일 탐색기**에서 데이터를 살펴보도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-214">Right click Azure Data Lake Store, you can choose to look at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="36ae0-217"><a name="quality"></a>데이터 품질 검사</span><span class="sxs-lookup"><span data-stu-id="36ae0-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="36ae0-218">Trip 및 fare 테이블을 읽은 후 다음과 같은 방식으로 데이터 품질 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-218">After trip and fare tables have been read in, data quality checks can be done in the following way.</span></span> <span data-ttu-id="36ae0-219">결과 CSV 파일은 Azure Blob 저장소 또는 Azure Data Lake 저장소에 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-219">The resulting CSV files can be output to Azure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="36ae0-220">medallion 수와 medallion의 고유 번호를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-220">Find the number of medallions and unique number of medallions:</span></span>

    ///check the number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="36ae0-221">여정(trip)이 100개가 넘는 medallion을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="36ae0-222">pickup_longitude 조건으로 유효하지 않은 레코드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="36ae0-223">일부 변수에 대해 누락된 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="36ae0-224"><a name="explore"></a>데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="36ae0-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="36ae0-225">데이터를 잘 이해하기 위해 몇 가지 데이터 탐색을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-225">We can do some data exploration to get a better understanding of the data.</span></span>

<span data-ttu-id="36ae0-226">왕복 및 비왕복 여정의 분포를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-226">Find the distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="36ae0-227">0, 5, 10, 20달러의 제한 값을 가진 팁 금액의 분포를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-227">Find the distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="36ae0-228">여정 거리의 기본 통계를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="36ae0-229">여정 거리의 백분위수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-229">Find the percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="36ae0-230"><a name="join"></a>trip 및 fare 테이블 조인</span><span class="sxs-lookup"><span data-stu-id="36ae0-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="36ae0-231">medallion, hack_license 및 pickup_time으로 trip 및 fare 테이블을 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output to blob
    OUTPUT @model_data_full   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data to ADL
    OUTPUT @model_data_full   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="36ae0-232">각 승객 수 수준에 대해 레코드 수, 평균 팁 금액, 팁 금액의 분산, 왕복 여정의 백분율을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-232">For each level of passenger count, calculate the number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="36ae0-233"><a name="sample"></a>데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="36ae0-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="36ae0-234">먼저 조인된 테이블에서 0.1%의 데이터를 임의로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-234">First we randomly select 0.1% of the data from the joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="36ae0-235">다음으로 이진 변수 tip_class로 계층화된 샘플링을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output to blob
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data to ADL
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="36ae0-236"><a name="run"></a>U-SQL 작업 실행</span><span class="sxs-lookup"><span data-stu-id="36ae0-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="36ae0-237">U-SQL 스크립트 편집을 마치면 Azure Data Lake 분석 계정을 사용하여 서버에 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-237">When you finish editing U-SQL scripts, you can submit them to the server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="36ae0-238">**Data Lake**, **작업 제출**을 클릭하고 **분석 계정**, **병렬 처리**를 선택하고 **제출** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="36ae0-240">작업이 성공적으로 컴파일되면 모니터링을 위해 작업 상태가 Visual Studio에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-240">When the job is complied successfully, the status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="36ae0-241">작업 실행을 완료한 후에는 작업 실행 프로세스를 재생하여 병목 단계를 파악하고 작업 효율성을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-241">After the job finishes running, you can even replay the job execution process and find out the bottleneck steps to improve your job efficiency.</span></span> <span data-ttu-id="36ae0-242">또한 Azure 포털로 이동하여 U-SQL 작업의 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-242">You can also go to Azure Portal to check the status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="36ae0-245">이제 Azure Blob 저장소 또는 Azure 포털에서 출력 파일을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-245">Now you can check the output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="36ae0-246">다음 단계에서 모델링을 위한 계층화된 샘플 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-246">We will use the stratified sample data for our modeling in the next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="36ae0-249">Azure 기계 학습에서 모델 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="36ae0-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="36ae0-250">Azure 기계 학습으로 데이터를 끌어와 빌드 및 배포하기 위한 두 가지 옵션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-250">We demonstrate two options available for you to pull data into Azure Machine Learning to build and</span></span> 

* <span data-ttu-id="36ae0-251">첫 번째 옵션에서는 Azure Blob에 기록된 샘플링된 데이터를 사용하고(위의 **데이터 샘플링** 단계에서) 모델을 빌드하고 Azure 기계 학습에 배포하는 데 Python을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-251">In the first option, you use the sampled data that has been written to an Azure Blob (in the **Data sampling** step above) and use Python to build and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="36ae0-252">두 번째 옵션에서는 Hive 쿼리를 사용하여 Azure Data Lake의 데이터를 직접 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-252">In the second option, you query the data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="36ae0-253">이 옵션에서는 새 HDInsight 클러스터를 만들거나 Hive 테이블이 Azure Data Lake 저장소의 NY 택시 데이터를 가리키는 기존 HDInsight 클러스터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where the Hive tables point to the NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="36ae0-254">아래의 두 옵션을 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-to-build-and-deploy-machine-learning-models"></a><span data-ttu-id="36ae0-255">옵션 1: Python을 사용하여 기계 학습 모델 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="36ae0-255">Option 1: Use Python to build and deploy machine learning models</span></span>
<span data-ttu-id="36ae0-256">Python을 사용하여 기계 학습 모델을 빌드 및 배포하려면 로컬 컴퓨터에서 또는 Azure 기계 학습 스튜디오에서 Jupyter Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-256">To build and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="36ae0-257">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)에 제공된 Jupyter Notebook에는 데이터 탐색 및 시각화, 기능 엔지니어링, 모델링 및 배포를 위한 전체 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-257">The Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains the full code to explore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="36ae0-258">이 문서에서는 모델링 및 배포 단계만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-258">In this article, we show just the modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="36ae0-259">Python 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="36ae0-259">Import Python libraries</span></span>
<span data-ttu-id="36ae0-260">샘플 Jupyter Notebook 또는 Python 스크립트 파일을 실행하기 위해 다음 Python 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-260">In order to run the sample Jupyter Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="36ae0-261">AzureML Notebook 서비스를 사용하는 경우 이러한 패키지는 미리 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-261">If you are using the AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-the-data-from-blob"></a><span data-ttu-id="36ae0-262">Blob에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="36ae0-262">Read in the data from blob</span></span>
* <span data-ttu-id="36ae0-263">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="36ae0-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="36ae0-264">텍스트로 읽기</span><span class="sxs-lookup"><span data-stu-id="36ae0-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds to read in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="36ae0-266">열 이름 추가 및 열 구분</span><span class="sxs-lookup"><span data-stu-id="36ae0-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="36ae0-267">일부 열을 숫자로 변경</span><span class="sxs-lookup"><span data-stu-id="36ae0-267">Change some columns to numeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="36ae0-268">기계 학습 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="36ae0-268">Build machine learning models</span></span>
<span data-ttu-id="36ae0-269">여기서는 여정에서 팁을 받는지 여부를 예측하는 이진 분류 모델을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-269">Here we build a binary classification model to predict whether a trip is tipped or not.</span></span> <span data-ttu-id="36ae0-270">Jupyter Notebook에서 다중 클래스 분류 및 회귀 모델이라는 다른 두 모델을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-270">In the Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="36ae0-271">먼저 scikit-learn 모델에 사용할 수 있는 더미 변수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-271">First we need to create dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="36ae0-272">모델링을 위한 데이터 프레임 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-272">Create data frame for the modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="36ae0-273">학습 및 테스트 60-40분할</span><span class="sxs-lookup"><span data-stu-id="36ae0-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="36ae0-274">학습 집합에서 로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="36ae0-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="36ae0-275">테스트 데이터 집합 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="36ae0-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="36ae0-276">평가 메트릭 계산</span><span class="sxs-lookup"><span data-stu-id="36ae0-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="36ae0-277">웹 서비스 API 구축 및 Python에서 사용</span><span class="sxs-lookup"><span data-stu-id="36ae0-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="36ae0-278">기계 학습 모델을 빌드한 후 운영하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-278">We want to operationalize the machine learning model after it has been built.</span></span> <span data-ttu-id="36ae0-279">여기서는 예로 이진 로지스틱 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-279">Here we use the binary logistic model as an example.</span></span> <span data-ttu-id="36ae0-280">로컬 컴퓨터에서 scikit-learn 버전이 0.15.1인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-280">Make sure the scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="36ae0-281">Azure 기계 학습 스튜디오 서비스를 사용하는 경우에는 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-281">You don't have to worry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="36ae0-282">Azure 기계 학습 스튜디오 설정에서 작업 영역 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="36ae0-283">Azure Machine Learning 스튜디오에서 **설정** --> **이름** --> **권한 부여 토큰**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="36ae0-285">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="36ae0-286">웹 서비스 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="36ae0-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="36ae0-287">웹 서비스 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-287">Call Web service API.</span></span> <span data-ttu-id="36ae0-288">이전 단계를 수행한 후 5~10초 정도 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-288">You have to wait 5-10 seconds after the previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="36ae0-289">옵션 2: Azure 기계 학습에서 모델을 만들고 직접 배포</span><span class="sxs-lookup"><span data-stu-id="36ae0-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="36ae0-290">Azure 기계 학습 스튜디오에서는 Azure Data Lake 저장소에서 직접 데이터를 읽고 모델을 만들며 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used to create and deploy models.</span></span> <span data-ttu-id="36ae0-291">이 방식에서는 Azure Data Lake 저장소를 가리키는 Hive 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-291">This approach uses a Hive table that points at the Azure Data Lake Store.</span></span> <span data-ttu-id="36ae0-292">이를 위해 Hive 테이블이 만들어지는 별도의 Azure HDInsight 클러스터를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-292">This requires that a separate Azure HDInsight cluster be provisioned, on which the Hive table is created.</span></span> <span data-ttu-id="36ae0-293">다음 섹션에서는 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-293">The following sections show how to do this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="36ae0-294">HDInsight Linux 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="36ae0-295">[Azure Portal](http://portal.azure.com)에서 HDInsight 클러스터(Linux)를 만듭니다. 자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)의 **Azure Data Lake Store에 액세스할 수 있는 HDInsight 클러스터 만들기** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-295">Create an HDInsight Cluster (Linux) from the [Azure Portal](http://portal.azure.com).For details, see the **Create an HDInsight cluster with access to Azure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="36ae0-297">HDInsight에서 Hive 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="36ae0-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="36ae0-298">이제 이전 단계에서 Azure Data Lake 저장소에 저장한 데이터를 사용하여 Azure 기계 학습 스튜디오에서 사용할 Hive 테이블을 HDInsight 클러스터에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-298">Now we create Hive tables to be used in Azure Machine Learning Studio in the HDInsight cluster using the data stored in Azure Data Lake Store in the previous step.</span></span> <span data-ttu-id="36ae0-299">방금 만든 HDInsight 클러스터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-299">Go to the HDInsight cluster just created.</span></span> <span data-ttu-id="36ae0-300">**설정** --> **속성** --> **클러스터 AAD ID** --> **ADLS 액세스**를 클릭하고 Azure Data Lake Store 계정이 읽기, 쓰기 및 실행 권한이 있는 목록에 추가되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in the list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="36ae0-302">그런 다음 **설정** 단추 옆의 **대시보드**를 클릭하면 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-302">Then click **Dashboard** next to the **Settings** button and a window will pop up.</span></span> <span data-ttu-id="36ae0-303">페이지의 오른쪽 위 모서리에서 **Hive 보기**를 클릭하면 **쿼리 편집기**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-303">Click **Hive View** in the upper right corner of the page and you will see the **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="36ae0-306">다음 Hive 스크립트를 붙여 넣어 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-306">Paste in the following Hive scripts to create a table.</span></span> <span data-ttu-id="36ae0-307">데이터 원본은 다음 방식으로 Azure Data Lake Store 참조에 위치합니다. **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**</span><span class="sxs-lookup"><span data-stu-id="36ae0-307">The location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="36ae0-308">쿼리 실행이 끝나면 다음과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-308">When the query finishes running, you will see the results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="36ae0-310">Azure 기계 학습 스튜디오에서 모델 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="36ae0-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="36ae0-311">이제 팁이 Azure 기계 학습에서 유료인지 여부를 예측하는 모델을 빌드 및 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-311">We are now ready to build and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="36ae0-312">계층화된 샘플 데이터는 이 이진 분류(팁인지 아닌지) 문제에서 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-312">The stratified sample data is ready to be used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="36ae0-313">다중 클래스 분류(tip_class) 및 회귀(tip_amount)를 사용하는 예측 모델은 Azure 기계 학습 스튜디오를 사용하여 빌드 및 배포할 수도 있지만 여기에서는 이진 분류 모델을 사용하여 사례를 처리하는 방법만 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-313">The predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how to handle the case using the binary classification model.</span></span>

1. <span data-ttu-id="36ae0-314">**데이터 입력 및 출력** 섹션에서 제공되는 **데이터 가져오기** 모듈을 사용하여 Azure ML로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-314">Get the data into Azure ML using the **Import Data** module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="36ae0-315">자세한 내용은 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 참조 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36ae0-315">For more information, see the [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="36ae0-316">**속성** 패널에서 **데이터 원본**으로 **Hive 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-316">Select **Hive Query** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="36ae0-317">다음 Hive 스크립트를 **Hive 데이터베이스 쿼리** 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-317">Paste the following Hive script in the **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="36ae0-318">HDInsight 클러스터의 URI(Azure 포털에서 찾을 수 있음), Hadoop 자격 증명, 출력 데이터의 위치, Azure 저장소 계정 이름/키/컨테이너 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-318">Enter the URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="36ae0-320">아래 그림은 Hive 테이블에서 데이터를 읽는 이진 분류 실험 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-320">An example of a binary classification experiment reading data from Hive table is shown in the figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="36ae0-322">실험을 만든 후 **웹 서비스 설정** --> **예측 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-322">After the experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="36ae0-324">자동으로 생성된 점수 매기기 실험을 실행하고 완료되었으면 **웹 서비스 배포**</span><span class="sxs-lookup"><span data-stu-id="36ae0-324">Run the automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="36ae0-326">웹 서비스 대시보드가 바로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-326">The web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="36ae0-328">요약</span><span class="sxs-lookup"><span data-stu-id="36ae0-328">Summary</span></span>
<span data-ttu-id="36ae0-329">이 연습을 완료하면서 Azure Data Lake에서 확장성 있는 종단 간 솔루션을 구축하기 위한 데이터 과학 환경을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="36ae0-330">이 환경은 모델 학습을 통한 데이터 획득부터 웹 서비스로 모델 배포에 이르는 데이터 과학 프로세스의 정식 단계를 통해 가져온 대형 공용 데이터 집합을 분석하는 데 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-330">This environment was used to analyze a large public dataset, taking it through the canonical steps of the Data Science Process, from data acquisition through model training, and then to the deployment of the model as a web service.</span></span> <span data-ttu-id="36ae0-331">U-SQL은 이러한 데이터를 처리하고 탐색하며 샘플링하는 데 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-331">U-SQL was used to process, explore and sample the data.</span></span> <span data-ttu-id="36ae0-332">Python 및 Hive는 Azure 기계 학습 스튜디오에서 예측 모델을 빌드하고 배포하는 데 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-332">Python and Hive were used with Azure Machine Learning Studio to build and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="36ae0-333">다음 작업</span><span class="sxs-lookup"><span data-stu-id="36ae0-333">What's next?</span></span>
<span data-ttu-id="36ae0-334">[TDSP(팀 데이터 과학 프로세스)](http://aka.ms/datascienceprocess) 에 대한 학습 경로는 고급 분석 프로세스의 각 단계를 설명하는 토픽에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-334">The learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links to topics describing each step in the advanced analytics process.</span></span> <span data-ttu-id="36ae0-335">다양한 예측 분석 시나리오에서 리소스 및 서비스를 사용하는 방법을 소개하는 [팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md) 페이지에는 일련의 연습 과정이 항목별로 정리되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36ae0-335">There are a series of walkthroughs itemized on the [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how to use resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="36ae0-336">실행 중인 팀 데이터 과학 프로세스: SQL 데이터 웨어하우스 사용</span><span class="sxs-lookup"><span data-stu-id="36ae0-336">The Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="36ae0-337">실행 중인 팀 데이터 과학 프로세스: HDInsight Hadoop 클러스터 사용</span><span class="sxs-lookup"><span data-stu-id="36ae0-337">The Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="36ae0-338">팀 데이터 과학 프로세스: SQL Server 사용</span><span class="sxs-lookup"><span data-stu-id="36ae0-338">The Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="36ae0-339">Azure HDInsight에서 Spark를 사용하는 데이터 과학 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="36ae0-339">Overview of the Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

