---
title: "Azure Machine Learning에서 Hadoop 클러스터 데이터 탐색 및 모델 만들기 | Microsoft Docs"
description: "HDInsight Hadoop 클러스터를 사용하는 종단 간 시나리오에 팀 데이터 과학 프로세스를 사용하여 공개적으로 사용 가능한 데이터 집합으로 모델을 빌드 및 배포합니다."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e48d59ca467e3e7fd772389e6e48a2d81726f859
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="5681b-103">실행 중인 팀 데이터 과학 프로세스: Azure HDInsight Hadoop 클러스터 사용</span><span class="sxs-lookup"><span data-stu-id="5681b-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="5681b-104">이 연습에서는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/)를 사용하는 종단 간 시나리오에서 [TDSP(팀 데이터 과학 프로세스)](data-science-process-overview.md)를 사용하여 공개적으로 사용 가능한 [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합에서 데이터를 저장, 탐색, 기능 설계, 다운 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="5681b-105">데이터의 모델은 이진/다중 클래스 분류 및 회귀 예측 작업을 처리하기 위해 Azure 기계 학습으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="5681b-106">데이터 처리에 HDInsight Hadoop 클러스터를 사용하는 유사한 시나리오에서 더 큰 데이터 집합(1TB)을 처리하는 방법을 보여 주는 연습은 [팀 데이터 과학 프로세스 - 1TB 데이터 집합에서 Azure HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-criteo-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5681b-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="5681b-107">IPython 노트북에서 1TB 데이터 집합을 사용하는 연습의 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="5681b-108">이 방법을 사용하려면 [Hive ODBC 연결을 사용하여 Criteo 연습](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) 토픽을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="5681b-109"><a name="dataset"></a>NYC Taxi Trips 데이터 집합 설명</span><span class="sxs-lookup"><span data-stu-id="5681b-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="5681b-110">NYC Taxi Trip 데이터는 1억 7,300만 개가 넘는 개별 여정 및 각 여정의 요금으로 구성된 약 20GB의 압축된 CSV(쉼표로 구분된 값) 파일(압축되지 않은 경우 약 48GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="5681b-111">각 여정 레코드는 승차 및 하차 위치, 익명 처리된 hack(기사) 면허증 번호 및 medallion(택시의 고유 ID) 번호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="5681b-112">데이터는 2013년의 모든 여정을 포괄하며, 매월 다음 두 개의 데이터 집합으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="5681b-113">'trip_data' CSV 파일은 승객 수, 승차 및 하차 지점, 여정 기간, 여정 거리 등 여정 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="5681b-114">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="5681b-115">'trip_fare' CSV 파일은 지불 유형, 금액, 추가 요금 및 세금, 팁 및 통행료, 총 지불 금액 등 각 여정의 요금에 대한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="5681b-116">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="5681b-117">trip\_data와 trip\_fare를 조인할 고유 키는 medallion, hack\_licence 및 pickup\_datetime 필드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="5681b-118">특정 여정과 관련된 모든 세부 정보를 가져오려면 세 개의 키인 "medallion", "hack\_license" 및 "pickup\_datetime"을 사용하여 조인하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="5681b-119">데이터에 대한 보다 자세한 정보는 잠시 후 Hive 테이블을 저장할 때 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="5681b-120"><a name="mltasks"></a>예측 작업의 예제</span><span class="sxs-lookup"><span data-stu-id="5681b-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="5681b-121">데이터에 접근할 때 분석을 기반으로 수행할 예측의 종류를 결정하면 프로세스에 포함해야 하는 작업을 명확하게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="5681b-122">다음은 이 연습에서 우리가 해결할 예측 문제에 대한 3가지 예제입니다. 예제의 공식은 *tip\_amount*를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="5681b-123">**이진 분류**: 여정에 대해 팁이 지불되었는지 여부를 예측합니다. 즉, *tip\_amount*가 $0보다 크면 지불된 것이고 *tip\_amount*가 $0이면 지불되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="5681b-124">**다중 클래스 분류**: 여정에 대해 지불된 팁 금액의 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="5681b-125">*tip\_amount*를 5개의 bin 또는 클래스로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="5681b-126">**회귀 작업**: 여정에 대해 지불된 팁의 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <span data-ttu-id="5681b-127"><a name="setup"></a>고급 분석용 HDInsight Hadoop 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="5681b-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-128">이는 일반적으로 **관리자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5681b-129">다음 세 단계를 통해 HDInsight 클러스터를 사용하는 고급 분석용 Azure 환경을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="5681b-130">[저장소 계정 만들기](../storage/common/storage-create-storage-account.md):이 저장소 계정은 Azure Blob 저장소에 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="5681b-131">HDInsight 클러스터에 사용되는 데이터도 여기에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="5681b-132">[고급 분석 프로세스 및 기술을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5681b-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="5681b-133">이 단계에서는 모든 노드에 64비트 Anaconda Python 2.7이 설치된 Azure HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="5681b-134">HDInsight 클러스터 사용자 지정하는 동안 기억해야 할 중요한 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="5681b-135">HDInsight 클러스터를 만들 때 1단계에서 만든 저장소 계정을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="5681b-136">이 저장소 계정은 클러스터 내에서 처리되는 데이터에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="5681b-137">클러스터를 만든 후에는 클러스터의 헤드 노드에 대한 원격 액세스를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="5681b-138">**구성** 탭으로 이동하여 **원격 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="5681b-139">이 단계에서는 원격 로그인에 사용되는 사용자 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="5681b-140">[Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md): 이 Azure 기계 학습 작업 영역은 기계 학습 모델을 빌드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="5681b-141">이 작업은 초기 데이터 탐색을 완료하고 HDInsight 클러스터를 사용하여 다운 샘플링한 후 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <span data-ttu-id="5681b-142"><a name="getdata"></a>공용 원본에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="5681b-142"><a name="getdata"></a>Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-143">이는 일반적으로 **관리자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5681b-144">해당 공용 위치에서 [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합을 가져오려면 [Azure Blob Storage에서 데이터 이동](machine-learning-data-science-move-azure-blob.md)에 설명된 방법 중 하나를 사용하여 데이터를 컴퓨터에 복사하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="5681b-145">여기에서는 AzCopy를 사용하여 데이터가 포함된 파일을 전송하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="5681b-146">AzCopy를 다운로드하여 설치하려면 [AzCopy 명령줄 유틸리티 시작](../storage/common/storage-use-azcopy.md)지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="5681b-147">명령 프롬프트 창에서 *<path_to_data_folder>*를 원하는 대상으로 바꿔 다음 AzCopy 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="5681b-148">복사가 완료되면 총 24개의 압축된 파일이 선택한 데이터 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="5681b-149">로컬 컴퓨터에서 동일한 디렉터리에 다운로드한 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="5681b-150">압축을 푼 파일이 있는 폴더를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="5681b-151">이 폴더를 *<path\_to\_unzipped_data\_files\>*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="5681b-152"><a name="upload"></a>Azure HDInsight Hadoop 클러스터의 기본 컨테이너에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="5681b-152"><a name="upload"></a>Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-153">이는 일반적으로 **관리자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5681b-154">다음 AzCopy 명령에서 다음 매개 변수를 Hadoop 클러스터를 만들고 데이터 파일의 압축을 풀 때 지정한 실제 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="5681b-155">***&#60;path_to_data_folder>*** - 압축을 푼 데이터 파일이 들어 있는 컴퓨터의 디렉터리(경로와 함께)</span><span class="sxs-lookup"><span data-stu-id="5681b-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="5681b-156">***&#60;storage account name of Hadoop cluster>*** - HDInsight 클러스터와 연결된 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="5681b-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="5681b-157">***&#60;default container of Hadoop cluster>*** - 클러스터에서 사용하는 기본 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="5681b-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="5681b-158">기본 컨테이너의 이름은 일반적으로 클러스터 자체의 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="5681b-159">예를 들어 클러스터가 "abc123.azurehdinsight.net"인 경우 기본 컨테이너는 abc123입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="5681b-160">***&#60;storage account key>*** - 클러스터에서 사용하는 저장소 계정의 키</span><span class="sxs-lookup"><span data-stu-id="5681b-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="5681b-161">명령 프롬프트 또는 컴퓨터의 Windows PowerShell 창에서 다음 두 AzCopy 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="5681b-162">이 명령은 여정 데이터를 Hadoop 클러스터의 기본 컨테이너에 있는 ***nyctaxitripraw*** 디렉터리에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="5681b-163">이 명령은 요금 데이터를 Hadoop 클러스터의 기본 컨테이너에 있는 ***nyctaxifareraw*** 디렉터리에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="5681b-164">이제 데이터가 Azure Blob 저장소에 있고 HDInsight 클러스터 내에서 사용할 수 있도록 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <span data-ttu-id="5681b-165"><a name="#download-hql-files"></a>Hadoop 클러스터의 헤드 노드에 로그인하여 예비 데이터 분석 준비</span><span class="sxs-lookup"><span data-stu-id="5681b-165"><a name="#download-hql-files"></a>Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-166">이는 일반적으로 **관리자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5681b-167">예비 데이터 분석 및 데이터 다운 샘플링을 위해 클러스터의 헤드 노드에 액세스하려면 [Hadoop 클러스터의 헤드 노드 액세스](machine-learning-data-science-customize-hadoop-cluster.md#headnode)에 설명된 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="5681b-168">이 연습에서는 주로 SQL과 유사한 쿼리 언어인 [Hive](https://hive.apache.org/)로 작성된 쿼리를 사용하여 예비 데이터 탐색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="5681b-169">Hive 쿼리는 .hql 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="5681b-170">그런 다음 모델 빌드를 위해 Azure 기계 학습 내에서 사용하도록 이 데이터를 다운 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="5681b-171">예비 데이터 분석을 위해 클러스터를 준비하려면 [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)에서 관련 Hive 스크립트가 포함된 .hql 파일을 헤드 노드의 로컬 디렉터리(C:\temp)에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="5681b-172">이렇게 하려면 클러스터의 헤드 노드 내에서 **명령 프롬프트** 를 열고 다음 두 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="5681b-173">이 두 명령은 이 연습에 필요한 모든 .hql 파일을 헤드 노드의 로컬 디렉터리 ***C:\temp&#92;***에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <span data-ttu-id="5681b-174"><a name="#hive-db-tables"></a>월별로 분할된 Hive 데이터베이스 및 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="5681b-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-175">이는 일반적으로 **관리자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5681b-176">이제 NYC taxi 데이터 집합에 대한 Hive 테이블을 만들 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="5681b-177">Hadoop 클러스터 헤드 노드의 바탕 화면에서 ***Hadoop 명령줄*** 을 열고 명령을 입력하여 Hive 디렉터리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="5681b-178">**이 연습의 모든 Hive 명령은 위의 Hive bin/ 디렉터리 프롬프트에서 실행합니다. 경로 문제가 자동으로 해결됩니다. "Hive 디렉터리 프롬프트", "Hive bin/ 디렉터리 프롬프트" 및 "Hadoop 명령줄"은 이 연습에서 상호 교환적으로 사용되는 용어입니다.**</span><span class="sxs-lookup"><span data-stu-id="5681b-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="5681b-179">Hive 디렉터리 프롬프트에서 헤드 노드의 Hadoop 명령줄에 다음 명령을 입력하여 Hive 데이터베이스 및 테이블을 만드는 Hive 쿼리를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="5681b-180">다음은 Hive 데이터베이스 ***nyctaxidb***와 테이블 ***trip*** 및 ***fare***를 만드는 ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** 파일의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="5681b-181">이 Hive 스크립트는 두 개의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="5681b-182">"trip" 테이블은 각 승객의 여정 세부 정보(운전 기사 정보, 승차 시간, 여정 거리 및 시간)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="5681b-183">"fare" 테이블은 요금 세부 정보(요금 금액, 팁 금액, 통행료 및 추가 요금)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="5681b-184">이러한 절차에 대한 도움이 필요하거나 다른 방법을 조사하려는 경우 [Hadoop 명령줄에서 직접 Hive 쿼리 제출](machine-learning-data-science-move-hive-tables.md#submit) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5681b-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="5681b-185"><a name="#load-data"></a>분할된 Hive 테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="5681b-185"><a name="#load-data"></a>Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-186">이는 일반적으로 **관리자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5681b-187">NYC taxi 데이터 집합에는 처리 및 쿼리 시간을 단축하기 위해 사용하는 월별 자연 분할 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="5681b-188">아래의 PowerShell 명령( **Hadoop 명령줄**을 사용하여 Hive 디렉터리에서 실행)은 월별로 분할된 "trip" 및 "fare" Hive 테이블에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="5681b-189">*sample\_hive\_load\_data\_by\_partitions.hql* 파일에는 다음 **LOAD** 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="5681b-190">탐색 프로세스에서 사용한 Hive 쿼리 수에는 단일 파티션 또는 두 파티션에서 탐색한 횟수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="5681b-191">그러나 이러한 쿼리는 전체 데이터에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-191">But these queries could be run across the entire data.</span></span>

### <span data-ttu-id="5681b-192"><a name="#show-db"></a>HDInsight Hadoop 클러스터에서 데이터베이스 표시</span><span class="sxs-lookup"><span data-stu-id="5681b-192"><a name="#show-db"></a>Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="5681b-193">HDInsight Hadoop 클러스터에서 만든 데이터베이스를 Hadoop 명령줄 창 내에 표시하려면 Hadoop 명령줄에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="5681b-194"><a name="#show-tables"></a>nyctaxidb 데이터베이스에서 Hive 테이블 표시</span><span class="sxs-lookup"><span data-stu-id="5681b-194"><a name="#show-tables"></a>Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="5681b-195">nyctaxidb 데이터베이스에서 테이블을 표시하려면 Hadoop 명령줄에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="5681b-196">아래 명령을 실행하여 테이블이 분할되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="5681b-197">예상 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-197">The expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="5681b-198">마찬가지로 아래 명령을 실행하여 fare 테이블이 분할되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="5681b-199">예상 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-199">The expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="5681b-200"><a name="#explore-hive"></a>Hive에서 데이터 탐색 및 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="5681b-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-201">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-202">Hive 테이블에 로드된 데이터에 대한 데이터 탐색 및 기능 엔지니어링 작업은 Hive 쿼리를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="5681b-203">다음은 이 섹션에서 설명할 이러한 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="5681b-204">두 테이블의 상위 10개 레코드를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="5681b-205">다양한 기간에 걸쳐 몇몇 필드의 데이터 분포를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="5681b-206">경도 및 위도 필드의 데이터 품질을 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="5681b-207">**tip\_amount**에 따라 이진 및 다중 클래스 분류 레이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="5681b-208">직접 여정 거리를 계산하여 기능을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="5681b-209">탐색: trip 테이블의 상위 10개 레코드 보기</span><span class="sxs-lookup"><span data-stu-id="5681b-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-210">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-211">데이터 모양을 보려면 각 테이블에서 10개의 레코드를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="5681b-212">Hadoop 명령줄 콘솔의 Hive 디렉터리 프롬프트에서 다음 두 쿼리를 따로 실행하여 레코드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="5681b-213">첫째 달의 "trip" 테이블에서 상위 10개의 레코드를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="5681b-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="5681b-214">첫째 달의 "fare" 테이블에서 상위 10개의 레코드를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="5681b-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="5681b-215">보기 편하도록 레코드를 파일로 저장하는 것이 유용한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="5681b-216">위 쿼리를 약간 변경하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="5681b-217">탐색: 각 12개 파티션의 각 레코드 수 보기</span><span class="sxs-lookup"><span data-stu-id="5681b-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-218">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-219">연간 여정 수가 어떻게 다른지 확인하려는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="5681b-220">월별로 그룹화를 통해 이 여정 분포를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="5681b-221">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-221">This gives us the output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="5681b-222">여기서 첫 번째 열은 월이고, 두 번째 열은 해당 월의 여정 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="5681b-223">Hive 디렉터리 프롬프트에서 다음 명령을 실행하여 여정 데이터 집합의 총 레코드 수를 계산할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="5681b-224">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="5681b-225">trip 데이터 집합에 표시된 것과 유사한 명령을 사용하여 Hive 디렉터리 프롬프트에서 fare 데이터 집합에 대해 레코드 수를 확인하는 Hive 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="5681b-226">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-226">This gives us the output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="5681b-227">두 데이터 집합 모두에 대해 정확히 동일한 월별 여정 수가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="5681b-228">이는 데이터가 올바르게 로드되었는지 확인하는 첫 번째 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="5681b-229">Hive 디렉터리 프롬프트에서 아래 명령을 사용하여 fare 데이터 집합의 총 레코드 수를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="5681b-230">다음과 같은 결과가 산출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="5681b-231">두 테이블 모두의 총 레코드 수가 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="5681b-232">이는 데이터가 올바르게 로드되었는지 확인하는 두 번째 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="5681b-233">탐색: medallion별 여정 분포</span><span class="sxs-lookup"><span data-stu-id="5681b-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-234">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-235">이 예제에서는 지정된 기간 내의 여정이 100개가 넘는 medallion(택시 번호)을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="5681b-236">쿼리는 파티션 변수 **month**의 영향을 받기 때문에 테이블을 분할하면 쿼리 성능이 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="5681b-237">쿼리 결과는 `C:\temp` 헤드 노드의 로컬 파일 queryoutput.tsv에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="5681b-238">다음은 검사할 *sample\_hive\_trip\_count\_by\_medallion.hql* 파일의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="5681b-239">NYC taxi 데이터 집합의 medallion은 고유한 택시를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="5681b-240">특정 기간에 특정 여정 수를 초과하는 택시를 조회하여 "운행량이 많은" 택시를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="5681b-241">다음 예제에서는 첫 3개월 동안 여정 수가 100건이 넘는 택시를 식별하여 쿼리 결과를 로컬 파일 C:\temp\queryoutput.tsv에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="5681b-242">다음은 검사할 *sample\_hive\_trip\_count\_by\_medallion.hql* 파일의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="5681b-243">Hive 디렉터리 프롬프트에서 아래 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="5681b-244">탐색: medallion 및 hack_license별 여정 분포</span><span class="sxs-lookup"><span data-stu-id="5681b-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-245">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-246">데이터 집합을 탐색할 때 값 그룹의 동시 발생 횟수를 조사하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="5681b-247">이 섹션에서는 택시와 운전 기사에 대해 이 작업을 수행하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="5681b-248">*sample\_hive\_trip\_count\_by\_medallion\_license.hql* 파일은 "medallion" 및 "hack_license"에서 fare 데이터 집합을 그룹화하고 각 조합의 개수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="5681b-249">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="5681b-250">이 쿼리는 택시와 특정 운전 기사의 조합을 여정 수 내림차순으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="5681b-251">Hive 디렉터리 프롬프트에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="5681b-252">쿼리 결과는 로컬 파일 C:\temp\queryoutput.tsv에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="5681b-253">탐색: 잘못된 경도/위도 레코드를 확인하여 데이터 품질 평가</span><span class="sxs-lookup"><span data-stu-id="5681b-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-254">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-255">예비 데이터 분석의 일반적인 목적은 유효하지 않거나 잘못된 레코드를 걸러내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="5681b-256">이 섹션의 예제에서는 위도 또는 경도 필드에 NYC 영역 밖의 값이 포함되어 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="5681b-257">이러한 레코드에는 잘못된 경도-위도 값이 있을 수 있기 때문에 모델링에 사용할 데이터에서 이를 제거하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="5681b-258">다음은 검사할 *sample\_hive\_quality\_assessment.hql* 파일의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="5681b-259">Hive 디렉터리 프롬프트에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="5681b-260">이 명령에 포함된 *-S* 인수는 Hive 맵/감소 작업의 상태 화면 인쇄를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="5681b-261">이렇게 하면 Hive 쿼리 출력의 화면 인쇄를 좀 더 쉽게 읽을 수 있으므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="5681b-262">탐색: 여정 팁의 이진 클래스 분포</span><span class="sxs-lookup"><span data-stu-id="5681b-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-263">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-264">[예측 작업의 예제](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 섹션에 설명된 이진 분류 문제의 경우 팁 제공 여부를 아는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="5681b-265">이 팁 분포는 이진입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="5681b-266">tip given(Class 1, tip\_amount > $0)</span><span class="sxs-lookup"><span data-stu-id="5681b-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="5681b-267">no tip (Class 0, tip\_amount = $0).</span><span class="sxs-lookup"><span data-stu-id="5681b-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="5681b-268">아래에 나온 *sample\_hive\_tipped\_frequencies.hql* 파일에서 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="5681b-269">Hive 디렉터리 프롬프트에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="5681b-270">탐색: 다중 클래스 설정의 클래스 분포</span><span class="sxs-lookup"><span data-stu-id="5681b-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-271">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-272">[예측 작업의 예제](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 섹션에 설명된 다중 클래스 분류 문제의 경우 이 데이터 집합은 제공된 팁 금액을 예측할 수 있는 자연 분류 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="5681b-273">bin을 사용하여 쿼리에서 팁 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="5681b-274">여러 팁 범위에 대한 클래스 분포를 가져오려면 *sample\_hive\_tip\_range\_frequencies.hql* 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="5681b-275">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="5681b-276">Hadoop 명령줄 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="5681b-277">탐색: 두 경도-위도 위치 간의 직접 거리 계산</span><span class="sxs-lookup"><span data-stu-id="5681b-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-278">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-279">직접 거리를 측정하면 직접 거리와 실제 여정 거리 간의 불일치를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="5681b-280">이 기능이 필요한 이유는 승객이 운전 기사가 의도적으로 훨씬 더 긴 경로를 이용했는지 알면 팁을 제공하지 않을 것이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="5681b-281">실제 여정 거리와 두 경도-위도 지점 간의 [Haversine 거리](http://en.wikipedia.org/wiki/Haversine_formula) ("대권" 거리)를 비교하려면 Hive 내에서 제공되는 삼각 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="5681b-282">위 쿼리에서 R은 지구의 반경(마일)이고, pi는 라디안으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="5681b-283">경도-위도 지점은 NYC 영역에서 멀리 떨어진 값을 제거하기 위해 "필터링"됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="5681b-284">이 예제에서는 결과를 "queryoutputdir"이라는 디렉터리에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="5681b-285">아래 표시된 명령 시퀀스는 먼저 이 출력 디렉터리를 만든 다음 Hive 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="5681b-286">Hive 디렉터리 프롬프트에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="5681b-287">쿼리 결과는 Hadoop 클러스터 기본 컨테이너 아래의 9개의 Azure Blob(***queryoutputdir/000000\_0*** ~  ***queryoutputdir/000008\_0***)에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="5681b-288">개별 blob의 크기를 보려면 Hive 디렉터리 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="5681b-289">지정된 파일, 즉 000000\_0의 내용을 보려면 Hadoop의 `copyToLocal` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="5681b-290">`copyToLocal`은 파일이 큰 경우 매우 느려질 수 있으므로 큰 파일에 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="5681b-291">이 데이터를 Azure blob에 두면 [데이터 가져오기][import-data] 모듈을 사용하여 Azure 기계 학습 내에서 데이터를 탐색할 수 있는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <span data-ttu-id="5681b-292"><a name="#downsample"></a>Azure 기계 학습에서 데이터 다운 샘플링 및 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="5681b-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="5681b-293">이는 일반적으로 **데이터 과학자** 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5681b-294">예비 데이터 분석 단계를 마쳤으므로 이제 Azure 기계 학습에서 모델을 빌드하기 위한 데이터를 다운 샘플링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="5681b-295">이 섹션에서는 Hive 쿼리를 사용하여 Azure 기계 학습의 [데이터 가져오기][import-data] 모듈에서 액세스할 데이터를 다운 샘플링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="5681b-296">데이터 다운 샘플링</span><span class="sxs-lookup"><span data-stu-id="5681b-296">Down sampling the data</span></span>
<span data-ttu-id="5681b-297">이 절차에는 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-297">There are two steps in this procedure.</span></span> <span data-ttu-id="5681b-298">먼저 모든 레코드에 있는 세 개의 키("medallion", "hack\_license" 및 "pickup\_datetime")에서 **nyctaxidb.trip** 및 **nyctaxidb.fare** 테이블을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="5681b-299">그런 다음, 이진 분류 레이블 **tipped**와 다중 클래스 분류 레이블 **tip\_class**를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="5681b-300">다운 샘플링한 데이터를 Azure 기계 학습의 [데이터 가져오기][import-data] 모듈에서 직접 사용하려면 위 쿼리 결과를 내부 Hive 테이블에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="5681b-301">내부 Hive 테이블을 만들고 조인 및 다운 샘플링된 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="5681b-302">이 쿼리는 표준 Hive 함수를 직접 적용하여 "pickup\_datetime" 필드에서 시간, 주, 요일(월요일은 1, 토요일은 7)을 생성하고 승차 위치와 하차 위치 간의 직접 거리를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="5681b-303">이러한 항목의 전체 목록은 [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) 에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="5681b-304">그런 다음 이 쿼리는 쿼리 결과가 Azure 기계 학습 스튜디오에 적합하도록 데이터를 다운 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="5681b-305">원래 데이터 집합의 약 1%만 스튜디오로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="5681b-306">다음은 Azure Machine Learning에서 모델 빌드를 위한 데이터를 준비하는 *sample\_hive\_prepare\_for\_aml\_full.hql* 파일의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of the join into the above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="5681b-307">이 쿼리를 실행하려면 Hive 디렉터리 프롬프트에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="5681b-308">이제 Azure 기계 학습의 [데이터 가져오기][import-data] 모듈을 사용하여 액세스할 수 있는 내부 테이블 "nyctaxidb.nyctaxi_downsampled_dataset"가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="5681b-309">또한 이 데이터 집합을 사용하여 기계 학습 모델을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="5681b-310">Azure 기계 학습의 데이터 가져오기 모듈을 사용하여 다운 샘플링된 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="5681b-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="5681b-311">Azure 기계 학습의 [데이터 가져오기][import-data] 모듈에서 Hive 쿼리를 실행하려면 Azure Machine Learning 작업 영역과 클러스터 및 연결된 해당 저장소 계정의 자격 증명에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="5681b-312">[데이터 가져오기][import-data] 모듈과 입력할 매개 변수에 대한 일부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="5681b-313">**HCatalog server URI**: 클러스터 이름이 abc123인 경우 단순히 https://abc123.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="5681b-314">**Hadoop user account name**: 클러스터에 대해 선택한 사용자 이름(원격 액세스 사용자 이름이 **아님**)입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="5681b-315">**Hadoop ser account password**: 클러스터에 대해 선택한 암호(원격 액세스 암호가 **아님**)입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="5681b-316">**Location of output data** : Azure로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="5681b-317">**Azure storage account name** : 클러스터와 연결된 기본 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="5681b-318">**Azure container name** : 클러스터의 기본 컨테이너 이름이며, 일반적으로 클러스터 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="5681b-319">"abc123"이라는 클러스터의 경우 단순히 abc123입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5681b-320">**Azure Machine Learning의 [데이터 가져오기][import-data] 모듈을 사용하여 쿼리할 모든 테이블은 내부 테이블이어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5681b-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="5681b-321">데이터베이스 D.db의 테이블 T가 내부 테이블인지 확인하기 위한 팁은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="5681b-322">Hive 디렉터리 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="5681b-323">테이블이 내부 테이블이고 채워진 경우 해당 내용이 여기에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="5681b-324">테이블이 내부 테이블인지 확인하는 또 다른 방법은 Azure 저장소 탐색기를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="5681b-325">Azure 저장소 탐색기를 사용하여 클러스터의 기본 컨테이너 이름으로 이동한 다음 테이블 이름으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="5681b-326">테이블과 해당 내용이 표시되면 내부 테이블인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="5681b-327">다음은 Hive 쿼리 및 [데이터 가져오기][import-data] 모듈의 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![데이터 가져오기 모듈에 대한 Hive 쿼리](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="5681b-329">다운 샘플링된 데이터는 기본 컨테이너에 있으므로 Azure Machine Learning의 결과 Hive 쿼리는 매우 단순하며 "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data"입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="5681b-330">이제 이 데이터 집합을 기계 학습 모델 빌드를 위한 시작 지점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="5681b-331"><a name="mlmodel"></a>Azure 기계 학습에서 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="5681b-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="5681b-332">이제 [Azure 기계 학습](https://studio.azureml.net)에서 모델 빌드 및 모델 배포를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="5681b-333">위에서 파악된 다음과 같은 예측 문제를 해결하는 데 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="5681b-334">**1. 이진 분류**: 여정에 대해 팁이 지불되었는지 여부를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="5681b-335">**사용된 학습자:** 2클래스 로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="5681b-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="5681b-336">a.</span><span class="sxs-lookup"><span data-stu-id="5681b-336">a.</span></span> <span data-ttu-id="5681b-337">이 문제의 경우 대상(또는 클래스) 레이블은 "tipped"입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="5681b-338">원래 다운 샘플링된 데이터 집합에는 이 분류 실험에 대한 대상 누수인 몇 가지 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="5681b-339">특히 tip\_class, tip\_amount 및 total\_amount는 테스트 시 사용할 수 없는 대상 레이블에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="5681b-340">[데이터 집합의 열 선택][select-columns] 모듈을 사용하여 이러한 열을 고려 대상에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5681b-341">아래 스냅숏은 주어진 여정에 대해 팁이 지불되었는지 여부를 예측하는 실험을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![실험 스냅숏](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="5681b-343">b.</span><span class="sxs-lookup"><span data-stu-id="5681b-343">b.</span></span> <span data-ttu-id="5681b-344">이 실험의 경우 대상 레이블 분포는 약 1:1입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="5681b-345">아래 스냅숏은 이진 분류 문제에 대한 팁 클래스 레이블의 분포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![팁 클래스 레이블의 분포](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="5681b-347">결과적으로, 아래 그림에 표시된 것처럼 AUC는 0.987입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![AUC 값](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="5681b-349">**2. 다중 클래스 분류**: 이전에 정의된 클래스를 사용하여 여정에 대해 지불된 팁 금액 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="5681b-350">**사용된 학습자:** 다중 클래스 로지스틱 회귀</span><span class="sxs-lookup"><span data-stu-id="5681b-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="5681b-351">a.</span><span class="sxs-lookup"><span data-stu-id="5681b-351">a.</span></span> <span data-ttu-id="5681b-352">이 문제의 경우 대상(또는 클래스) 레이블은 5개 값(0, 1, 2, 3, 4) 중 하나일 수 있는 "tip\_class"입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="5681b-353">이진 분류와 마찬가지로 이 실험에 대한 대상 누수인 몇 개 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="5681b-354">특히 tipped, tip\_amount, total\_amount는 테스트 시 사용할 수 없는 대상 레이블에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="5681b-355">[데이터 집합의 열 선택][select-columns] 모듈을 사용하여 이러한 열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5681b-356">아래 스냅숏은 팁이 속할 수 있는 bin을 예측하는 실험을 보여 줍니다(Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20).</span><span class="sxs-lookup"><span data-stu-id="5681b-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![실험 스냅숏](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="5681b-358">실제 테스트 클래스 분포는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="5681b-359">Class 0과 Class 1은 우세한 반면, 다른 클래스는 희박합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![테스트 클래스 분포](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="5681b-361">b.</span><span class="sxs-lookup"><span data-stu-id="5681b-361">b.</span></span> <span data-ttu-id="5681b-362">이 실험에서는 혼동 행렬을 사용하여 예측 정확도를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="5681b-363">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-363">This is shown below.</span></span>

![혼동 행렬](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="5681b-365">우세한 클래스의 클래스 정확도는 매우 좋지만 희박한 클래스에서 "학습"하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="5681b-366">**3. 회귀 작업**: 여정에 대해 지불된 팁의 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="5681b-367">**사용된 학습자:** 향상된 의사 결정 트리</span><span class="sxs-lookup"><span data-stu-id="5681b-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="5681b-368">a.</span><span class="sxs-lookup"><span data-stu-id="5681b-368">a.</span></span> <span data-ttu-id="5681b-369">이 문제의 경우 대상(또는 클래스) 레이블은 "tip\_amount"입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="5681b-370">이 경우 대상 누수는 tipped, tip\_class, total\_amount입니다. 이러한 변수는 모두 일반적으로 테스트 시 사용할 수 없는 팁 금액에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="5681b-371">[데이터 집합의 열 선택][select-columns] 모듈을 사용하여 이러한 열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5681b-372">아래 스냅숏에서는 주어진 팁 금액을 예측하는 실험을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![실험 스냅숏](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="5681b-374">b.</span><span class="sxs-lookup"><span data-stu-id="5681b-374">b.</span></span> <span data-ttu-id="5681b-375">회귀 문제의 경우 예측의 제곱된 오류, 결정 계수 등을 확인하여 예측 정확도를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="5681b-376">아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-376">We show these below.</span></span>

![예측 통계](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="5681b-378">결정 계수가 0.709인데, 이는 분산의 약 71%가 모델 계수로 설명됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5681b-379">Azure Machine Learning 및 이를 사용하고 액세스하는 방법에 대한 자세한 내용은 [Machine Learning이란?](machine-learning-what-is-machine-learning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5681b-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="5681b-380">Azure 기계 학습의 다양한 기계 학습 실험을 활용하는 데 매우 유용한 리소스는 [Cortana Intelligence 갤러리](https://gallery.cortanaintelligence.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="5681b-381">갤러리에는 다양한 실험이 있으며, Azure 기계 학습의 광범위한 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="5681b-382">라이선스 정보</span><span class="sxs-lookup"><span data-stu-id="5681b-382">License Information</span></span>
<span data-ttu-id="5681b-383">이 샘플 연습 및 함께 제공되는 스크립트는 Microsoft에서 MIT 라이선스에 따라 공유하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5681b-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="5681b-384">자세한 내용은 GitHub의 샘플 코드 디렉터리에 있는 LICENSE.txt 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5681b-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="5681b-385">참조</span><span class="sxs-lookup"><span data-stu-id="5681b-385">References</span></span>
<span data-ttu-id="5681b-386">• [Andrés Monroy NYC Taxi Trips 다운로드 페이지](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="5681b-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="5681b-387">• [Chris Whong의 FOILing NYC Taxi Trip 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="5681b-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="5681b-388">• [NYC Taxi 및 Limousine 수수료 연구 및 통계](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="5681b-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
