---
title: "1TB 데이터 집합에는 Azure HDInsight Hadoop 클러스터를 사용 하 여 작업-에 팀 데이터 과학 프로세스 hello | Microsoft Docs"
description: "HDInsight Hadoop을 사용 하는 종단 간 시나리오에 대 한 hello 팀 데이터 과학 프로세스를 사용 하 여 클러스터링 toobuild 하 고 큰 (1TB) 공개적으로 사용할 수 있는 데이터 집합을 사용 하 여 모델 배포"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="911c5-103">1TB 데이터 집합에는 Azure HDInsight Hadoop 클러스터를 사용 하 여 작업-에 hello 팀 데이터 과학 프로세스</span><span class="sxs-lookup"><span data-stu-id="911c5-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="911c5-104">이 연습에 대해서도 설명를 사용 하 여 데이터 과학 팀 프로세스를 사용 하는 종단 간 시나리오에서 hello는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/) toostore, 탐색, 엔지니어, 기능 및 hello 중 하나에서 예제 데이터를 공개적으로 아래쪽 사용 가능한 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="911c5-105">이 데이터에 대해 Azure 기계 학습 toobuild 이진 분류 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="911c5-106">또한 어떻게 toopublish 다음 중 하나를 모델링 웹 서비스로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="911c5-107">이 연습에서 수행할는 IPython 노트북 tooaccomplish hello 작업 가능한 toouse 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="911c5-108">사용자에 게는이 방법을 문의 해야 tootry 같은 hello [하이브 ODBC 연결을 사용 하 여 Criteo 연습](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="911c5-109"><a name="dataset"></a>데이터 집합 설명</span><span class="sxs-lookup"><span data-stu-id="911c5-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="911c5-110">hello Criteo 데이터는 클릭 예측 데이터 집합을 gzip 압축 TSV 파일 (~1.3TB 압축 되지 않은)의 약 370 g B 이상 4.3 십억 레코드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="911c5-111">[Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)에서 사용할 수 있는 24일간의 클릭 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="911c5-112">데이터 과학자의 hello 편의 위해 데이터를 사용할 수 있는 toous tooexperiment에 압축을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="911c5-113">이 데이터 집합의 각 레코드에는 40개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="911c5-114">hello 첫 번째 열은 사용자가 클릭 여부를 나타내는 레이블 열은 **추가** (값 1) (값 0) 하나를 클릭 하지 않는 또는</span><span class="sxs-lookup"><span data-stu-id="911c5-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="911c5-115">다음 13개의 열은 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="911c5-116">마지막 26개는 범주 열입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-116">last 26 are categorical columns</span></span>

<span data-ttu-id="911c5-117">hello 열은 익명으로 처리 및 여러 개의 열거 된 이름 사용 하 여: (hello 레이블 열)에 대 한 "Col1" 너무 ' Col40 "(마지막 범주 열 hello)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="911c5-118">여기서는 hello의 일부 먼저 20의 열이 데이터이 집합에서 두 가지 사항을 확인할 (행):</span><span class="sxs-lookup"><span data-stu-id="911c5-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="911c5-119">이 데이터 집합에 두 hello 숫자 및 범주 열에 누락 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="911c5-120">Hello 누락 값을 처리 하는 간단한 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="911c5-121">Hello 데이터에 대 한 자세한 내용은 Hive 테이블에 저장 하는 경우에 대해서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="911c5-122">**정의:** *클릭 광고 속도 (CTR):* hello 데이터 â hello 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="911c5-123">이 Criteo 데이터 집합에 hello CTR는 약 3.3% 또는 0.033 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="911c5-124"><a name="mltasks"></a>예측 작업의 예제</span><span class="sxs-lookup"><span data-stu-id="911c5-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="911c5-125">이 연습에서는 두 가지 샘플 예측 문제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="911c5-126">**이진 분류**: 사용자가 광고를 클릭했는지 여부를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="911c5-127">클래스 0: 클릭 안 함</span><span class="sxs-lookup"><span data-stu-id="911c5-127">Class 0: No Click</span></span>
   * <span data-ttu-id="911c5-128">클래스 1: 클릭</span><span class="sxs-lookup"><span data-stu-id="911c5-128">Class 1: Click</span></span>
2. <span data-ttu-id="911c5-129">**회귀**: 사용자 기능에서 클릭 광고의 hello 확률을 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="911c5-130"><a name="setup"></a>데이터 과학용 HDInsight Hadoop 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="911c5-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="911c5-131">**참고:** 일반적으로 **관리** 태스크입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="911c5-132">다음 3단계에 따라 HDInsight 클러스터를 사용하여 예측 분석 솔루션을 빌드하기 위한 Azure 데이터 과학 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="911c5-133">[저장소 계정 만들기](../storage/common/storage-create-storage-account.md):이 저장소 계정은 Azure Blob 저장소에 사용 되는 toostore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="911c5-134">HDInsight 클러스터에 사용 되는 hello 데이터 여기에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="911c5-135">[데이터 과학용 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md):이 단계에서는 모든 노드에 설치된 64비트 Anaconda Python 2.7을 사용하여 Azure HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="911c5-136">Hello HDInsight 클러스터를 사용자 지정할 때 두 가지 중요 한 단계 (이 항목에서 설명) toocomplete가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="911c5-137">Hello 저장소 계정을 만들 때 HDInsight 클러스터와 1 단계에서 만든 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="911c5-138">이 저장소 계정은 hello 클러스터 내에서 처리할 수 있는 데이터에 액세스 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="911c5-139">만든 후 원격 액세스 toohello hello 클러스터의 헤드 노드를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="911c5-140">Hello 원격 액세스 (생성 시 hello 클러스터에 대 한 지정 된 것과 다른) 여기에서 지정한 자격 증명 기억: toocomplete 필요한 경우 다음 절차 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="911c5-141">[Azure ML 작업 영역을 만들](machine-learning-create-workspace.md):이 Azure 기계 학습 작업 영역은 초기 데이터 탐색 후] 및 [아래로 hello HDInsight 클러스터에서 샘플링 기계 학습 모델을 구축 하기 위한 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="911c5-142"><a name="getdata"></a>공용 원본에서 데이터 가져오기 및 사용</span><span class="sxs-lookup"><span data-stu-id="911c5-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="911c5-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) hello 링크를 클릭 하면 hello 사용 약관을 수락 하 고 이름을 제공 하 여 데이터 집합을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="911c5-144">다음과 같은 스냅숏이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-144">A snapshot of what this looks like is shown here:</span></span>

![Criteo 조건 동의](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="911c5-146">클릭 **계속 tooDownload** tooread hello 데이터 집합 및 가용성에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="911c5-147">공용에서 hello 데이터가 있는 [Azure blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 위치: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="911c5-148">"wasb" hello tooAzure Blob 저장소 위치를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="911c5-149">이 공용 blob 저장소에 hello 데이터 압축 푼된 데이터의 세 가지 하위 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="911c5-150">하위 폴더를 hello *원시/count/* hello 데이터 요금-날부터의 첫 번째 21 일 포함\_00 tooday\_20</span><span class="sxs-lookup"><span data-stu-id="911c5-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="911c5-151">하위 폴더를 hello *원시/학습/* 데이터의 하루 이루어져 일\_21</span><span class="sxs-lookup"><span data-stu-id="911c5-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="911c5-152">하위 폴더를 hello *원시/테스트/* 2 일 분량의 데이터를 이루어져 일\_22 및 day\_23</span><span class="sxs-lookup"><span data-stu-id="911c5-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="911c5-153">사람들 toostart hello 원시 gzip 데이터와, 이러한 사용할 수도 있습니다 hello 기본 폴더에 *원시 /* 00 too23에서 NN 흐름 방향은 day_NN.gz로 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="911c5-154">다른 접근 방식은 tooaccess 탐색 하 고 로컬 다운로드 하이브 테이블을 만들 때이 연습 뒷부분에서 설명 하지 않아도이 데이터를 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="911c5-155"><a name="login"></a>Toohello 클러스터 헤드 노드에 로그인</span><span class="sxs-lookup"><span data-stu-id="911c5-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="911c5-156">사용 하 여 hello hello 클러스터의 헤드 노드에 toohello toolog [Azure 포털](https://ms.portal.azure.com) toolocate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="911c5-157">왼쪽 hello에 hello HDInsight 코끼리 아이콘을 클릭 하 고 클러스터의 hello 이름을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="911c5-158">Toohello 이동 **구성** 탭 hello hello 페이지 아래쪽에 hello 연결 아이콘을 두 번 클릭 하 고 메시지가 표시 되 면 원격 액세스 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="911c5-159">Hello 클러스터의 헤드 노드에 toohello 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="911c5-160">클러스터 헤드 노드에 toohello에 일반적인 첫 번째 로그의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Toocluster 로그인](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="911c5-162">Hello 왼쪽에 "Hadoop 명령" 하는 줄 hello 데이터 탐색에 대 한 우리의 즐겨 hello를 보면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="911c5-163">두 가지 유용한 URL인 "Hadoop Yarn Status" 및 "Hadoop Name Node"도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="911c5-164">hello yarn 상태 URL 작업 진행 상황을 표시 하 고 hello 이름 노드 URL hello 클러스터 구성에 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="911c5-165">이제 우리는를 설정 하 고 hello 연습의 첫 번째 부분 toobegin 준비 됨: 데이터 탐색 하이브를 사용 하 여 및 Azure 기계 학습에 대 한 데이터를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="911c5-166"><a name="hive-db-tables"></a> Hive 데이터베이스 및 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="911c5-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="911c5-167">하이브 toocreate 우리의 Criteo 데이터 집합 열기 hello에 대 한 테이블 ***Hadoop 명령줄*** hello 헤드 노드의 데스크톱 hello 되 고 hello 명령을 입력 하 여 hello 하이브 디렉터리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="911c5-168">Hello 하이브 bin에서이 연습에서 모든 하이브 명령을 실행 / directory 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="911c5-169">경로 문제가 자동으로 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="911c5-170">Hello 용어 "하이브 디렉터리 프롬프트"를 사용 하 여 "하이브 bin / directory 프롬프트", "Hadoop 명령줄" 같은 의미로 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="911c5-171">tooexecute 모든 하이브 쿼리 하나 명령 뒤 hello 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="911c5-172">Hello 후 하이브 REPL 표시는 "하이브 >" 서명, 단순히에서 잘라내기 및 붙여넣기 hello 쿼리 tooexecute 것입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="911c5-173">hello 다음 코드에서는 "criteo" 데이터베이스 만들고 4 테이블을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="911c5-174">*개수를 생성 하기 위한 테이블이* 일 날에 빌드된\_00 tooday\_20 일</span><span class="sxs-lookup"><span data-stu-id="911c5-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="911c5-175">*사용 하기 위해 테이블에 hello 학습 데이터 집합으로* 날에 빌드된\_21, 및</span><span class="sxs-lookup"><span data-stu-id="911c5-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="911c5-176">두 개의 *hello로 사용 하기 위해 테이블 테스트 데이터 집합* 날에 빌드된\_22 및 day\_23 각각.</span><span class="sxs-lookup"><span data-stu-id="911c5-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="911c5-177">우리는 휴일, 고 hello 모델 hello 클릭 광고 속도에서 공휴일 및 비 휴일 간의 차이점을 검색할 수 있는 경우 원하는 toodetermine hello 일 중 하나 때문에 서로 다른 두 테이블으로 우리의 테스트 데이터 집합을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="911c5-178">스크립트 hello [샘플 &#95; 하이브 &#95; 만들기 &#95; criteo &#95; 데이터베이스 &#95; 및 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) 편의 위해 여기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="911c5-179">이러한 모든 테이블은 단순히 지점 tooAzure Blob 저장소 (wasb) 위치에서는으로 외부 기록한 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="911c5-180">**두 가지 방법 tooexecute ANY 하이브 쿼리 이제 언급 하는 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="911c5-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="911c5-181">**하이브 REPL 명령줄 hello를 사용 하 여**: hello 먼저 tooissue "하이브" 명령과 복사 되며 hello 하이브 REPL 명령줄에서 쿼리를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="911c5-182">toodo이를이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="911c5-183">명령줄 REPL hello에 잘라내기 및 붙여넣기 이제 hello 쿼리를 실행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="911c5-184">**저장 쿼리 tooa 파일과 hello 명령을 실행**: hello toosave hello 쿼리 tooa.hql 파일을 두 번째는 ([샘플 &#95; 하이브 &#95; 만들기 &#95; criteo &#95; 데이터베이스 &#95; 및 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql))과 다음 문제 hello 다음 명령 tooexecute hello 쿼리:</span><span class="sxs-lookup"><span data-stu-id="911c5-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="911c5-185">데이터베이스 및 테이블 만들기 확인</span><span class="sxs-lookup"><span data-stu-id="911c5-185">Confirm database and table creation</span></span>
<span data-ttu-id="911c5-186">다음으로 hello 하이브 bin에서 다음 명령을 hello로 hello hello 데이터베이스 만들기 확인 / directory 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="911c5-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="911c5-187">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="911c5-188">Hello "criteo" hello 새 데이터베이스 만들기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="911c5-189">toosee 만든 테이블에서는 단순히 hello에서에서 명령을 실행할 여기 hello 하이브 bin / directory 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="911c5-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="911c5-190">다음 출력을 따라 hello 표시:</span><span class="sxs-lookup"><span data-stu-id="911c5-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="911c5-191"><a name="exploration"></a> Hive에서 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="911c5-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="911c5-192">이제 toodo 하이브에 몇 가지 기본 데이터 탐색을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="911c5-193">Hello hello 학습의 예제 수를 계산 하 여 시작 하 고 테스트 데이터 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="911c5-194">train 예제 수</span><span class="sxs-lookup"><span data-stu-id="911c5-194">Number of train examples</span></span>
<span data-ttu-id="911c5-195">내용을 hello [샘플 &#95; 하이브 #95 개수 및 #95; 기차 및 #95; 테이블 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) 여기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="911c5-196">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="911c5-197">또는 하나 또한 발행 hello 하이브 bin에서 다음 명령을 hello / directory 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="911c5-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="911c5-198">테스트 예제 hello 두 테스트 데이터 집합의 수</span><span class="sxs-lookup"><span data-stu-id="911c5-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="911c5-199">에서는 이제 hello 두 개의 테스트 데이터 집합의 예제에서는 hello 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="911c5-200">내용을 hello [샘플 &#95; 하이브 및 #95 개수 및 #95; criteo &#95; 테스트 및 #95; 일 및 #95; 22 &#95; 테이블 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) 는 여기에서:</span><span class="sxs-lookup"><span data-stu-id="911c5-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="911c5-201">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="911c5-202">일반적으로 म 호출할 수도 있습니다 hello 스크립트 hello 하이브 bin에서 /directory hello 명령을 실행 하 여 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="911c5-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="911c5-203">Hello hello 일을 기준으로 테스트 데이터 집합에 테스트 예제 수가 마지막으로 살펴볼\_23입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="911c5-204">hello 명령 toodo 이것은 앞서 설명한 하나 비슷한 toohello (너무 참조[샘플 &#95; 하이브 및 #95; 개수 및 #95; criteo #95 테스트 및 #95; 일 및 #95; 23 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="911c5-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="911c5-205">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="911c5-206">Hello 학습 데이터 집합의 레이블 배포</span><span class="sxs-lookup"><span data-stu-id="911c5-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="911c5-207">hello 학습 데이터 집합의 레이블 배포 hello은 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="911c5-208">toosee이 내용의 알아보겠습니다 [샘플 &#95; 하이브 및 #95; criteo #95 레이블 및 #95; 배포 &#95; 기차 &; #95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="911c5-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="911c5-209">이 식이 hello 레이블 배포가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="911c5-210">양수 레이블 백분율로 hello 참고는 3.3% 정도 (원래 hello 데이터 집합과 일치)입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="911c5-211">데이터 집합을 학습 하는 hello의 일부 숫자 변수 histogram 분포</span><span class="sxs-lookup"><span data-stu-id="911c5-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="911c5-212">하이브의 네이티브를 사용할 수 있습니다 "히스토그램\_숫자" hello 숫자 변수 어떤 hello 분포 처럼 보이는 아웃 toofind 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="911c5-213">다음은 hello 내용의 [샘플 &#95; 하이브 및 #95; criteo #95 히스토그램 &; #95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="911c5-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="911c5-214">이 hello 다음을 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-214">This yields hello following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="911c5-215">hello 측면 뷰-폭발에서 하이브 처리 tooproduce hello 일반적인 목록 대신 SQL과 유사한 출력을 조합 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="911c5-216">참고는에 hello 테이블, hello 첫 번째 열이 해당 toohello bin 중심과 hello 두 번째 toohello bin 빈도.</span><span class="sxs-lookup"><span data-stu-id="911c5-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="911c5-217">데이터 집합을 학습 하는 hello의 일부 숫자 변수 대략적인 백분위 수</span><span class="sxs-lookup"><span data-stu-id="911c5-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="911c5-218">또한 관심 있는 숫자 변수와 함께 대략적인 백분위 수의 hello 계산이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="911c5-219">여기에는 Hive의 기본 "percentile\_approx"가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="911c5-220">내용을 hello [샘플 &#95; hive &#95; criteo &; #95; 근사치 &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) 됩니다:</span><span class="sxs-lookup"><span data-stu-id="911c5-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="911c5-221">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="911c5-222">에서는 주석 백분위 수의 hello 분포는 숫자 변수 밀접 한 관련이 toohello 히스토그램 분포 일반적으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="911c5-223">Hello 학습 데이터 집합의 일부 범주 열에 대 한 고유 값 수 찾기</span><span class="sxs-lookup"><span data-stu-id="911c5-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="911c5-224">지속적 hello 데이터 탐색, 이제 보면 일부 범주 열의 경우 hello 가지도록 고유 값 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="911c5-225">toodo이의 콘텐츠를 표시 했습니다 [샘플 &#95; hive &#95; criteo &; #95 고유; &#95; 값 &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="911c5-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="911c5-226">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="911c5-227">Col15에 1,900만 개의 고유 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="911c5-228">Tooencode "하나 핫 인코딩"와 같은 naïve 기법을 사용 하 여 이러한 차원 범주 변수는 쉽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="911c5-229">따라서 여기에서는 이 문제를 효과적으로 해결하는 [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) 라는 강력한 기술을 설명하고 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="911c5-230">몇 가지 다른 범주 열에 대 한 고유 값 수가 hello 확인 하 여에이 하위 섹션을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="911c5-231">내용을 hello [샘플 &#95; hive &#95; criteo &; #95 고유; & #95, 값 및 #95, 여러 &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) 됩니다:</span><span class="sxs-lookup"><span data-stu-id="911c5-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="911c5-232">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="911c5-233">다시 보면 있는지 Col20를 제외한 모든 hello 다른 많은 고유 값이 있는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="911c5-234">Hello 학습 데이터 집합의 범주 변수의 쌍 공동 발생 횟수</span><span class="sxs-lookup"><span data-stu-id="911c5-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="911c5-235">hello 공동 발생 횟수 범주 변수의 쌍은도 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="911c5-236">hello 코드를 사용 하 여 확인할 수 있습니다 [샘플 &#95; hive &#95; criteo &; #95 쌍을 이루는; &#95; 범주 &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="911c5-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="911c5-237">म 발생 하 여 주문 hello 수량이 역방향으로 한이 예에서 hello 상위 15 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="911c5-238">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="911c5-239"><a name="downsample"></a>Azure 기계 학습에 대 한 샘플 hello 데이터 집합 아래로</span><span class="sxs-lookup"><span data-stu-id="911c5-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="911c5-240">데이터 집합 탐색된 hello 필요 하 고 있습니다 방법은 이러한 유형의 샘플 hello 데이터 집합 아래로 이제 우리는 변수 (포함 하 여 조합)에 대 한 탐색 하 여 Azure 기계 학습에서 모델을 작성할 수 있습니다를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="911c5-241">에 대해 살펴볼 해당 hello 문제는 회수: Col1은 0 (클릭 없음) 또는 1 (클릭) 하는 경우 예측 예제 특성 (c o l 2-Col40에서에서 기능 값)의 집합을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="911c5-242">toodown 샘플 우리의 학습 및 테스트 데이터 집합 too1 %hello 원래 크기의, 하이브의 네이티브 rand () 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="911c5-243">다음 스크립트를 hello [샘플 &#95; 하이브 및 #95; criteo &#95; 저해상도 #95 기차 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) hello 학습 데이터 집합에 대해이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="911c5-244">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="911c5-245">스크립트 hello [샘플 &#95; 하이브 및 #95; criteo &#95; 저해상도 #95 테스트 및 #95; 일 및 #95; 22 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) 테스트 데이터에는 하루\_22:</span><span class="sxs-lookup"><span data-stu-id="911c5-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="911c5-246">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="911c5-247">마지막으로 스크립트를 hello [샘플 &#95; 하이브 및 #95; criteo &#95; 저해상도 #95 테스트 및 #95; 일 및 #95; 23 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) 테스트 데이터에는 하루\_23:</span><span class="sxs-lookup"><span data-stu-id="911c5-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="911c5-248">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="911c5-249">이 준비 toouse 우리의 다운 샘플링 하는 학습 및 테스트에 Azure 기계 학습 모델을 작성 하는 것에 대 한 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="911c5-250">문제 hello 개수 테이블은 기계 학습에서는 tooAzure 넘어가기 전에는 최종 중요 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="911c5-251">Hello 다음 하위 섹션에서이 부분은 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="911c5-252"><a name="count"></a>Hello 개수 테이블에 대 한 간단한 설명</span><span class="sxs-lookup"><span data-stu-id="911c5-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="911c5-253">몇몇 범주 변수는 차원이 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="911c5-254">이 연습에서는 강력한 기술을 소개 [학습와 계산](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode 효율적이 고 강력한 방식으로 이러한 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="911c5-255">이 방법에 대 한 자세한 내용은 hello에 제공 된 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="911c5-256">이 연습에서는 차원 범주 기능의 개수 테이블 tooproduce compact 표현을 사용 하 여 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="911c5-257">이 hello 유일한 방법은 tooencode 범주 기능입니다. 다른 기술에 대 한 자세한 내용은 사용자가 관심된을 체크 아웃할 수 [하나 핫-인코딩](http://en.wikipedia.org/wiki/One-hot) 및 [기능 해시](http://en.wikipedia.org/wiki/Feature_hashing)합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="911c5-258">hello 개수 데이터에서 toobuild 개수 테이블에서 개수 폴더 원시/hello hello 데이터 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="911c5-259">사용자가 알아보겠습니다 섹션을 모델링 하는 hello에 어떻게 toobuild 이러한 계산 테이블은 처음부터 새로, 또는 또는 toouse 범주 기능에 대 한 해당 탐색에 대 한 미리 작성 된 개수 테이블 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="911c5-260">기능에서 참조 하는 경우 다음과 같이 너무 "미리 작성 된 개수 테이블", 제공 하는 hello 개수 테이블을 사용 하 여 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="911c5-261">Tooaccess 이러한 테이블 제공 방법을 hello 다음 섹션에 대 한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="911c5-262"><a name="aml"></a> Azure 기계 학습에서 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="911c5-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="911c5-263">Azure Machine Learning의 모델 빌드 프로세스는 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="911c5-264">Azure 기계 학습에 Hive 테이블에서 hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="911c5-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="911c5-265">Hello 실험 만들기: hello 데이터 및 기능 화할 개수 테이블 정리</span><span class="sxs-lookup"><span data-stu-id="911c5-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="911c5-266">빌드, 학습 및 점수 hello 모델</span><span class="sxs-lookup"><span data-stu-id="911c5-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="911c5-267">Hello 모델 평가</span><span class="sxs-lookup"><span data-stu-id="911c5-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="911c5-268">Hello 모델을 웹 서비스로 게시</span><span class="sxs-lookup"><span data-stu-id="911c5-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="911c5-269">이제는 Azure 기계 학습 스튜디오에서 준비 toobuild 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="911c5-270">아래쪽 샘플링 된 데이터는 hello 클러스터의 Hive 테이블으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="911c5-271">Hello Azure 기계 학습 사용 하 여 **데이터 가져오기** 모듈 tooread이이 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="911c5-272">이 클러스터의 hello 자격 증명 tooaccess hello 저장소 계정 다음에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="911c5-273"><a name="step1"></a>1 단계: hello 데이터 가져오기 모듈을 사용 하 여 Azure 기계 학습에 Hive 테이블에서 데이터 가져오기 및 기계 학습 실험에 대 한 선택</span><span class="sxs-lookup"><span data-stu-id="911c5-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="911c5-274">**+새로 만들기** -> **실험** -> **빈 실험**을 선택하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="911c5-275">그런 다음 hello에서 **검색** 상자 위에 표시 hello, "데이터"에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="911c5-276">끌어서 놓기 hello **데이터 가져오기** 모듈 데이터 액세스를 위한 toohello 실험 캔버스 (hello 화면의 중간 부분 hello) toouse hello 모듈에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="911c5-277">이 어떤 hello **데이터 가져오기** hello Hive 테이블에서 데이터를 가져오는 동안 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![데이터 가져오기로 데이터 가져오기](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="911c5-279">Hello에 대 한 **데이터 가져오기** hello hello 매개 변수 값의 hello 그래픽은 일종의 값의 hello 예일 뿐 제공 되는 모듈 tooprovide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="911c5-280">Hello 매개 변수는 toofill hello에 대 한 설정 하는 방법에 몇 가지 일반적인 지침 같습니다 **데이터 가져오기** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="911c5-281">**데이터 원본**</span><span class="sxs-lookup"><span data-stu-id="911c5-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="911c5-282">Hello에 **하이브 데이터베이스 쿼리** 상자의 간단한 SELECT * FROM < 프로그램\_데이터베이스\_name.your\_테이블\_이름 >-충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="911c5-283">**Hcatalog 서버 URI**: 클러스터가 "abc"인 경우 간단하게 https://abc.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="911c5-284">**Hadoop 사용자 계정 이름을**: hello 클러스터 위탁 hello 시 선택한 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="911c5-285">Hello 원격 액세스 사용자 이름이 아닌!</span><span class="sxs-lookup"><span data-stu-id="911c5-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="911c5-286">**Hadoop 사용자 계정 암호**: hello hello 사용자 이름의 암호를 위탁 hello 클러스터의 hello 타임에 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="911c5-287">(하지 hello 원격 액세스 암호!)</span><span class="sxs-lookup"><span data-stu-id="911c5-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="911c5-288">**Location of output data**(출력 데이터 위치): "Azure"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="911c5-289">**Azure 저장소 계정 이름**: hello hello 클러스터와 연결 된 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="911c5-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="911c5-290">**Azure 저장소 계정 키**: hello 클러스터와 연결 된 hello 저장소 계정의 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="911c5-291">**Azure 컨테이너 이름을**: hello 클러스터 이름에 "abc"는 경우 일반적으로이 단순히 "abc".</span><span class="sxs-lookup"><span data-stu-id="911c5-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="911c5-292">한 번 hello **데이터 가져오기** (녹색 hello 눈금에 표시 hello 모듈) 데이터를 가져오기 완료 (사용자가 선택한 이름)으로 데이터 집합으로이 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="911c5-293">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-293">What this looks like:</span></span>

![데이터 가져오기로 데이터 저장](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="911c5-295">마우스 오른쪽 단추로 클릭 hello 출력 포트의 hello **데이터 가져오기** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="911c5-296">**데이터 집합으로 저장** 옵션 및 **시각화** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="911c5-297">hello **시각화** 옵션을 클릭 하면 hello 데이터 일부 요약 통계에 대 한 유용한 오른쪽 패널 100 개 행 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="911c5-298">toosave 데이터를 선택 하기만 하면 **데이터 집합으로 저장할** 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="911c5-299">컴퓨터 학습 실험에서 사용 하기 위해 tooselect hello 저장 된 데이터 집합 hello를 사용 하 여 hello 데이터 집합을 찾을 **검색** 상자 hello 다음 그림에에서 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="911c5-300">Hello 이름을 제공한 형식만 hello dataset 다음 tooaccess 하 고 끌어서 hello 데이터 집합의 주 패널 hello 부분적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="911c5-301">Hello 기본 패널에 놓으면 컴퓨터 학습 모델링에 사용 하기 위해 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Hello 주 패널 끌기 데이터 집합](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="911c5-303">Hello 학습 및 테스트 데이터 집합 hello 모두에 대해이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="911c5-304">또한 toouse hello 데이터베이스 이름 및이 위해 지정한 테이블 이름을 기억해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="911c5-305">만 위한 그림 purposes.* * hello 그림에 사용 되는 hello 값은</span><span class="sxs-lookup"><span data-stu-id="911c5-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="911c5-306"><a name="step2"></a>2 단계: Azure 기계 학습 toopredict 번의 클릭에서 간단한 실험 만들기 / 클릭 없음</span><span class="sxs-lookup"><span data-stu-id="911c5-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="911c5-307">Azure ML 실험은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-307">Our Azure ML experiment looks like this:</span></span>

![기계 학습 실험](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="911c5-309">이제이 실험의 주요 구성 요소를 hello 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="911c5-310">참고로이 저장 된 학습 및 테스트 데이터 집합 tooour 실험 캔버스에 먼저 toodrag이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="911c5-311">누락 데이터 정리</span><span class="sxs-lookup"><span data-stu-id="911c5-311">Clean Missing Data</span></span>
<span data-ttu-id="911c5-312">hello **누락 데이터 정리** 모듈 이름을 제안지 않습니다: 사용자 지정 될 수 있는 방법으로 누락 된 데이터를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="911c5-313">이 모듈을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-313">Looking into this module, we see this:</span></span>

![누락 데이터 정리](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="911c5-315">여기에서 선택한 이유 tooreplace 0 인 누락 된 모든 값.</span><span class="sxs-lookup"><span data-stu-id="911c5-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="911c5-316">Hello 드롭다운 목록 hello 모듈에서 확인 하 여 볼 수 있는 다른 옵션을도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="911c5-317">Hello 데이터에서 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="911c5-317">Feature engineering on hello data</span></span>
<span data-ttu-id="911c5-318">큰 데이터 집합의 범주 기능 중 일부에는 수백 만개의 고유 값이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="911c5-319">원 핫(one-hot) 인코딩과 같은 미숙한 방법을 사용하여 이러한 고차원 범주 기능을 나타내는 것은 전적으로 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="911c5-320">이 연습에서는 기본 제공 Azure 기계 학습 모듈 toogenerate를 사용 하 여 toouse 개수 기능 이러한 차원 범주 변수의 표현을 압축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="911c5-321">hello 최종 결과 더 작은 모델 크기, 더 빠른 학습 시간 및 toousing 매우 비교할 수 있는 성능 메트릭을 기타 기술 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="911c5-322">개수 변환 작성</span><span class="sxs-lookup"><span data-stu-id="911c5-322">Building counting transforms</span></span>
<span data-ttu-id="911c5-323">toobuild 수 기능을 사용 하 여 hello **변환 계산 빌드** Azure 기계 학습에서 사용할 수 있는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="911c5-324">hello 모듈은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-324">hello module looks like this:</span></span>

<span data-ttu-id="911c5-325">![개수 변환 모듈 빌드](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![개수 변환 모듈 작성](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="911c5-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="911c5-326">Hello에 **열 개수를 계산할** 상자에서 원하는 म tooperform 계산 열에서는 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="911c5-327">이미 설명한 대로 이러한 열은 일반적으로 고차원 범주의 열입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="911c5-328">Hello 시작 부분에 설명한 대로 해당 hello Criteo 데이터 집합에 범주 열이 26: Col15 tooCol40에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="911c5-329">모든 속성에 수는 여기에서 (쉼표로 구분 하 여 표시 된 것 처럼 15 too40)에서 해당 인덱스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="911c5-330">toouse hello 모듈에 hello MapReduce 모드 (큰 데이터 집합에 대 한 적절 한), (hello 기능 탐색을 위해 사용 되는 이러한 용도로 다시 사용할 수 있습니다) tooan HDInsight Hadoop 클러스터 및 해당 자격 증명에 액세스할 필요 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="911c5-331">이전 그림 hello 모양을 (replace hello 값에 직접 사용 사례에 대 한 관련 내용과 제공) 채워진 값을 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![모듈 매개 변수](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="911c5-333">Tooenter hello blob를 입력 하는 방법을 알아보겠습니다 위 hello 그림에 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="911c5-334">이 위치에 hello 데이터가 개수 테이블을 기반으로 구축 하기 위해 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="911c5-335">이 모듈에서 실행을 완료 한 후 수 저장에 대 한 hello 변환을 나중 hello 모듈을 마우스 오른쪽 단추로 클릭 하 고 hello를 선택 하 여 **변환으로 저장** 옵션:</span><span class="sxs-lookup"><span data-stu-id="911c5-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

!["변환으로 저장" 옵션](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="911c5-337">위에 표시 된 가이드의 실험 아키텍처에서 hello 데이터 집합 "ytransform2" count 변환을 저장 tooa 정확 하 게 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="911c5-338">사용 되는 해당 hello 판독기 가정이 실험 hello 나머지 인는 **변환 계산 빌드** 모듈에 일부 데이터 toogenerate 횟수 및 있습니다 hello 학습에서 해당 개수 toogenerate 수 기능을 사용 하 고 테스트 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="911c5-339">어떤 기능 tooinclude hello 학습의 일부로 계산 및 테스트 데이터 집합 선택</span><span class="sxs-lookup"><span data-stu-id="911c5-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="911c5-340">Hello 사용자가 기차에서 어떤 기능 tooinclude를 선택할 수 있으며 테스트 hello를 사용 하 여 데이터 집합 준비 변형할 수 있으면, **개수 테이블 매개 변수 수정** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="911c5-341">완성된 모양을 보여 주기 위해 이 모듈을 여기 표시해 놓기는 했지만 실험을 단순하게 하려면 이 모듈을 실제로 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="911c5-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![개수 테이블 매개 변수를 수정합니다.](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="911c5-343">이 예에서 볼 수 있듯이 선택한 toouse 정당한 hello 로그 확률 및 tooignore hello 열 백오프입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="911c5-344">Hello 휴지통 임계값, 다듬기에 대 한 이전 의사 예제 tooadd 개수 등의 매개 변수도 설정할 수 있습니다 및 여부 toouse 모든 라플라스 노이즈 여부.</span><span class="sxs-lookup"><span data-stu-id="911c5-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="911c5-345">이러한 모든 고급 기능 아니며 toobe hello 기본 값 새로운 toothis 유형의 기능 생성이 사용자를 위한 좋은 출발점으로 언급 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="911c5-346">Hello 수 기능을 생성 하기 전에 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="911c5-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="911c5-347">이제 우리의 기차 변형 하는 방법에 대 한 중요 한 내용에 집중 하 고 데이터 사전 tooactually 생성 개수 기능 테스트.</span><span class="sxs-lookup"><span data-stu-id="911c5-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="911c5-348">두 개의 **R 스크립트 실행** hello count tooour 데이터 변환 적용 하기 전에 사용 되는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![R 스크립트 모듈 실행](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="911c5-350">Hello 첫 번째 R 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-350">Here is hello first R script:</span></span>

![첫 번째 R 스크립트](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="911c5-352">이 R 스크립트에서 이름을 바꾸지 우리의 열 toonames "Col1" 너무 "Col40"입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="911c5-353">Hello count 변환에서는이 형식의 이름을 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="911c5-354">두 번째 R 스크립트 hello 양수 및 음수 클래스 간의 hello 배포 고려해 (각각 클래스 1과 0) 샘플링 hello 음수 클래스에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="911c5-355">hello R 스크립트 방법에서는 여기 toodo이:</span><span class="sxs-lookup"><span data-stu-id="911c5-355">hello R script here shows how toodo this:</span></span>

![두 번째 R 스크립트](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="911c5-357">이 간단한 R 스크립트를 사용 하 여 "pos\_neg\_비율" tooset hello 양을 hello 양수 및 음수 클래스 hello 간의 균형입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="911c5-358">이 과정이 중요 toodo hello 클래스 분포는 여기서 분류 문제에 대 한 성능상의 이점을 일반적으로 클래스 불균형 향상 때문에 왜곡 (회수 경우에 있는지 3.3% 양의 클래스와 96.7% 음수 클래스).</span><span class="sxs-lookup"><span data-stu-id="911c5-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="911c5-359">Hello 개수 변환을 데이터에 적용</span><span class="sxs-lookup"><span data-stu-id="911c5-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="911c5-360">마지막으로, 우리 צ ְ ײ hello **변환 적용** 모듈 tooapply 우리의 학습에는 개수 변환을 hello 및 테스트 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="911c5-361">이 모듈 학습 또는 테스트 데이터 집합의 다른 입력 hello 하나의 입력과 hello 저장 hello count 변형 됩니다 하 고 개수 기능을 사용 하 여 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="911c5-362">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-362">It is shown here:</span></span>

![변환 모듈 적용](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="911c5-364">hello 개수 기능 모양을 발췌 한 구문</span><span class="sxs-lookup"><span data-stu-id="911c5-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="911c5-365">것이 좋습니다 toosee hello 개수 기능에는 어떤 경우에는 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="911c5-366">다음은 이 기능이 보이는 부분을 발췌한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-366">Here we show an excerpt of this:</span></span>

![개수 기능](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="911c5-368">발췌 한이 म 입증 계산 म 있는 hello 열에 대 한 म hello 개수를 가져올 추가 tooany 관련 backoffs 확률 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="911c5-369">이제는 준비 toobuild 이러한 변환 된 데이터 집합을 사용 하는 Azure 기계 학습 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="911c5-370">Hello 다음 섹션에서는 수 수행 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="911c5-371"><a name="step3"></a>3 단계: 작성, 학습 및 hello 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="911c5-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="911c5-372">학습자의 선택</span><span class="sxs-lookup"><span data-stu-id="911c5-372">Choice of learner</span></span>
<span data-ttu-id="911c5-373">먼저 toochoose는 학습자입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="911c5-374">이 학습자로 진행 중인 toouse 2 클래스 승격 된 의사 결정 트리는입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="911c5-375">다음은이 학습자에 대 한 hello 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-375">Here are hello default options for this learner:</span></span>

![2 클래스 향상된 의사 결정 트리 매개 변수](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="911c5-377">이 실험에 대 한 진행 중인 toochoose hello 기본 값은 했습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="911c5-378">해당 hello 기본값은 일반적으로 의미 있는 성능에 좋은 방법 tooget 빠른 기준을 기록한 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="911c5-379">스윕 매개 변수 있는 tooonce를 선택 하는 경우 초기 하 여 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="911c5-380">Hello 모델 학습</span><span class="sxs-lookup"><span data-stu-id="911c5-380">Train hello model</span></span>
<span data-ttu-id="911c5-381">학습용으로 간단히 **모델 학습** 모듈을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="911c5-382">두 입력 tooit hello는 hello 2 클래스 승격 된 의사 결정 트리 학습자 및 우리의 학습 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="911c5-383">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-383">This is shown here:</span></span>

![모델 학습 모듈](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="911c5-385">Hello 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="911c5-385">Score hello model</span></span>
<span data-ttu-id="911c5-386">준비 하는 학습된 된 모델 상태, tooscore hello에 테스트 데이터 집합 및 tooevaluate 성능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="911c5-387">Hello를 사용 하 여 수행 **모델 점수 매기기** hello 그림에서는 아래에 표시 된 모듈은 **모델 평가** 모듈:</span><span class="sxs-lookup"><span data-stu-id="911c5-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![모델 점수 매기기 모듈](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="911c5-389"><a name="step4"></a>4 단계: hello 모델 평가</span><span class="sxs-lookup"><span data-stu-id="911c5-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="911c5-390">마지막으로, tooanalyze 모델 성능을 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="911c5-391">일반적으로 두 가지 클래스 (이진) 분류 문제에 대 한 유용한 척도 hello AUC입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="911c5-392">toovisualize이 hello 후크 했습니다 **모델 점수 매기기** 모듈 tooan **모델 평가** 이 대 한 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="911c5-393">클릭 하면 **시각화** hello에 **모델 평가** 모듈 하나를 따르는 hello와 같은 그래픽을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Evaluate module BDT 모델](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="911c5-395">이진 (또는 두 개의 클래스)에서 분류 문제를 예측 정확도 측정 한 값 영역에서 곡선 (AUC) hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="911c5-396">다음은 테스트 데이터 집합에서 이 모델을 사용한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="911c5-397">tooget hello이를 마우스 오른쪽 단추로 클릭 hello 출력 포트 **모델 평가** 모듈 차례로 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Evaluate Model 모듈 시각화](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="911c5-399"><a name="step5"></a>5 단계: 웹 서비스로 hello 모델 게시</span><span class="sxs-lookup"><span data-stu-id="911c5-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="911c5-400">hello 기능 toopublish 간단 하 게 최소화 하 여 웹 서비스로 Azure 기계 학습 모델은 광범위 하 게 제공 하기 위한 중요 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="911c5-401">작업이 완료 되 면 누구나 호출 toohello 웹 서비스는 필요한 예측을 하 고 hello 웹 서비스는 hello 모델 tooreturn 이러한 예상 입력된 데이터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="911c5-402">toodo이를 먼저 예제의 학습 된 모델 학습 된 모델 개체와 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="911c5-403">Hello를 마우스 오른쪽 단추로 클릭 하 여 이렇게 **모델 학습** 모듈과 hello를 사용 하 여 **학습 된 모델로 저장** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="911c5-404">다음으로, toocreate 입력 및 출력 해야 웹 서비스에 대 한 포트:</span><span class="sxs-lookup"><span data-stu-id="911c5-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="911c5-405">입력된 포트에 대 한 예측 해야 하는 hello 데이터로 형성 동일 hello의 데이터를 받아</span><span class="sxs-lookup"><span data-stu-id="911c5-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="911c5-406">출력 포트 hello 점수가 매겨진 레이블 및 hello 관련 된 확률을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="911c5-407">Hello 입력된 포트에 대 한 데이터 행을 몇 개를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="911c5-408">편리한 toouse는는 **SQL 변환 적용** hello로 모듈 tooselect 정당한 10 행 tooserve 입력 포트 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="911c5-409">여기에 표시 된 hello SQL 쿼리를 사용 하 여 입력된 포트에 대 한 데이터의 이러한 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![입력 포트 데이터](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="911c5-411">웹 서비스</span><span class="sxs-lookup"><span data-stu-id="911c5-411">Web service</span></span>
<span data-ttu-id="911c5-412">이제 toorun toopublish 사용된 될 수 있는 작은 실험 웹 서비스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="911c5-413">웹 서비스에 대한 입력 데이터 생성</span><span class="sxs-lookup"><span data-stu-id="911c5-413">Generate input data for webservice</span></span>
<span data-ttu-id="911c5-414">0 번째 단계로, 있으므로 hello 개수 테이블 크기가 클에서는 테스트 데이터의 하면 몇 줄 되 고 개수 기능에서 데이터 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="911c5-415">이 통해 웹 서비스에 대 한 hello 입력된 데이터 형식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="911c5-416">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-416">This is shown here:</span></span>

![BDT 입력 데이터 만들기](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="911c5-418">Hello 입력된 데이터 형식에서는 이제 사용 hello hello의 출력 **Count Featurizer** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="911c5-419">이 실행이 완료 될 실험해 보고 되 면 hello에서 hello 출력을 저장 **Count Featurizer** 데이터 집합으로 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="911c5-420">이 데이터 집합은 hello hello 웹 서비스에서 입력된 데이터에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="911c5-421">웹 서비스 게시를 위한 실험 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="911c5-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="911c5-422">먼저 구조를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-422">First, we show what this looks like.</span></span> <span data-ttu-id="911c5-423">hello 필수 구조는 한 **모델 점수 매기기** 우리의 학습 된 모델 개체와 hello를 사용 하 여 hello 이전 단계에서 생성 우리는 입력된 데이터의 몇 줄을 허용 하는 모듈 **Count Featurizer** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="911c5-424">"Dataset에서 열 선택" tooproject hello 점수가 매겨진 레이블 및 hello 점수 확률을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![데이터 집합의 열 선택](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="911c5-426">Hello 어떻게 확인 **데이터 집합의 열 선택** 모듈 '필터링 하는 데' 데이터는 데이터 집합에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="911c5-427">Hello 내용 표시:</span><span class="sxs-lookup"><span data-stu-id="911c5-427">We show hello contents here:</span></span>

![데이터 집합 모듈에서 열 선택 hello를 사용 하 여 필터링](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="911c5-429">tooget hello 파란색 입력 및 출력 포트를 클릭 하면 **webservice 준비** 오른쪽 hello 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="911c5-430">이 실험을 실행할 수도 있습니다 toopublish hello 웹 서비스: hello 클릭 **웹 서비스 게시** 아이콘 hello 맨 아래 오른쪽, 표시 된 여기에서:</span><span class="sxs-lookup"><span data-stu-id="911c5-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![PUBLISH WEB SERVICE](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="911c5-432">Hello 웹 서비스를 게시 하면 리디렉션된 tooa 페이지가 따라서 구했습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![웹 서비스 대시보드](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="911c5-434">웹 서비스에 대 한 두 개의 링크가 hello 왼쪽에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="911c5-435">hello **요청/응답** 서비스 (또는 RR) 단일 예측에 대 한 것 이며이 워크샵에 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="911c5-436">hello **일괄 처리 실행** 서비스 (BES) 일괄 처리 예측에 사용 되 고 hello 사용 되는 입력된 데이터 toomake 예측 Azure Blob 저장소에 상주 하는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="911c5-437">Hello 링크를 클릭 하면 **요청/응답** tooa는 페이지를 제공 하는 C#, python 및 오른쪽에서 코드를 미리 고정 이 코드 toohello 웹 서비스 호출 하기 위한 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="911c5-438">Note 해당 hello이이 페이지의 API 키 toobe 인증에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="911c5-439">것이 편리한 toocopy hello IPython 전자 필기장의 tooa 새로운 셀을 통해이 python 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="911c5-440">여기 hello 올바른 API 키 python 코드 세그먼트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-440">Here we show a segment of python code with hello correct API key.</span></span>

![Python 코드](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="911c5-442">Note 우리의 webservices API 키와 hello 기본 API 키를 교체 했습니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="911c5-443">클릭 하면 **실행** 이 셀에 IPython 노트북 생성 응답 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="911c5-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![IPython 응답](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="911c5-445">Hello에 대 한 예제에 대 한 hello python 스크립트의 hello JSON 프레임 워크) (에 요청한 테스트 두 보면, 구했습니다 다시 hello 형태로 답변 "점수가 매겨진 레이블, 점수가 매겨진 확률"입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="911c5-446">참고는이 경우 선택한 이유 hello 기본값 hello 미리 준비 된 코드 (0의 모든 숫자 열과 모든 범주 열에 대 한 "value" hello 문자열)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="911c5-447">이것으로 마칩니다 우리의 종단 간 연습 보여 주는 방법을 Azure 기계 학습을 사용 하 여 toohandle 대규모 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="911c5-448">우리는 테라바이트 임 데이터의 시작, 예측 모델을 생성 및 hello 클라우드에서 웹 서비스로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="911c5-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

