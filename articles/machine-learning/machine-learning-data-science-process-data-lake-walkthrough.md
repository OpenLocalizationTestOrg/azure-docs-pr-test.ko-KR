---
title: "Azure Data Lake를 사용한 확장성 있는 데이터 과학: 종단 간 연습 | Microsoft Docs"
description: "방식과 toouse Azure 데이터 레이크 toodo 데이터 탐색 및 이진 분류에는 데이터 집합 작업 합니다."
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
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="d6b31-103">Azure Data Lake를 사용한 확장성 있는 데이터 과학: 종단 간 연습</span><span class="sxs-lookup"><span data-stu-id="d6b31-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="d6b31-104">이 연습에서는 어떻게 toouse Azure 데이터 레이크 toodo 데이터 탐색 및 hello NYC의 샘플에 있는 이진 분류 작업 택시 여행 및 요금 데이터 집합 toopredict 팁 요금을 지불 합니다 여부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="d6b31-105">Hello hello 단계가 안내 합니다 [팀 데이터 과학 프로세스](http://aka.ms/datascienceprocess), 최종 데이터 취득 toomodel 학습 한 다음 toohello 배포 hello 모델을 게시 하는 웹 서비스의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="d6b31-106">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="d6b31-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="d6b31-107">hello [Microsoft Azure 데이터 레이크](https://azure.microsoft.com/solutions/data-lake/) 모든 hello 기능 필수 toomake에 쉽게의 고급 컴퓨터 학습 모델링 및 분석, 크기, 모양 및 속도 tooconduct 데이터 처리, 데이터 과학자 toostore 데이터에 대 한 비용 효율적인 방식으로 높은 확장성와.</span><span class="sxs-lookup"><span data-stu-id="d6b31-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="d6b31-108">데이터가 실제로 처리되는 경우에만 작업 단위로 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="d6b31-109">혼합 hello와 C# tooprovide 확장 가능한의 역대 hello SQL의 선언적 특성을 언어 분산 쿼리 기능, azure Data Lake 분석 U-SQL 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="d6b31-110">Tooprocess 수 구조화 되지 않은 데이터 읽기의 경우 스키마를 적용 하 여 사용자 지정 논리를 삽입 하 고 사용자 정의 함수 (Udf) 작성과 확장성 tooenable 미세 하 게 제어할 방법 배율로 tooexecute 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="d6b31-111">toolearn U SQL 뒤 hello 디자인 원칙에 대 한 자세한 참조 [Visual Studio 블로그 게시물](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="d6b31-112">Data Lake 분석은 또한 Cortana Analytics Suite에서 핵심적인 부분으로, Azure SQL 데이터 웨어하우스, Power BI 및 Data Factory와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="d6b31-113">이렇게 전체 클라우드 빅 데이터 및 고급 분석 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="d6b31-114">이 연습에서는 먼저 hello 필수 구성 요소 및 리소스를 필요한 toocomplete hello hello 데이터 과학 프로세스를 구성 하는 데이터 레이크 분석을 사용 하 여 작업 방법 등에 tooinstall 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="d6b31-115">U-SQL를 사용 하 여 hello 데이터 처리 단계를 간략하게 설명 하 고 표시 하 여 결론을 내립니다 방법을 toouse Python, Azure 기계 학습 스튜디오 toobuild와 하이브 및 hello 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="d6b31-116">U-SQL 및 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6b31-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="d6b31-117">이 연습에서는 Visual Studio tooedit U-SQL 스크립트 tooprocess hello 데이터 집합을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="d6b31-118">hello U-SQL 스크립트 여기에서 설명 되며 별도 파일에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="d6b31-119">hello 프로세스 수집 하는 방법, 탐색 및 샘플링 hello 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="d6b31-120">또한 U SQL toorun hello Azure 포털에서에서 작업을 스크립팅 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="d6b31-121">Hello 데이터 연결 된 HDInsight 클러스터 toofacilitate hello 빌드 및 Azure 기계 학습 스튜디오에서 이진 분류 모델의 배포에 대 한 하이브 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="d6b31-122">Python</span><span class="sxs-lookup"><span data-stu-id="d6b31-122">Python</span></span>
<span data-ttu-id="d6b31-123">이 연습에 표시 하는 섹션도 포함 되어 있습니다 어떻게 toobuild Python을 사용 하 여 Azure 기계 학습 스튜디오와 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="d6b31-124">이 프로세스에서 이러한 단계에 대 한 Jupyter 노트북 hello Python 스크립트 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="d6b31-125">hello 노트북 몇 가지 추가 기능 엔지니어링 단계 및 다중 클래스 분류 및 회귀 모델링 또한 여기에 설명 된 toohello 이진 분류 모델 같은 모델 생성에 대 한 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="d6b31-126">hello 회귀 작업은 다른 팁 기능을 기반으로 하는 hello 팁의 toopredict hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="d6b31-127">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="d6b31-127">Azure Machine Learning</span></span>
<span data-ttu-id="d6b31-128">Azure 기계 학습 스튜디오는 사용 되는 toobuild 하 고 hello 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="d6b31-129">이러한 작업은 먼저 Python 스크립트를 사용한 다음 HDInsight(Hadoop) 클러스터의 Hive 테이블을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="d6b31-130">스크립트</span><span class="sxs-lookup"><span data-stu-id="d6b31-130">Scripts</span></span>
<span data-ttu-id="d6b31-131">만 hello 주요 단계는이 연습에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="d6b31-132">Hello 전체를 다운로드할 수 있습니다 **U-SQL 스크립트** 및 **Jupyter 노트북** 에서 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b31-133">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d6b31-133">Prerequisites</span></span>
<span data-ttu-id="d6b31-134">이러한 항목을 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="d6b31-135">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d6b31-135">An Azure subscription.</span></span> <span data-ttu-id="d6b31-136">아직 가지고 있지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b31-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d6b31-137">[권장] Visual Studio 2013 이상.</span><span class="sxs-lookup"><span data-stu-id="d6b31-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="d6b31-138">아직 이러한 버전이 설치되지 않은 경우 [Visual Studio Community](https://www.visualstudio.com/vs/community/)에서 무료로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="d6b31-139">Visual Studio 대신 hello Azure 포털 toosubmit Azure 데이터 레이크 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="d6b31-140">지침에 어떻게 toodo 하므로 hello 섹션의 hello 포털 및 Visual Studio와 함께 모두 이라는 제공할 것 **U-SQL를 사용 하 여 데이터를 처리할**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="d6b31-141">Azure Data Lake에 대한 데이터 과학 환경 준비</span><span class="sxs-lookup"><span data-stu-id="d6b31-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="d6b31-142">이 연습에서는 tooprepare hello 데이터 과학 환경 hello 다음 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="d6b31-143">Azure Data Lake 저장소(ADLS)</span><span class="sxs-lookup"><span data-stu-id="d6b31-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="d6b31-144">Azure Data Lake 분석(ADLA)</span><span class="sxs-lookup"><span data-stu-id="d6b31-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="d6b31-145">Azure Blob 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="d6b31-145">Azure Blob storage account</span></span>
* <span data-ttu-id="d6b31-146">Azure 기계 학습 스튜디오 계정</span><span class="sxs-lookup"><span data-stu-id="d6b31-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="d6b31-147">Visual Studio용 Azure Data Lake 도구(권장)</span><span class="sxs-lookup"><span data-stu-id="d6b31-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="d6b31-148">이 섹션 방법에 대해 설명 각 toocreate 이러한 리소스 중입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="d6b31-149">Toouse와 Azure 기계 학습 Python, toobuild 모델 대신 하이브 테이블을 선택할 경우 tooprovision (Hadoop) HDInsight 클러스터 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="d6b31-150">아래 hello 적절 한 섹션에서이 대체 절차에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="d6b31-151">hello **Azure 데이터 레이크 저장소** 또는 만들 수 있습니다 하나 별도로 hello를 만들 때 **Azure 데이터 레이크 분석** hello 기본 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="d6b31-152">각 별도로 아래 이러한 리소스를 만들기 위한 지침 참조 하지만 hello 데이터 레이크 저장소 계정 별도로 만들 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="d6b31-153">Azure 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="d6b31-154">ADLS hello에서 만들 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="d6b31-155">자세한 내용은 [Azure 포털을 사용하여 Data Lake 저장소로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b31-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="d6b31-156">Hello에 클러스터 AAD Id hello 있는지 tooset 수 **DataSource** hello의 블레이드에서 **옵션 구성** 블레이드 설명 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="d6b31-158">Azure Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="d6b31-159">Hello에서 ADLA 계정 만들기 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="d6b31-160">자세한 내용은 [자습서: Azure 포털을 사용하여 Azure Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b31-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="d6b31-162">Azure Blob 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="d6b31-163">Hello에서 Azure Blob 저장소 계정 만들기 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="d6b31-164">자세한 내용은 hello 만들기 저장소 계정 섹션을 참조 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="d6b31-166">Azure 기계 학습 스튜디오 계정 설정</span><span class="sxs-lookup"><span data-stu-id="d6b31-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="d6b31-167">Hello에서 등록/Azure 기계 학습 스튜디오에 로그인 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 페이지.</span><span class="sxs-lookup"><span data-stu-id="d6b31-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="d6b31-168">Hello 클릭 **지금 시작** 단추를 선택한 다음 "가능한 작업 영역" 또는 "표준 작업 영역"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="d6b31-169">그러면 Azure 기계 학습 스튜디오에서 실험 수 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="d6b31-170">Azure Data Lake 도구 설치[권장]</span><span class="sxs-lookup"><span data-stu-id="d6b31-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="d6b31-171">[Visual Studio용 Azure Data Lake 도구](https://www.microsoft.com/download/details.aspx?id=49504)에서 사용 중인 Visual Studio 버전에 대한 Azure Data Lake 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="d6b31-173">Hello 설치가 성공적으로 완료 되 면 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="d6b31-174">Hello 데이터 레이크 탭 hello 메뉴 hello 위쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="d6b31-175">Azure 리소스는 Azure 계정에 로그인 할 때 hello 왼쪽된 패널에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="d6b31-177">hello NYC 택시 Trips 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="d6b31-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="d6b31-178">hello 여기에 데이터 집합은 공개적으로 사용할 수 있는 데이터 집합-hello [NYC 택시 Trips dataset](http://www.andresmh.com/nyctaxitrips/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="d6b31-179">hello NYC 택시 여행 데이터 약 20GB의 압축 된 CSV 파일 (~ 48 GB 압축 되지 않음)로, 기록을 173 백만 개 이상의 개별 라운드트립 및 hello fares 각 시에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="d6b31-180">Hello 픽업 및 자동 전송 위치를 포함 하는 각 여행 레코드 및 익명으로 처리 하는 시간 (드라이버의) 라이선스 번호 해킹 및 hello 메달 (택시의 고유 id) 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="d6b31-181">hello 데이터 hello 2013 년의 모든 왕복에 설명 하 고 각 월에 대 한 두 개의 데이터 집합을 따라 hello에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="d6b31-182">hello 'trip_data' CSV 승객, 픽업 및 dropoff 포인트, 여행 기간 및 여행 길이 수와 같이 여행 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="d6b31-183">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="d6b31-184">hello 'trip_fare' CSV hello 요금을 지불 유형, 요금 크기, 추가 요금 및 세금, 팁 및 통행료가, 및 유료 hello 총 금액 등 각 여정에 대해 지불한의 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="d6b31-185">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="d6b31-186">hello 고유 키 toojoin 여행\_데이터와 여행\_요금은 다음 세 개의 필드가 hello 이루어져: 메달 해킹\_라이선스 및 픽업\_날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="d6b31-187">hello 원시 CSV 파일을 공용 Azure 저장소 blob에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="d6b31-188">U-SQL 스크립트를이 조인은 hello에 대 한 hello [여행 및 요금 테이블을 조인](#join) 섹션.</span><span class="sxs-lookup"><span data-stu-id="d6b31-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="d6b31-189">U-SQL로 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="d6b31-189">Process data with U-SQL</span></span>
<span data-ttu-id="d6b31-190">이 섹션에서 설명 하는 hello 데이터 처리 작업에 수집 하는 방법, 품질 확인, 탐색 및 샘플링 hello 데이터 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="d6b31-191">또한 어떻게 toojoin 여행 및 요금 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="d6b31-192">hello 최종 섹션 hello Azure 포털에서에서 U-SQL 스크립트를 사용한 작업 실행 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="d6b31-193">다음 링크를 tooeach 하위 섹션은:</span><span class="sxs-lookup"><span data-stu-id="d6b31-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="d6b31-194">데이터 수집: 공용 Blob에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="d6b31-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="d6b31-195">데이터 품질 검사</span><span class="sxs-lookup"><span data-stu-id="d6b31-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="d6b31-196">데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="d6b31-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="d6b31-197">trip 및 fare 테이블 조인</span><span class="sxs-lookup"><span data-stu-id="d6b31-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="d6b31-198">데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="d6b31-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="d6b31-199">U-SQL 작업 실행</span><span class="sxs-lookup"><span data-stu-id="d6b31-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="d6b31-200">hello U-SQL 스크립트 여기에서 설명 되며 별도 파일에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="d6b31-201">Hello 전체를 다운로드할 수 있습니다 **U-SQL 스크립트** 에서 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="d6b31-202">tooexecute U-SQL을 열고 Visual Studio를 클릭 하 여 **파일-새로 만들기-> 프로젝트를-->**, 선택 **U-SQL 프로젝트**, 이름을 지정 하 고 tooa 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="d6b31-204">Visual Studio 대신 가능한 toouse hello Azure 포털 tooexecute U-SQL 것합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="d6b31-205">Hello 포털에서 toohello Azure Data Lake 분석 리소스를 탐색할 수 있으며 직접 hello 다음 그림에에서 나온 것 처럼 쿼리를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="d6b31-207"><a name="ingest"></a>데이터 수집: 공용 Blob에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="d6b31-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="d6b31-208">hello Azure blob에에서 hello 데이터의 hello 위치 참조  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  를 사용 하 여 추출할 수 있습니다 및 **Extractors.Csv()**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="d6b31-209">대신 사용자 고유의 컨테이너 이름 및 저장소 계정 이름에 대 한 다음 스크립트의 container_name@blob_storage_account_name hello wasb 주소에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="d6b31-210">Hello 파일 이름은 같은 형식 이므로 사용할 수 **여행\_데이터 {\*\}.csv** tooread 모든 12 여행 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

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

<span data-ttu-id="d6b31-211">Hello 첫 번째 행에 머리글 때문 tooremove hello 헤더 및 필요를 적절 한 시나리오로 열 형식을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="d6b31-212">처리 하는 hello tooAzure 데이터 레이크 저장소 사용 하 여 데이터를 저장할 수도 있습니다 **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ 또는 tooAzure Blob 저장소를 사용 하 여 계정을  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="d6b31-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

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

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="d6b31-213">마찬가지로 hello 요금 데이터 집합에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="d6b31-214">마우스 오른쪽 단추로 클릭 하 여 Azure 데이터 레이크 저장소에서 데이터에 toolook를 선택할 수 있습니다, **Azure 포털-데이터 탐색기->** 또는 **파일 탐색기** Visual Studio 내에서.</span><span class="sxs-lookup"><span data-stu-id="d6b31-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="d6b31-217"><a name="quality"></a>데이터 품질 검사</span><span class="sxs-lookup"><span data-stu-id="d6b31-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="d6b31-218">여행 및 요금 테이블에서을 읽은 후 데이터 품질 확인 hello 방식으로 다음에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="d6b31-219">CSV 파일을 생성 하는 hello 출력 tooAzure Blob 저장소 또는 Azure 데이터 레이크 저장소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="d6b31-220">Medallions hello 수와 medallions의 고유한 번호 찾기:</span><span class="sxs-lookup"><span data-stu-id="d6b31-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d6b31-221">여정(trip)이 100개가 넘는 medallion을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d6b31-222">pickup_longitude 조건으로 유효하지 않은 레코드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d6b31-223">일부 변수에 대해 누락된 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-223">Find missing values for some variables:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="d6b31-224"><a name="explore"></a>데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="d6b31-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="d6b31-225">일부 데이터 탐색 tooget hello 데이터에 대해 더 자세히 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="d6b31-226">기울어진 및 비 위의 hello 배포를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-226">Find hello distribution of tipped and non-tipped trips:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d6b31-227">잘린 값을 가진 팁 금액의 hello 배포 찾기: 0,5,10, 및 20 달러입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d6b31-228">여정 거리의 기본 통계를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-228">Find basic statistics of trip distance:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="d6b31-229">여행 거리의 hello 백분위 수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="d6b31-230"><a name="join"></a>trip 및 fare 테이블 조인</span><span class="sxs-lookup"><span data-stu-id="d6b31-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="d6b31-231">medallion, hack_license 및 pickup_time으로 trip 및 fare 테이블을 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="d6b31-232">승객 수의 각 수준에 대해 레코드, 평균 팁 금액, 팁 금액의 차이, 크리스마스와의 백분율 hello 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="d6b31-233"><a name="sample"></a>데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="d6b31-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="d6b31-234">먼저 임의로 선택 hello 데이터의 0.1 %hello 조인 된 테이블에서:</span><span class="sxs-lookup"><span data-stu-id="d6b31-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

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
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d6b31-235">다음으로 이진 변수 tip_class로 계층화된 샘플링을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="d6b31-236"><a name="run"></a>U-SQL 작업 실행</span><span class="sxs-lookup"><span data-stu-id="d6b31-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="d6b31-237">U-SQL 스크립트 편집을 마치면 제출할 수 있습니다 이러한 Azure Data Lake 분석 계정을 사용 하 여 toohello 서버.</span><span class="sxs-lookup"><span data-stu-id="d6b31-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="d6b31-238">**Data Lake**, **작업 제출**을 클릭하고 **분석 계정**, **병렬 처리**를 선택하고 **제출** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="d6b31-240">Hello 작업은 성공적으로 컴파일, 하는 경우 작업의 hello 상태 모니터링을 위해 Visual Studio에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="d6b31-241">Hello 작업 실행을 완료 한 후에 재생 hello 작업 실행 프로세스를 수행할 수 있습니다 및 hello 확인 단계 tooimprove의 작업 효율을 보 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="d6b31-242">TooAzure U-SQL 작업의 포털 toocheck hello 상태를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="d6b31-245">이제 Azure Blob 저장소 또는 Azure 포털의 hello 출력 파일을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="d6b31-246">Hello 다음 단계에서 우리의 모델링에 대 한 층 화 hello 예제 데이터 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="d6b31-249">Azure 기계 학습에서 모델 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="d6b31-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="d6b31-250">두 개의 사용할 수 있는 옵션 toopull 데이터를 Azure 기계 학습 toobuild에 대해서도 설명 하 고</span><span class="sxs-lookup"><span data-stu-id="d6b31-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="d6b31-251">Hello 첫 번째 옵션을 사용 하 여 Azure Blob tooan 작성 된 hello 샘플링 된 데이터 (hello에 **데이터 샘플링** 위의 단계) 및 Python toobuild 사용 및 Azure 기계 학습에서 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="d6b31-252">Hello 두 번째 옵션에서 데이터를 쿼리할 hello Azure 데이터 레이크에서 하이브 쿼리를 사용 하 여 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="d6b31-253">이 옵션을 사용 하려면 새 HDInsight 클러스터를 만들거나 하이브 hello Azure 데이터 레이크 저장소의 지점 toohello NY 택시 데이터 테이블에 기존 HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="d6b31-254">아래의 두 옵션을 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="d6b31-255">옵션 1: Python 사용 toobuild 및 기계 학습 모델 배포</span><span class="sxs-lookup"><span data-stu-id="d6b31-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="d6b31-256">toobuild 및 Python을 사용 하는 기계 학습 모델을 배포, 로컬 컴퓨터에서 또는 Azure 기계 학습 스튜디오에서 Jupyter 노트북을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="d6b31-257">hello Jupyter 노트북에 제공 된 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) 포함 된 전체 코드 tooexplore hello, 데이터, 기능 엔지니어링, 모델링 및 배포를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="d6b31-258">이 문서에서는 hello 모델링 및 배포만 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="d6b31-259">Python 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="d6b31-259">Import Python libraries</span></span>
<span data-ttu-id="d6b31-260">순서 toorun hello 예제 Jupyter 노트북 또는 Python 스크립트 파일을 hello, hello 다음 Python 패키지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="d6b31-261">Hello AzureML 노트북 서비스를 사용 하는 경우 이러한 패키지는 미리 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

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


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="d6b31-262">Blob에서 hello 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="d6b31-262">Read in hello data from blob</span></span>
* <span data-ttu-id="d6b31-263">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="d6b31-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="d6b31-264">텍스트로 읽기</span><span class="sxs-lookup"><span data-stu-id="d6b31-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="d6b31-266">열 이름 추가 및 열 구분</span><span class="sxs-lookup"><span data-stu-id="d6b31-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="d6b31-267">일부 열 toonumeric 변경</span><span class="sxs-lookup"><span data-stu-id="d6b31-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="d6b31-268">기계 학습 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="d6b31-268">Build machine learning models</span></span>
<span data-ttu-id="d6b31-269">여기 또는 not 맞게 되 고 한 이동 여부를 이진 분류 모델 toopredict을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="d6b31-270">Hello Jupyter 노트북에서에서 다른 두 모델을 찾을 수 있습니다: 다중 클래스 분류 및 회귀 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="d6b31-271">먼저 scikit에 사용할 수 있는 toocreate 더미 변수 해야-모델에 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="d6b31-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="d6b31-272">Hello 모델링에 대 한 데이터 프레임 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="d6b31-273">학습 및 테스트 60-40분할</span><span class="sxs-lookup"><span data-stu-id="d6b31-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="d6b31-274">학습 집합에서 로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="d6b31-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="d6b31-275">테스트 데이터 집합 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="d6b31-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="d6b31-276">평가 메트릭 계산</span><span class="sxs-lookup"><span data-stu-id="d6b31-276">Calculate Evaluation metrics</span></span>
  
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

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="d6b31-277">웹 서비스 API 구축 및 Python에서 사용</span><span class="sxs-lookup"><span data-stu-id="d6b31-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="d6b31-278">Toooperationalize hello로 기계를 학습 모델 작성 된 후 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="d6b31-279">문서의 예를 들어 hello 이진 로지스틱 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="d6b31-280">있는지 hello scikit 확인-로컬 컴퓨터에서이 버전은 0.15.1에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="d6b31-281">Azure ML studio 서비스를 사용 하는 경우이 대 한 tooworry가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="d6b31-282">Azure 기계 학습 스튜디오 설정에서 작업 영역 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="d6b31-283">Azure Machine Learning 스튜디오에서 **설정** --> **이름** --> **권한 부여 토큰**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="d6b31-285">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="d6b31-286">웹 서비스 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="d6b31-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="d6b31-287">웹 서비스 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-287">Call Web service API.</span></span> <span data-ttu-id="d6b31-288">Toowait hello 이전 단계를 수행한 후 5-10 초 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="d6b31-289">옵션 2: Azure 기계 학습에서 모델을 만들고 직접 배포</span><span class="sxs-lookup"><span data-stu-id="d6b31-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="d6b31-290">Azure 기계 학습 스튜디오 Azure 데이터 레이크 저장소에서 직접 데이터를 읽을 하 고 수 사용된 toocreate 있고 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="d6b31-291">이 방법은 hello Azure 데이터 레이크 저장소에서 가리키는 Hive 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="d6b31-292">이렇게 하려면 별도 Azure HDInsight 클러스터 프로 비전 할 하이브는 hello 테이블이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="d6b31-293">섹션 표시 방법을 따르는 hello toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="d6b31-294">HDInsight Linux 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="d6b31-295">Hello에서 (Linux) 하는 HDInsight 클러스터 만들기 [Azure 포털](http://portal.azure.com)합니다. 자세한 내용은 참조 hello **액세스 tooAzure 데이터 레이크 저장소는 HDInsight 클러스터 만들기** 섹션 [데이터 레이크 저장소 Azure 포털을 사용 하는 HDInsight 클러스터를 만듭니다](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="d6b31-297">HDInsight에서 Hive 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="d6b31-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="d6b31-298">이제 Azure 기계 학습 스튜디오에서 사용 하 여 hello 이전 단계에서 Azure 데이터 레이크 저장소에 저장 된 hello 데이터를 사용 하 여 hello HDInsight 클러스터의 Hive 테이블 toobe를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="d6b31-299">Toohello 방금 만든 HDInsight 클러스터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="d6b31-300">클릭 **설정** --> **속성** --> **클러스터 AAD Id** --> **ADLS 액세스**, Azure 데이터 레이크 저장소 계정의 읽기 hello 목록에 추가 되어 있는지 확인 하 고, 쓰기 및 실행 권한을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="d6b31-302">클릭 **대시보드** 다음 toohello **설정을** 단추와 창이 팝업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="d6b31-303">클릭 **하이브 보기** hello hello 페이지의 오른쪽 위 모서리 hello 나타납니다 **쿼리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="d6b31-306">테이블을 hello 하이브 스크립트 toocreate 뒤에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="d6b31-307">이러한 방식으로 Azure 데이터 레이크 저장소 참조의 데이터 원본의 hello 위치는: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

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


<span data-ttu-id="d6b31-308">Hello 쿼리 실행이 끝나면 다음과 같은 hello 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="d6b31-310">Azure 기계 학습 스튜디오에서 모델 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="d6b31-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="d6b31-311">이제 준비 toobuild 했으며와 Azure 기계 학습 팁을 지불 여부를 예측 하는 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="d6b31-312">hello 층 화 샘플 데이터는이 이진 분류에 사용 되는 준비 toobe (여부 팁) 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="d6b31-313">다중 클래스 분류 (tip_class)를 사용 하 여 예측 모델 hello 및 회귀 (tip_amount)도 빌드 및 Azure 기계 학습 스튜디오를 사용 하 여 배포 수 않지만, 여기만 toohandle hello 사례를 사용 하 여 이진 분류 모델을 hello 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="d6b31-314">Hello 데이터 hello를 사용 하 여 Azure ML로 가져오므로 **데이터 가져오기** hello에서 사용할 수 있는 모듈 **데이터 입력 및 출력** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d6b31-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="d6b31-315">자세한 내용은 참조 hello [데이터 가져오기 모듈](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 참조 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="d6b31-316">선택 **하이브 쿼리** hello로 **데이터 소스** hello에 **속성** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="d6b31-317">Hello에서 하이브 스크립트를 다음 붙여넣기 hello **하이브 데이터베이스 쿼리** 편집기</span><span class="sxs-lookup"><span data-stu-id="d6b31-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="d6b31-318">Hello URI의 HDInsight 클러스터 (있습니다 Azure 포털에서), Hadoop 자격 증명, Azure 저장소 계정 이름/키/컨테이너 이름 및 출력 데이터의 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="d6b31-320">Hive 테이블에서 데이터를 읽는 이진 분류 실험의 예는 아래 hello 그림에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="d6b31-322">Hello 실험을 만든 후 클릭 **웹 서비스 설정** --> **예측 웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="d6b31-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="d6b31-324">자동으로 생성 하는 실행된 hello 클릭이 완료 되었을 때 실험에서는 점수 매기기 **웹 서비스 배포**</span><span class="sxs-lookup"><span data-stu-id="d6b31-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="d6b31-326">hello 웹 서비스 대시보드는 곧 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="d6b31-328">요약</span><span class="sxs-lookup"><span data-stu-id="d6b31-328">Summary</span></span>
<span data-ttu-id="d6b31-329">이 연습을 완료하면서 Azure Data Lake에서 확장성 있는 종단 간 솔루션을 구축하기 위한 데이터 과학 환경을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="d6b31-330">이 환경이 사용 되는 tooanalyze 큰 공용 데이터 집합, 데이터 과학 프로세스에서 모델 학습을 통해 데이터 취득 hello hello 정식 단계를 수행 하 고 웹 서비스로 hello toohello 배포 모델링 하는 다음 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="d6b31-331">U-SQL가 사용 되는 tooprocess, 탐색 하 고 hello 데이터 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="d6b31-332">Python 및 Hive toobuild Azure 기계 학습 스튜디오에서 사용 하 고 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="d6b31-333">다음 작업</span><span class="sxs-lookup"><span data-stu-id="d6b31-333">What's next?</span></span>
<span data-ttu-id="d6b31-334">hello에 대 한 경로 파악 중는 [팀 데이터 과학 프로세스 (TDSP)](http://aka.ms/datascienceprocess) 각각 설명 하는 링크 tootopics hello 고급 분석 프로세스에서에서 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b31-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="d6b31-335">일련의 연습 hello에 항목별로 없는 [팀 데이터 과학 프로세스 연습](data-science-process-walkthroughs.md) 해당 쇼케이스 어떻게 페이지 toouse 리소스 및 다양 한 예측 분석 시나리오에서 서비스:</span><span class="sxs-lookup"><span data-stu-id="d6b31-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="d6b31-336">작업에 팀 데이터 과학 프로세스 hello: SQL 데이터 웨어하우스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d6b31-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="d6b31-337">작업에 팀 데이터 과학 프로세스 hello: HDInsight Hadoop 클러스터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d6b31-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="d6b31-338">hello 팀 데이터 과학 프로세스: SQL Server를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d6b31-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="d6b31-339">Azure HDInsight의 hello 데이터 과학 프로세스를 사용 하 여 간략하게 멤버</span><span class="sxs-lookup"><span data-stu-id="d6b31-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

