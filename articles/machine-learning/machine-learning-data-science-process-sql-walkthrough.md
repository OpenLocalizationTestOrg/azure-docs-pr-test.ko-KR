---
title: "Azure VM에서 SQL Server를 사용하여 기계 학습 모델 빌드 및 배포 | Microsoft Docs"
description: "활성 중인 고급 분석 프로세스 및 기술"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 6c5361c7e47209c8eb4d5630b44b3dcfeedeaf01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="1e000-103">실행 중인 팀 데이터 과학 프로세스: SQL Server 사용</span><span class="sxs-lookup"><span data-stu-id="1e000-103">The Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="1e000-104">이 자습서에서는 SQL Server 및 공개적으로 사용할 수 있는 데이터 집합([NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합)을 사용하여 Machine Learning 모델의 배포 및 빌드 처리를 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-104">In this tutorial, you walk through the process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="1e000-105">이 절차는 표준 데이터 과학 워크플로를 따릅니다. 데이터를 수집 및 탐색하고 학습이 용이하도록 기능을 엔지니어링한 후 모델을 빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-105">The procedure follows a standard data science workflow: ingest and explore the data, engineer features to facilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="1e000-106"><a name="dataset"></a>NYC Taxi Trips 데이터 집합 설명</span><span class="sxs-lookup"><span data-stu-id="1e000-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="1e000-107">NYC Taxi Trip 데이터는 1억 7,300만 개가 넘는 개별 여정 및 각 여정의 요금으로 구성된 약 20GB의 압축된 CSV 파일(압축되지 않은 경우 약 48GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-107">The NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="1e000-108">각 여정 레코드는 승차 및 하차 위치, 익명 처리된 hack(기사) 면허증 번호 및 medallion(택시의 고유 ID) 번호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-108">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="1e000-109">데이터는 2013년의 모든 여정을 포괄하며, 매월 다음 두 개의 데이터 집합으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-109">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="1e000-110">'trip_data' CSV는 승객 수, 승차 및 하차 지점, 여정 기간, 여정 거리 등 여정 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-110">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="1e000-111">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="1e000-112">'trip_fare' CSV는 지불 유형, 금액, 추가 요금 및 세금, 팁 및 통행료, 총 지불 금액 등 각 여정의 요금에 대한 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-112">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="1e000-113">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="1e000-114">trip\_data와 trip\_fare를 조인할 고유 키는 medallion, hack\_licence 및 pickup\_datetime 필드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-114">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="1e000-115"><a name="mltasks"></a>예측 작업의 예제</span><span class="sxs-lookup"><span data-stu-id="1e000-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="1e000-116">*tip\_amount*를 기반으로 다음 세 가지 예측 문제를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-116">We will formulate three prediction problems based on the *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="1e000-117">이진 분류: 여정에 대해 팁이 지불되었는지 여부를 예측합니다. 즉, *tip\_amount*가 $0보다 크면 지불된 것이고 *tip\_amount*가 $0이면 지불되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="1e000-118">다중 클래스 분류: 여정에 대해 지불된 팁의 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-118">Multiclass classification: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="1e000-119">*tip\_amount*를 5개의 bin 또는 클래스로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-119">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="1e000-120">회귀 작업: 여정에 대해 지불된 팁의 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-120">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="1e000-121"><a name="setup"></a>고급 분석을 위한 Azure 데이터 과학 환경 설정</span><span class="sxs-lookup"><span data-stu-id="1e000-121"><a name="setup"></a>Setting Up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="1e000-122">[환경 계획 가이드](machine-learning-data-science-plan-your-environment.md) 에서 볼 수 있듯이 Azure에서 NYC Taxi Trips 데이터 집합으로 작업할 수 있는 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-122">As you can see from the [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options to work with the NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="1e000-123">Azure Blob의 데이터로 작업한 다음 Azure 기계 학습에서 모델링</span><span class="sxs-lookup"><span data-stu-id="1e000-123">Work with the data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="1e000-124">SQL Server 데이터베이스로 데이터를 로드한 다음 Azure 기계 학습에서 모델링</span><span class="sxs-lookup"><span data-stu-id="1e000-124">Load the data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="1e000-125">이 자습서에서는 SQL Server Management Studio 및 IPython Notebook을 사용하여 대량의 데이터를 SQL Server로 병렬로 가져오기, 데이터 탐색, 기능 엔지니어링 및 다운 샘플링을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-125">In this tutorial we will demonstrate parallel bulk import of the data to a SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="1e000-126">[샘플 스크립트](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) 및 [IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)은 GitHub에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="1e000-127">Azure Blob의 데이터로 작업하는 샘플 IPython Notebook도 같은 위치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-127">A sample IPython notebook to work with the data in Azure blobs is also available in the same location.</span></span>

<span data-ttu-id="1e000-128">Azure 데이터 과학 환경을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="1e000-128">To set up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="1e000-129">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1e000-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="1e000-130">Azure 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="1e000-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="1e000-131">[데이터 과학 가상 컴퓨터 프로비전](machine-learning-data-science-setup-sql-server-virtual-machine.md)(SQL Server 및 IPython Notebook 서버 제공)</span><span class="sxs-lookup"><span data-stu-id="1e000-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1e000-132">샘플 스크립트와 IPython Notebook은 설정 프로세스 중에 데이터 과학 가상 컴퓨터로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-132">The sample scripts and IPython notebooks will be downloaded to your Data Science virtual machine during the setup process.</span></span> <span data-ttu-id="1e000-133">VM 사후 설치 스크립트가 완료되면 샘플이 VM의 문서 라이브러리에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-133">When the VM post-installation script completes, the samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="1e000-134">샘플 스크립트: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="1e000-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="1e000-135">샘플 IPython Notebook: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="1e000-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="1e000-136">where `<user_name>` 은(는) VM의 Windows 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="1e000-137">샘플 폴더는 **Sample Scripts** 및 **Sample IPython Notebooks**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-137">We will refer to the sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="1e000-138">데이터 집합 크기, 데이터 원본 위치 및 선택한 Azure 대상 환경에 따라 이 시나리오는 [시나리오 \#5: 로컬 파일에서 큰 데이터집합, Azure VM에서 대상 SQL Server](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb)와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-138">Based on the dataset size, data source location, and the selected Azure target environment, this scenario is similar to [Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="1e000-139"><a name="getdata"></a>공용 원본에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="1e000-139"><a name="getdata"></a>Get the Data from Public Source</span></span>
<span data-ttu-id="1e000-140">해당 공용 위치에서 [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합을 가져오려면 [Azure Blob Storage에서 데이터 이동](machine-learning-data-science-move-azure-blob.md)에 설명된 방법 중 하나를 사용하여 데이터를 새 가상 컴퓨터에 복사하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-140">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your new virtual machine.</span></span>

<span data-ttu-id="1e000-141">AzCopy를 사용하여 데이터를 복사하려면</span><span class="sxs-lookup"><span data-stu-id="1e000-141">To copy the data using AzCopy:</span></span>

1. <span data-ttu-id="1e000-142">VM(가상 컴퓨터)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-142">Log in to your virtual machine (VM)</span></span>
2. <span data-ttu-id="1e000-143">VM의 데이터 디스크에서 새 디렉터리를 만듭니다(참고: VM과 함께 제공되는 임시 디스크를 데이터 디스크로 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-143">Create a new directory in the VM's data disk (Note: Do not use the Temporary Disk which comes with the VM as a Data Disk).</span></span>
3. <span data-ttu-id="1e000-144">명령 프롬프트 창에서 <path_to_data_folder>를 (2)에서 만든 데이터 폴더로 바꿔 다음 Azcopy 명령줄을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-144">In a Command Prompt window, run the following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="1e000-145">AzCopy가 완료되면 데이터 폴더에 총 24개의 압축된 CSV 파일(trip\_data 파일 12개와 trip\_fare 12개)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-145">When the AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in the data folder.</span></span>
4. <span data-ttu-id="1e000-146">다운로드한 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-146">Unzip the downloaded files.</span></span> <span data-ttu-id="1e000-147">압축을 푼 파일이 있는 폴더를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-147">Note the folder where the uncompressed files reside.</span></span> <span data-ttu-id="1e000-148">이 폴더를 <path\_to\_data\_files\>라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-148">This folder will be referred to as the <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="1e000-149"><a name="dbload"></a>SQL Server 데이터베이스로 대량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="1e000-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="1e000-150">*분할된 테이블 및 뷰*를 사용하여 대량의 데이터를 SQL Database로 로드/전송하고 이후에 쿼리하는 성능을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-150">The performance of loading/transferring large amounts of data to an SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="1e000-151">이 섹션에서는 [SQL 파티션 테이블을 사용하여 병렬로 대량 데이터 가져오기](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) 에 설명된 지침에 따라 새 데이터베이스를 만들고 데이터를 분할된 테이블로 병렬로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-151">In this section, we will follow the instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) to create a new database and load the data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="1e000-152">VM에 로그인한 상태로 **SQL Server Management Studio**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-152">While logged in to your VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="1e000-153">Windows 인증을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="1e000-153">Connect using Windows Authentication.</span></span>
   
    ![SSMS 연결][12]
3. <span data-ttu-id="1e000-155">SQL Server 인증 모드를 변경하여 새 SQL 로그인 사용자를 만드는 작업을 아직 수행하지 않은 경우 **Sample Scripts** 폴더에서 **change\_auth.sql**이라는 스크립트 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-155">If you have not yet changed the SQL Server authentication mode and created a new SQL login user, open the script file named **change\_auth.sql** in the **Sample Scripts** folder.</span></span> <span data-ttu-id="1e000-156">기본 사용자 이름 및 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-156">Change the  default user name and password.</span></span> <span data-ttu-id="1e000-157">도구 모음에서 **!실행** 을 클릭하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-157">Click **!Execute** in the toolbar to run the script.</span></span>
   
    ![스크립트 실행][13]
4. <span data-ttu-id="1e000-159">SQL Server 기본 데이터베이스 및 로그 폴더를 확인하거나 변경하여 새로 만든 데이터베이스가 데이터 디스크에 저장되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-159">Verify and/or change the SQL Server default database and log folders to ensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="1e000-160">데이터 웨어하우징 로드에 최적화된 SQL Server VM 이미지는 데이터 및 로그 디스크로 미리 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-160">The SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="1e000-161">VM에 데이터 디스크가 포함되지 않은 상태에서 VM 설정 프로세스 중에 새 가상 하드 디스크를 추가한 경우 다음과 같이 기본 폴더를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-161">If your VM did not include a Data Disk and you added new virtual hard disks during the VM setup process, change the default folders as follows:</span></span>
   
   * <span data-ttu-id="1e000-162">왼쪽 패널에서 SQL Server 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-162">Right-click the SQL Server name in the left panel and click **Properties**.</span></span>
     
       ![SQL Server 속성][14]
   * <span data-ttu-id="1e000-164">왼쪽의 **페이지 선택** 목록에서 **데이터베이스 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-164">Select **Database Settings** from the **Select a page** list to the left.</span></span>
   * <span data-ttu-id="1e000-165">**데이터베이스 기본 위치**가 선택한 **데이터 디스크** 위치인지 확인하고 아닌 경우 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-165">Verify and/or change the **Database default locations** to the **Data Disk** locations of your choice.</span></span> <span data-ttu-id="1e000-166">기본 위치 설정을 사용하여 만든 새 데이터베이스는 여기에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-166">This is where new databases reside if created with the default location settings.</span></span>
     
       ![SQL 데이터베이스 기본값][15]  
5. <span data-ttu-id="1e000-168">새 데이터베이스 및 파일 그룹 집합을 만들어 분할된 테이블을 유지하려면 **create\_db\_default.sql** 샘플 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-168">To create a new database and a set of filegroups to hold the partitioned tables, open the sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="1e000-169">이 스크립트는 **TaxiNYC** 라는 새 데이터베이스를 만들고 기본 데이터 위치에 12개의 파일 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-169">The script will create a new database named **TaxiNYC** and 12 filegroups in the default data location.</span></span> <span data-ttu-id="1e000-170">각 파일 그룹에는 한 달 분량의 trip\_data 및 trip\_fare 데이터가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="1e000-171">필요한 경우 데이터베이스 이름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-171">Modify the database name, if desired.</span></span> <span data-ttu-id="1e000-172">**!실행** 을 클릭하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-172">Click **!Execute** to run the script.</span></span>
6. <span data-ttu-id="1e000-173">이제 trip\_data와 trip\_fare에 대해 각각 하나씩 두 개의 파티션 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-173">Next, create two partition tables, one for the trip\_data and another for the trip\_fare.</span></span> <span data-ttu-id="1e000-174">다음 작업을 수행하는 **create\_partitioned\_table.sql** 샘플 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-174">Open the sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="1e000-175">데이터를 월별로 분할하는 파티션 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-175">Create a partition function to split the data by month.</span></span>
   * <span data-ttu-id="1e000-176">각 월의 데이터를 다른 파일 그룹에 매핑하는 파티션 구성표를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-176">Create a partition scheme to map each month's data to a different filegroup.</span></span>
   * <span data-ttu-id="1e000-177">파티션 구성표에 매핑된 분할된 테이블 두 개를 만듭니다. **nyctaxi\_trip**은 trip\_data 보유하고 **nyctaxi\_fare**는 trip\_fare 데이터를 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-177">Create two partitioned tables mapped to the partition scheme: **nyctaxi\_trip** will hold the trip\_data and **nyctaxi\_fare** will hold the trip\_fare data.</span></span>
     
     <span data-ttu-id="1e000-178">**!실행** 을 클릭하여 스크립트를 실행하고 분할된 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-178">Click **!Execute** to run the script and create the partitioned tables.</span></span>
7. <span data-ttu-id="1e000-179">**Sample Scripts** 폴더에는 대량의 데이터를 SQL Server 테이블로 병렬로 가져오는 방법을 보여 주는 두 개의 샘플 PowerShell 스크립트가 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-179">In the **Sample Scripts** folder, there are two sample PowerShell scripts provided to demonstrate parallel bulk imports of data to SQL Server tables.</span></span>
   
   * <span data-ttu-id="1e000-180">**bcp\_parallel\_generic.ps1**은 대량의 데이터를 테이블로 병렬로 가져오는 일반 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-180">**bcp\_parallel\_generic.ps1** is a generic script to parallel bulk import data into a table.</span></span> <span data-ttu-id="1e000-181">이 스크립트를 수정하여 스크립트의 명령줄에 표시된 대로 입력 및 대상 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-181">Modify this script to set the input and target variables as indicated in the comment lines in the script.</span></span>
   * <span data-ttu-id="1e000-182">**bcp\_parallel\_nyctaxi.ps1**은 미리 구성된 버전의 일반 스크립트로서, NYC Taxi Trips 데이터의 두 테이블을 모두 로드하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of the generic script and can be used to to load both tables for the NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="1e000-183">**bcp\_parallel\_nyctaxi.ps1** 스크립트 이름을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭하여 PowerShell에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-183">Right-click the **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** to open it in PowerShell.</span></span> <span data-ttu-id="1e000-184">사전 설정 변수를 검토하고 선택한 데이터베이스 이름, 입력 데이터 폴더, 대상 로그 폴더 및 샘플 형식파일 **nyctaxi_trip.xml** 및 **nyctaxi\_fare.xml**(**Sample Scripts** 폴더에 제공)의 경로에 따라 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-184">Review the preset variables and modify according to your selected database name, input data folder, target log folder, and paths to the  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in the **Sample Scripts** folder).</span></span>
   
    ![대용량 데이터 가져오기][16]
   
    <span data-ttu-id="1e000-186">인증 모드를 선택할 수도 있습니다. 기본값은 Windows 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-186">You may also select the authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="1e000-187">도구 모음에서 녹색 화살표를 클릭하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-187">Click the green arrow in the toolbar to run.</span></span> <span data-ttu-id="1e000-188">스크립트는 분할된 테이블에 대해 12개씩 24개의 대량 가져오기 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-188">The script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="1e000-189">위에 설정된 대로 SQL Server 기본 데이터 폴더를 열어 데이터 가져오기 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-189">You may monitor the data import progress by opening the SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="1e000-190">PowerShell 스크립트는 시작 및 종료 시간을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-190">The PowerShell script reports the starting and ending times.</span></span> <span data-ttu-id="1e000-191">모든 대량 가져오기가 완료되면 종료 시간이 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-191">When all bulk imports complete, the ending time is reported.</span></span> <span data-ttu-id="1e000-192">대상 로그 폴더를 확인하여 대량 가져오기에 성공했는지, 즉 대상 로그 폴더에 보고된 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-192">Check the target log folder to verify that the bulk imports were successful, i.e., no errors reported in the target log folder.</span></span>
10. <span data-ttu-id="1e000-193">이제 데이터베이스에서 탐색, 기능 엔지니어링 및 필요에 따라 다른 작업을 수행할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="1e000-194">테이블은 **pickup\_datetime** 필드에 따라 분할되어 있으므로 **WHERE** 절에 **pickup\_datetime** 조건이 포함된 쿼리에서 파티션 구성테이블을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-194">Since the tables are partitioned according to the **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in the **WHERE** clause will benefit from the partition scheme.</span></span>
11. <span data-ttu-id="1e000-195">**SQL Server Management Studio**에서 제공된 샘플 스크립트인 **sample\_queries.sql**을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-195">In **SQL Server Management Studio**, explore the provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="1e000-196">샘플 쿼리를 실행하려면 쿼리 줄을 강조 표시한 다음 도구 모음에서 **!실행** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-196">To run any of the sample queries, highlight the query lines then click **!Execute** in the toolbar.</span></span>
12. <span data-ttu-id="1e000-197">NYC Taxi Trips 데이터가 별도 두 테이블에 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-197">The NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="1e000-198">조인 작업을 향상시키려면 테이블을 인덱싱하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-198">To improve join operations, it is highly recommended to index the tables.</span></span> <span data-ttu-id="1e000-199">샘플 스크립트 **create\_partitioned\_index.sql**은 복합 조인 키 **medallion, hack\_license 및 pickup\_datetime**에 대한 분할된 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-199">The sample script **create\_partitioned\_index.sql** creates partitioned indexes on the composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="1e000-200"><a name="dbexplore"></a>SQL Server에서 데이터 탐색 및 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="1e000-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="1e000-201">이 섹션에서는 이전에 만든 SQL Server 데이터베이스를 사용하여 **SQL Server Management Studio**에서 직접 SQL 쿼리를 실행해 데이터 탐색 및 기능 생성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in the **SQL Server Management Studio** using the SQL Server database created earlier.</span></span> <span data-ttu-id="1e000-202">**sample\_queries.sql**이라는 샘플 스크립트는 **Sample Scripts** 폴더에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-202">A sample script named **sample\_queries.sql** is provided in the **Sample Scripts** folder.</span></span> <span data-ttu-id="1e000-203">기본값과 다른 경우 스크립트를 수정하여 데이터베이스 이름을 변경합니다. **TaxiNYC**</span><span class="sxs-lookup"><span data-stu-id="1e000-203">Modify the script to change the database name, if it is different from the default: **TaxiNYC**.</span></span>

<span data-ttu-id="1e000-204">이 연습에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-204">In this exercise, we will:</span></span>

* <span data-ttu-id="1e000-205">Windows 인증 또는 SQL 인증과 SQL 로그인 이름 및 암호를 사용하여 **SQL Server Management Studio** 에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-205">Connect to **SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and the SQL login name and password.</span></span>
* <span data-ttu-id="1e000-206">다양한 기간에 걸쳐 몇몇 필드의 데이터 분포를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="1e000-207">경도 및 위도 필드의 데이터 품질을 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="1e000-208">**tip\_amount**에 따라 이진 및 다중 클래스 분류 레이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="1e000-209">기능을 생성하고 여정 거리를 계산/비교합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="1e000-210">두 테이블을 조인하고 모델을 빌드하는 데 사용할 무작위 샘플을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

<span data-ttu-id="1e000-211">Azure 기계 학습을 진행할 준비가 되었으면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-211">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="1e000-212">데이터를 추출 및 샘플링할 최종 SQL 쿼리를 저장하고 Azure 기계 학습의 [데이터 가져오기][import-data] 모듈에 쿼리를 직접 복사하여 붙여 넣습니다. 또는</span><span class="sxs-lookup"><span data-stu-id="1e000-212">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="1e000-213">모델을 빌드하는 데 사용할 샘플링 및 엔지니어링된 데이터를 새 데이터베이스 테이블에 유지하고 Azure 기계 학습의 [데이터 가져오기][import-data] 모듈에서 새 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-213">Persist the sampled and engineered data you plan to use for model building in a new database table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="1e000-214">이 섹션에서는 데이터를 추출 및 샘플링할 최종 SQL 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-214">In this section we will save the final query to extract and sample the data.</span></span> <span data-ttu-id="1e000-215">두 번째 방법은 [IPython Notebook에서 데이터 탐색 및 기능 엔지니어](#ipnb) 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-215">The second method is demonstrated in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="1e000-216">이전에 병렬 대량 가져오기를 사용하여 채운 테이블에서 행 및 열 수를 신속하게 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-216">For a quick verification of the number of rows and columns in the tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="1e000-217">탐색: medallion별 여정 분포</span><span class="sxs-lookup"><span data-stu-id="1e000-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="1e000-218">이 예제에서는 지정된 기간 내의 여정이 100개가 넘는 medallion(택시 번호)을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-218">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="1e000-219">쿼리는 **pickup\_datetime** 파티션 구성표를 조건으로 하므로 분할된 테이블 액세스를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-219">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="1e000-220">전체 데이터 집합을 쿼리할 때도 분할된 테이블 및/또는 인덱스 검색을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-220">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="1e000-221">탐색: medallion 및 hack_license별 여정 분포</span><span class="sxs-lookup"><span data-stu-id="1e000-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="1e000-222">데이터 품질 평가: 경도 및/또는 위도가 잘못된 레코드 확인</span><span class="sxs-lookup"><span data-stu-id="1e000-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="1e000-223">이 예제에서는 경도 및/또는 위도 필드에 유효하지 않은 값(라디안이 -90도~90도에 속해야 함)이 포함되거나 (0, 0) 좌표가 있는지 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-223">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="1e000-224">탐색: 왕복 여정과 비왕복 여정 분포</span><span class="sxs-lookup"><span data-stu-id="1e000-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="1e000-225">이 예제에서는 지정된 기간 동안(또는 전체 연도를 포괄하는 경우 전체 데이터 집합에서) 왕복 여정 수와 비왕복 여정 수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-225">This example finds the number of trips that were tipped vs. not tipped in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="1e000-226">이 분포는 나중에 이진 분류 모델링에 사용할 이진 레이블 분포를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-226">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="1e000-227">탐색: 팁 클래스/범위 분포</span><span class="sxs-lookup"><span data-stu-id="1e000-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="1e000-228">이 예제에서는 지정된 기간 동안(또는 전체 연도를 포괄하는 경우 전체 데이터 집합에서) 팁 범위 분포를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-228">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="1e000-229">이는 나중에 다중 클래스 분류 모델링에 사용할 레이블 클래스의 분포입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-229">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="1e000-230">탐색: 여정 거리 계산 및 비교</span><span class="sxs-lookup"><span data-stu-id="1e000-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="1e000-231">이 예제에서는 승차 및 하차 경도/위도를 SQL 지리 지점으로 변환하고, SQL 지리 지점 차이를 사용하여 여정 거리를 계산한 다음, 비교를 위해 무작위 결과 샘플을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-231">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="1e000-232">앞서 설명한 데이터 품질 평가 쿼리를 사용하여 유효한 좌표로만 결과가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-232">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="1e000-233">SQL 쿼리의 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="1e000-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="1e000-234">레이블 생성 및 지리 변환 탐색 쿼리는 계산 부분을 제거하여 레이블/기능을 생성하는 데에도 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-234">The label generation and geography conversion exploration queries can also be used to generate labels/features by removing the counting part.</span></span> <span data-ttu-id="1e000-235">추가적인 기능 엔지니어링 SQL 예제는 [IPython Notebook에서 데이터 탐색 및 기능 엔지니어링](#ipnb) 섹션에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-235">Additional feature engineering SQL examples are provided in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="1e000-236">SQL Server 데이터베이스 인스턴스에서 직접 실행되는 SQL 쿼리를 사용하여 전체 데이터 집합 또는 전체 데이터 집합의 큰 하위 집합에서 기능 생성 쿼리를 실행하는 것이 보다 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-236">It is more efficient to run the feature generation queries on the full dataset or a large subset of it using SQL queries which run directly on the SQL Server database instance.</span></span> <span data-ttu-id="1e000-237">**SQL Server Management Studio**, IPython Notebook 또는 로컬이나 원격으로 데이터베이스에 액세스할 수 있는 모든 개발 도구/환경에서 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-237">The queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access the database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="1e000-238">모델 빌드를 위한 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="1e000-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="1e000-239">다음 쿼리는 **nyctaxi\_trip** 및 **nyctaxi\_fare** 테이블을 조인하고, 이진 분류 레이블 **tipped**와 다중 클래스 분류 레이블 **tip\_class**를 생성하며, 조인된 전체 데이터 집합에서 1% 무작위 샘플을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-239">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from the full joined dataset.</span></span> <span data-ttu-id="1e000-240">Azure의 SQL Server 데이터베이스 인스턴스에서 데이터를 직접 수집하기 위해 이 쿼리를 복사한 다음 [Azure 기계 학습 스튜디오](https://studio.azureml.net) [데이터 가져오기][import-data] 모듈에 직접 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-240">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL Server database instance in Azure.</span></span> <span data-ttu-id="1e000-241">잘못된 (0, 0) 좌표가 있는 레코드는 쿼리에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-241">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="1e000-242"><a name="ipnb"></a>IPython Notebook에서 데이터 탐색 및 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="1e000-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="1e000-243">이 섹션에서는 Python과 SQL 쿼리를 모두 사용하여 이전에 만든 SQL Server 데이터베이스에 대해 데이터 탐색 및 기능 생성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL Server database created earlier.</span></span> <span data-ttu-id="1e000-244">**machine-Learning-data-science-process-sql-story.ipynb**라는 샘플 IPython Notebook은 **Sample IPython Notebooks** 폴더에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in the **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="1e000-245">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)에서 이 Notebook을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="1e000-246">빅 데이터로 작업하는 권장 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-246">The recommended sequence when working with big data is the following:</span></span>

* <span data-ttu-id="1e000-247">소량의 데이터 샘플을 메모리 내 데이터 프레임으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-247">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="1e000-248">샘플링된 데이터를 사용하여 일부 시각화 및 탐색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-248">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="1e000-249">샘플링된 데이터를 사용하여 기능 엔지니어링을 실험합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-249">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="1e000-250">더 큰 데이터 탐색, 데이터 조작 및 기능 엔지니어링의 경우 Python을 사용하여 Azure VM의 SQL Server 데이터베이스에 대해 SQL 쿼리를 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-250">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL Server database in the Azure VM.</span></span>
* <span data-ttu-id="1e000-251">Azure 기계 학습 모델 빌드에 사용할 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-251">Decide the sample size to use for Azure Machine Learning model building.</span></span>

<span data-ttu-id="1e000-252">Azure 기계 학습을 진행할 준비가 되었으면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-252">When ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="1e000-253">데이터를 추출 및 샘플링할 최종 SQL 쿼리를 저장하고 Azure 기계 학습의 [데이터 가져오기][import-data] 모듈에 쿼리를 직접 복사하여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-253">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="1e000-254">이 방법은 [Azure 기계 학습에서 모델 빌드](#mlmodel) 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-254">This method is demonstrated in the [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="1e000-255">모델을 빌드하는 데 사용할 샘플링 및 엔지니어링된 데이터를 새 데이터베이스 테이블에 유지한 다음 [데이터 가져오기][import-data] 모듈에서 새 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-255">Persist the sampled and engineered data you plan to use for model building in a new database table, then use the new table in the [Import Data][import-data] module.</span></span>

<span data-ttu-id="1e000-256">다음은 데이터 탐색, 데이터 시각화 및 기능 엔지니어링에 대한 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-256">The following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="1e000-257">더 많은 예제는 **Sample IPython Notebooks** 폴더에 있는 샘플 SQL IPython Notebook을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-257">For more examples, see the sample SQL IPython notebook in the **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="1e000-258">데이터베이스 자격 증명 초기화</span><span class="sxs-lookup"><span data-stu-id="1e000-258">Initialize Database Credentials</span></span>
<span data-ttu-id="1e000-259">다음 변수에서 데이터베이스 연결 설정을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-259">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="1e000-260">데이터베이스 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="1e000-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="1e000-261">nyctaxi_trip 테이블의 행 및 열 수 보고</span><span class="sxs-lookup"><span data-stu-id="1e000-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="1e000-262">총 행 수 = 173179759</span><span class="sxs-lookup"><span data-stu-id="1e000-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="1e000-263">총 열 수 = 14</span><span class="sxs-lookup"><span data-stu-id="1e000-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-the-sql-server-database"></a><span data-ttu-id="1e000-264">SQL Server 데이터베이스에서 소량의 데이터 샘플 읽기</span><span class="sxs-lookup"><span data-stu-id="1e000-264">Read-in a small data sample from the SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="1e000-265">샘플 테이블을 읽은 시간 = 6.492000초</span><span class="sxs-lookup"><span data-stu-id="1e000-265">Time to read the sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="1e000-266">검색된 행 및 열 수 = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="1e000-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="1e000-267">기술 통계</span><span class="sxs-lookup"><span data-stu-id="1e000-267">Descriptive Statistics</span></span>
<span data-ttu-id="1e000-268">이제 샘플링된 데이터를 탐색할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-268">Now are ready to explore the sampled data.</span></span> <span data-ttu-id="1e000-269">**trip\_distance**(또는 다른 모든) 필드에 대한 기술 통계부터 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-269">We start with looking at descriptive statistics for the **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="1e000-270">시각화: 상자 그림 예제</span><span class="sxs-lookup"><span data-stu-id="1e000-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="1e000-271">다음으로, 여정 거리에 대한 상자 그림을 확인하여 사분위수를 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-271">Next we look at the box plot for the trip distance to visualize the quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![그릴 #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="1e000-273">시각화: 분포 그림 예제</span><span class="sxs-lookup"><span data-stu-id="1e000-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![그릴 #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="1e000-275">시각화: 가로 막대형 및 꺾은선형 차트</span><span class="sxs-lookup"><span data-stu-id="1e000-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="1e000-276">이 예에서는 여정 거리를 5개의 bin으로 범주화하고 범주화 결과를 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-276">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="1e000-277">위의 bin 분포를 아래와 같이 가로 막대형 또는 꺾은선형 차트로 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-277">We can plot the above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![그릴 #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![그릴 #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="1e000-280">시각화: 산점도 예제</span><span class="sxs-lookup"><span data-stu-id="1e000-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="1e000-281">**trip\_time\_in\_secs** 및 **trip\_distance** 사이의 산점도를 표시하여 상관관계가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![그릴 #6][6]

<span data-ttu-id="1e000-283">마찬가지로 **rate\_code** 및 **trip\_distance** 간의 관계를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-283">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![그릴 #8][8]

### <a name="sub-sampling-the-data-in-sql"></a><span data-ttu-id="1e000-285">SQL에서 데이터 하위 샘플링</span><span class="sxs-lookup"><span data-stu-id="1e000-285">Sub-Sampling the Data in SQL</span></span>
<span data-ttu-id="1e000-286">[Azure Machine Learning 스튜디오](https://studio.azureml.net)에서 모델을 빌드하기 위해 데이터를 준비할 때 **데이터 가져오기 모듈에서 직접 사용할 SQL 쿼리**를 결정하거나, 간단한 **SELECT * FROM <your\_new\_table\_name>**을 사용하여 [데이터 가져오기][import-data] 모듈에서 사용할 수 있는 엔지니어링 및 샘플링된 데이터를 새 테이블에 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on the **SQL query to use directly in the Import Data module** or persist the engineered and sampled data in a new table, which you could use in the [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="1e000-287">이 섹션에서는 샘플링 및 엔지니어링된 데이터를 유지할 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-287">In this section we will create a new table to hold the sampled and engineered data.</span></span> <span data-ttu-id="1e000-288">모델 빌드를 위한 직접 SQL 쿼리 예제는 SQL Server에서 [데이터 탐색 및 기능 엔지니어링 섹션](#dbexplore) 에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-288">An example of a direct SQL query for model building is provided in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-the-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="1e000-289">샘플 테이블을 만들고 조인된 테이블의 1%로 채우기(테이블이</span><span class="sxs-lookup"><span data-stu-id="1e000-289">Create a Sample Table and Populate with 1% of the Joined Tables.</span></span> <span data-ttu-id="1e000-290">있는 경우 먼저 해당 테이블 삭제)</span><span class="sxs-lookup"><span data-stu-id="1e000-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="1e000-291">이 섹션에서는 **nyctaxi\_trip** 및 **nyctaxi\_fare**를 조인하고, 1% 무작위 샘플을 추출하며, 이름이 **nyctaxi\_one\_percent**인 새 테이블에 샘플링된 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-291">In this section, we join the tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist the sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="1e000-292">IPython Notebook에서 SQL 쿼리를 사용하여 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="1e000-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="1e000-293">이 섹션에서는 위에서 만든 새 테이블에 유지되는 1%의 샘플링된 데이터를 사용하여 데이터 분포를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-293">In this section, we explore data distributions using the 1% sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="1e000-294">[SQL Server에서 데이터 탐색 및 기능 엔지니어링](#dbexplore) 섹션에 설명된 대로 선택적으로 **TABLESAMPLE**을 사용하여 탐색 샘플을 제한하거나, **pickup\_datetime** 파티션을 사용하여 결과를 지정된 기간으로 제한하여 원래 테이블로 유사한 탐색을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-294">Note that similar explorations can be performed using the original tables, optionally using **TABLESAMPLE** to limit the exploration sample or by limiting the results to a given time period using the **pickup\_datetime** partitions, as illustrated in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="1e000-295">탐색: 일일 여정 분포</span><span class="sxs-lookup"><span data-stu-id="1e000-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="1e000-296">탐색: medallion당 여정 분포</span><span class="sxs-lookup"><span data-stu-id="1e000-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="1e000-297">IPython Notebook에서 SQL 쿼리를 사용하여 기능 생성</span><span class="sxs-lookup"><span data-stu-id="1e000-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="1e000-298">이 섹션에서는 이전 섹션에서 만든 1% 샘플 테이블에서 작동하는 SQL 쿼리를 직접 사용하여 새 레이블 및 기능을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-298">In this section we will generate new labels and features directly using SQL queries, operating on the 1% sample table we created in the previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="1e000-299">레이블 생성: 클래스 레이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="1e000-300">다음 예제에서는 모델링에 사용할 두 개의 레이블 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-300">In the following example, we generate two sets of labels to use for modeling:</span></span>

1. <span data-ttu-id="1e000-301">이진 클래스 레이블 **tipped** (팁이 제공되는지 예측)</span><span class="sxs-lookup"><span data-stu-id="1e000-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="1e000-302">다중 클래스 레이블 **tip\_class**(팁 bin 또는 범위 예측)</span><span class="sxs-lookup"><span data-stu-id="1e000-302">Multiclass Labels **tip\_class** (predicting the tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="1e000-303">기능 엔지니어링: 범주 열에 대한 개수 기능</span><span class="sxs-lookup"><span data-stu-id="1e000-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="1e000-304">이 예제에서는 각 범주를 데이터에서 발생한 횟수로 바꿔 범주 필드를 숫자 필드로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-304">This example transforms a categorical field into a numeric field by replacing each category with the count of its occurrences in the data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="1e000-305">기능 엔지니어링: 숫자 열에 대한 Bin 기능</span><span class="sxs-lookup"><span data-stu-id="1e000-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="1e000-306">이 예제에서는 연속 숫자 필드를 사전 설정된 범주 범위로 변환합니다. 즉, 숫자 필드를 범주 필드로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="1e000-307">기능 엔지니어링: 10진수 위도/경도에서 위치 기능 추출</span><span class="sxs-lookup"><span data-stu-id="1e000-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="1e000-308">이 예제에서는 위도 및/또는 경도 필드의 10진수 표현을 세분성(예: 국가, 구/군/시, 동/면, 번지 등)이 서로 다른 지역 필드로 분류합니다. 새 지리 필드는 실제 위치에 매핑되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-308">This example breaks down the decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that the new geo-fields are not mapped to actual locations.</span></span> <span data-ttu-id="1e000-309">지오코드 위치 매핑에 대한 자세한 내용은 [Bing Maps REST 서비스](https://msdn.microsoft.com/library/ff701710.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="1e000-310">기능화한 테이블의 최종 양식 확인</span><span class="sxs-lookup"><span data-stu-id="1e000-310">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="1e000-311">이제 [Azure 기계 학습](https://studio.azureml.net)에서 모델 빌드 및 모델 배포를 진행할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-311">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="1e000-312">이전에 식별된 다음과 같은 예측 문제에 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-312">The data is ready for any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="1e000-313">이진 분류: 여정에 대해 팁이 지불되었는지 여부를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-313">Binary classification: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="1e000-314">다중 클래스 분류: 이전에 정의한 클래스에 따라 지불된 팁의 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-314">Multiclass classification: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="1e000-315">회귀 작업: 여정에 대해 지불된 팁의 금액을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-315">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="1e000-316"><a name="mlmodel"></a>Azure 기계 학습에서 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="1e000-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="1e000-317">모델링 연습을 시작하려면 Azure 기계 학습 작업 영역에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-317">To begin the modeling exercise, log in to your Azure Machine Learning workspace.</span></span> <span data-ttu-id="1e000-318">기계 학습 작업 영역을 아직 만들지 않은 경우 [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="1e000-319">Azure 기계 학습을 시작하려면 [Azure 기계 학습 스튜디오란?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="1e000-319">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="1e000-320">[Azure 기계 학습 스튜디오](https://studio.azureml.net)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-320">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="1e000-321">스튜디오 홈 페이지에서는 다양한 정보, 비디오, 자습서, 모듈 참조 링크 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-321">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="1e000-322">Azure 기계 학습에 대한 자세한 내용은 [Azure 기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-322">Fore more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="1e000-323">일반적인 학습 실험은 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-323">A typical training experiment consists of the following:</span></span>

1. <span data-ttu-id="1e000-324">**+새** 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="1e000-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="1e000-325">Azure 기계 학습으로 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-325">Get the data to Azure Machine Learning.</span></span>
3. <span data-ttu-id="1e000-326">필요에 따라 데이터를 전처리, 변환 및 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-326">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="1e000-327">필요에 따라 기능을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-327">Generate features as needed.</span></span>
5. <span data-ttu-id="1e000-328">데이터를 학습/유효성 검사/테스트 데이터 집합으로 분할하거나, 각각에 대한 별도의 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-328">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="1e000-329">해결할 학습 문제에 따라 하나 이상의 기계 학습 알고리즘(예:</span><span class="sxs-lookup"><span data-stu-id="1e000-329">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="1e000-330">이진 분류, 다중 클래스 분류, 회귀)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="1e000-331">학습 데이터 집합을 사용하여 하나 이상의 모델을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-331">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="1e000-332">학습된 모델을 사용하여 유효성 검사 데이터 집합의 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-332">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="1e000-333">모델을 평가하여 학습 문제에 대한 관련 메트릭을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-333">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="1e000-334">모델을 미세 조정하고 배포할 가장 적합한 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-334">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="1e000-335">이 연습에서는 이미 SQL Server에서 데이터를 탐색 및 엔지니어링하고 Azure 기계 학습에서 수집할 샘플 크기를 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-335">In this exercise, we have already explored and engineered the data in SQL Server, and decided on the sample size to ingest in Azure Machine Learning.</span></span> <span data-ttu-id="1e000-336">결정한 예측 모델 중 하나 이상을 빌드하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-336">To build one or more of the prediction models we decided:</span></span>

1. <span data-ttu-id="1e000-337">**데이터 입력 및 출력** 섹션에서 제공되는 [데이터 가져오기][import-data] 모듈을 사용하여 Azure 기계 학습으로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-337">Get the data to Azure Machine Learning using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="1e000-338">자세한 내용은 [데이터 가져오기][import-data] 참조 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-338">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Azure 기계 학습 데이터 가져오기][17]
2. <span data-ttu-id="1e000-340">**속성** 패널에서 **Azure SQL Database**를 **데이터 원본**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-340">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="1e000-341">**데이터베이스 서버 이름** 필드에 데이터베이스 DNS 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-341">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="1e000-342">형식: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="1e000-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="1e000-343">**데이터베이스 이름** 을 해당 필드에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-343">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="1e000-344">**서버 사용자 계정 이름에 **SQL 사용자 이름**을 입력하고 **서버 사용자 계정 암호**에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-344">Enter the **SQL user name** in the **Server user aqccount name, and the password in the **Server user account password**.</span></span>
6. <span data-ttu-id="1e000-345">**모든 서버 인증서 허용** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="1e000-346">**데이터베이스 쿼리** 편집 텍스트 영역에서 필요한 데이터베이스 필드를 추출하는 쿼리(레이블과 같은 모든 계산된 필드 포함)를 붙여 넣고 데이터를 원하는 샘플 크기로 다운 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-346">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="1e000-347">SQL Server 데이터베이스에서 직접 데이터를 읽는 이진 분류 실험 예제는 아래 그림에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-347">An example of a binary classification experiment reading data directly from the SQL Server database is in the figure below.</span></span> <span data-ttu-id="1e000-348">다중 클래스 분류 및 회귀 문제에 대한 유사한 실험을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure 기계 학습][10]

> [!IMPORTANT]
> <span data-ttu-id="1e000-350">이전 섹션에 제공된 모델링 데이터 추출 및 샘플링 쿼리 예제에서는 **세 가지 모델링 연습에 대한 모든 레이블이 쿼리에 포함되어 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="1e000-350">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="1e000-351">각 모델링 연습의 중요한(필수) 단계는 다른 두 문제에 대한 필요 없는 레이블 및 다른 모든 **목표 누설**을 **제외**하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-351">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="1e000-352">예를 들어, 이진 분류를 사용할 때는 레이블 **tipped**를 사용하고, **tip\_class**, **tip\_amount** 및 **total\_amount** 필드를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-352">For e.g., when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="1e000-353">이러한 필드는 지불된 팁을 의미하므로 목표 누설입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-353">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="1e000-354">필요 없는 열 또는 목표 누설을 제외하려면 [데이터 집합의 열 선택][select-columns] 모듈 또는 [메타데이터 편집][edit-metadata]을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-354">To exclude unnecessary columns and/or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="1e000-355">자세한 내용은 [데이터 집합의 열 선택][select-columns] 및 [메타데이터 편집][edit-metadata] 참조 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="1e000-356"><a name="mldeploy"></a>Azure 기계 학습에서 모델 배포</span><span class="sxs-lookup"><span data-stu-id="1e000-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="1e000-357">모델이 준비된 경우 실험에서 직접 웹 서비스로 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-357">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="1e000-358">Azure 기계 학습 웹 서비스 배포에 대한 자세한 내용은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="1e000-359">새 웹 서비스를 배포하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-359">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="1e000-360">점수 매기기 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="1e000-361">웹 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-361">Deploy the web service.</span></span>

<span data-ttu-id="1e000-362">**완료된** 학습 실험에서 점수 매기기 실험을 만들려면 아래쪽 작업 모음에서 **점수 매기기 실험 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-362">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Azure 점수 매기기][18]

<span data-ttu-id="1e000-364">Azure 기계 학습에서는 학습 실험의 구성 요소를 기반으로 점수 매기기 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-364">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="1e000-365">특히 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-365">In particular, it will:</span></span>

1. <span data-ttu-id="1e000-366">학습된 모델을 저장하고 모델 학습 모듈을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-366">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="1e000-367">필요한 입력 데이터 스키마를 나타내는 논리적 **입력 포트** 를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-367">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="1e000-368">필요한 웹 서비스 출력 스키마를 나타내는 논리적 **출력 포트** 를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-368">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="1e000-369">점수 매기기 실험을 만들 때 필요에 따라 검토하고 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-369">When the scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="1e000-370">일반적인 조정은 입력 데이터 집합 및/또는 쿼리를 레이블 필드를 제외한 것으로 바꾸는 것입니다. 레이블 필드는 서비스를 호출할 때 사용할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-370">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="1e000-371">또한 입력 데이터 집합 및/또는 쿼리 크기를 입력 스키마를 나타내는 데 충분한 정도의 몇몇 레코드로 줄이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-371">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="1e000-372">출력 포트의 경우 일반적으로 [데이터 집합의 열 선택][select-columns] 모듈을 사용하여 모든 입력 필드를 제외하고 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률**만 출력에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-372">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="1e000-373">샘플 점수 매기기 실험은 아래 그림에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-373">A sample scoring experiment is in the figure below.</span></span> <span data-ttu-id="1e000-374">배포할 준비가 되면 아래쪽 작업 모음에서 **웹 서비스 게시** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-374">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Azure 기계 학습 게시][11]

<span data-ttu-id="1e000-376">이 연습 자습서에서는 Azure 데이터 과학 환경을 만들고, 대용량 공용 데이터 집합으로 데이터 취득에서 모델 학습 및 Azure 기계 학습 웹 서비스 배포에 이르는 모든 과정을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-376">To recap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all the way from data acquisition to model training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="1e000-377">라이선스 정보</span><span class="sxs-lookup"><span data-stu-id="1e000-377">License Information</span></span>
<span data-ttu-id="1e000-378">이 샘플 연습 및 이와 함께 제공되는 스크립트와 IPython Notebook은 MIT 라이선스에 따라 Microsoft에서 공유한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e000-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="1e000-379">자세한 내용은 GitHub의 샘플 코드 디렉터리에 있는 LICENSE.txt 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e000-379">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="1e000-380">참조</span><span class="sxs-lookup"><span data-stu-id="1e000-380">References</span></span>
<span data-ttu-id="1e000-381">• [Andrés Monroy NYC Taxi Trips 다운로드 페이지](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="1e000-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="1e000-382">• [Chris Whong의 FOILing NYC Taxi Trip 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="1e000-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="1e000-383">• [NYC Taxi 및 Limousine 수수료 연구 및 통계](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="1e000-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
