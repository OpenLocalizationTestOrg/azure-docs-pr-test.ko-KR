---
title: "aaaBuild Azure VM에서 SQL Server를 사용 하 여 기계 학습 모델을 배포 하 고 | Microsoft Docs"
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
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="98969-103">작업에 팀 데이터 과학 프로세스 hello: SQL Server를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98969-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="98969-104">Hello 만들고 기계 학습 모델을 배포 하는 과정을 단계별로 안내이 자습서에서는 사용 하 여 SQL Server 및 공개적으로 사용할 수 있는 데이터 집합-hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="98969-105">hello 프로시저 표준 데이터 과학 워크플로 따릅니다: 수집 하 고 hello 데이터 탐색, 엔지니어링 기능 toofacilitate 학습 한 다음 빌드 및 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="98969-106"><a name="dataset"></a>NYC Taxi Trips 데이터 집합 설명</span><span class="sxs-lookup"><span data-stu-id="98969-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="98969-107">hello NYC 택시 여행 데이터는 약 20GB의 압축 된 CSV 파일 (~ 48 GB 압축 되지 않음), 구성 173 백만 개 이상의 개별 라운드트립 및 hello fares 각 시에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="98969-108">각 여행 레코드 hello 픽업 및 자동 전송 위치 및 시간, 익명화 된 해킹 (드라이버의) 라이선스 번호 및 메달 (택시의 고유 id) 번호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="98969-109">hello 데이터 hello 2013 년의 모든 왕복에 설명 하 고 각 월에 대 한 두 개의 데이터 집합을 따라 hello에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="98969-110">hello 'trip_data' CSV 승객, 픽업 및 dropoff 포인트, 여행 기간 및 여행 길이 수와 같이 여행 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="98969-111">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="98969-112">hello 'trip_fare' CSV hello 요금을 지불 유형, 요금 크기, 추가 요금 및 세금, 팁 및 통행료가, 및 유료 hello 총 금액 등 각 여정에 대해 지불한의 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="98969-113">다음은 몇 가지 샘플 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="98969-114">hello 고유 키 toojoin 여행\_데이터와 여행\_요금 가지 hello 필드로 구성 됩니다: 메달 해킹\_사용권 및 픽업\_날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="98969-115"><a name="mltasks"></a>예측 작업의 예제</span><span class="sxs-lookup"><span data-stu-id="98969-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="98969-116">우리는 hello에 따라 3 개의 예측 문제 작성 *팁\_양*, 즉:</span><span class="sxs-lookup"><span data-stu-id="98969-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="98969-117">이진 분류: 여정에 대해 팁이 지불되었는지 여부를 예측합니다. 즉, *tip\_amount*가 $0보다 크면 지불된 것이고 *tip\_amount*가 $0이면 지불되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="98969-118">다중 클래스 분류: toopredict hello 범위 끝의 hello 여행에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="98969-119">Hello 나눕니다 *팁\_양* 다섯 개의 bin 또는 클래스에:</span><span class="sxs-lookup"><span data-stu-id="98969-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="98969-120">회귀 작업: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="98969-121"><a name="setup"></a>설정 hello Azure 데이터 과학 환경에 대 한 고급 분석</span><span class="sxs-lookup"><span data-stu-id="98969-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="98969-122">Hello에서 볼 수 있듯이 [환경 계획](machine-learning-data-science-plan-your-environment.md) 가이드는 Azure의 hello NYC 택시 Trips 데이터 집합이 들어 있는 몇 가지 옵션 toowork:</span><span class="sxs-lookup"><span data-stu-id="98969-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="98969-123">Azure blob에 hello 데이터 다음 Azure 기계 학습에서 모델 사용</span><span class="sxs-lookup"><span data-stu-id="98969-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="98969-124">Hello 데이터를 SQL Server 데이터베이스 다음 Azure 기계 학습에서 모델 로드</span><span class="sxs-lookup"><span data-stu-id="98969-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="98969-125">이 자습서에서는 SQL Server, 데이터 탐색, 기능 hello 데이터 tooa의 병렬 대량 가져오기를 보여 드리겠습니다 엔지니어링 및 SQL Server Management Studio를 사용 하 여 샘플링 아래쪽으로 IPython 노트북을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="98969-126">[샘플 스크립트](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) 및 [IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)은 GitHub에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="98969-127">Azure blob에 대 한 hello 데이터로 샘플 IPython 노트북 toowork hello 제공 됩니다. 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="98969-128">Azure 데이터 과학 환 결 tooset:</span><span class="sxs-lookup"><span data-stu-id="98969-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="98969-129">저장소 계정을 만드는</span><span class="sxs-lookup"><span data-stu-id="98969-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="98969-130">Azure 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="98969-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="98969-131">[데이터 과학 가상 컴퓨터 프로비전](machine-learning-data-science-setup-sql-server-virtual-machine.md)(SQL Server 및 IPython Notebook 서버 제공)</span><span class="sxs-lookup"><span data-stu-id="98969-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98969-132">hello 예제 스크립트 및 IPython 노트북이 다운로드 한 tooyour 데이터 과학 가상 컴퓨터 hello 설치 프로세스 중 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="98969-133">Hello VM 설치 후 스크립트에는 다음이 완료 되 면 hello 샘플 VM의 문서 라이브러리에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="98969-134">샘플 스크립트: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="98969-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="98969-135">샘플 IPython Notebook: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="98969-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="98969-136">where `<user_name>` 은(는) VM의 Windows 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="98969-137">Toohello 예제 폴더를 언급할 **예제 스크립트** 및 **샘플 IPython 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="98969-138">Hello 데이터 집합의 크기, 데이터 원본 위치 및 hello 선택한 Azure 대상 환경에 따라,이 시나리오는 비슷한 너무[시나리오 \#5: 로컬 파일에 큰 데이터 집합에는 Azure VM의 SQL Server 대상](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb)합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="98969-139"><a name="getdata"></a>공개 소스에서 hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="98969-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="98969-140">tooget hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 공용 위치에서 데이터 집합을 사용할 수 있습니다에 설명 된 hello 메서드의 [Azure Blob 저장소에서 데이터 이동 tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello 데이터 tooyour 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="98969-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="98969-141">AzCopy를 사용 하 여 toocopy hello 데이터:</span><span class="sxs-lookup"><span data-stu-id="98969-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="98969-142">Tooyour 가상 컴퓨터 (VM)에 로그인</span><span class="sxs-lookup"><span data-stu-id="98969-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="98969-143">Hello VM 데이터 디스크에 새 디렉터리를 만듭니다 (참고: hello 데이터 디스크로 VM hello와 함께 제공 되는 임시 디스크를 사용 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="98969-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="98969-144">명령 프롬프트 창에서 다음 Azcopy 명령 줄, (2)에서 만든 데이터 폴더와 < path_to_data_folder > 대체 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="98969-145">총 24 CSV 파일을 압축 hello AzCopy 완료 되 면 (여행에 대 한 12\_데이터와 여행에 대 한 12\_요금) hello 데이터 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="98969-146">Hello 다운로드 한 파일을 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="98969-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="98969-147">참고 hello 폴더 hello 압축 되지 않은 파일이 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="98969-148">이 폴더에는 참조 된 tooas hello 됩니다 < 경로\_를\_데이터\_파일\>합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="98969-149"><a name="dbload"></a>SQL Server 데이터베이스로 대량 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="98969-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="98969-150">hello 로드/전송 많은 양의 데이터 tooan SQL 데이터베이스 및 후속 쿼리 성능이 향상 될 수 있습니다를 사용 하 여 *분할 테이블 및 뷰*합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="98969-151">이 섹션에 설명 된 hello 지침을 따릅니다 [병렬 대량 데이터 가져오기를 사용 하 여 SQL 파티션 테이블](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate를 동시에 분할 된 테이블에 새 데이터베이스 및 부하 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="98969-152">Tooyour VM에에서 로그인 한 상태, 시작 **SQL Server Management Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="98969-153">Windows 인증을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="98969-153">Connect using Windows Authentication.</span></span>
   
    ![SSMS 연결][12]
3. <span data-ttu-id="98969-155">Hello SQL Server 인증 모드를 변경 하지 않은 있고 새 SQL 로그인 사용자를 만든 경우 hello 스크립트 파일을 열고 **변경\_auth.sql** hello에 **예제 스크립트** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="98969-156">Hello 기본 사용자 이름과 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-156">Change hello  default user name and password.</span></span> <span data-ttu-id="98969-157">클릭 **! 실행** hello 도구 모음 toorun hello 스크립트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![스크립트 실행][13]
4. <span data-ttu-id="98969-159">확인 및/또는 변경 hello SQL Server를 새로 만든 데이터베이스는 기본 데이터베이스 및 로그 폴더 tooensure 데이터 디스크에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="98969-160">데이터 웨어하우징 로드에 대해 최적화 된 hello SQL Server VM 이미지는 데이터 및 로그 디스크가으로 미리 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="98969-161">VM 데이터 디스크를 포함 하지 않은 hello VM 설치 프로세스 중 새 가상 하드 디스크를 추가 하는 경우 다음과 같이 hello 기본 폴더를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="98969-162">왼쪽 패널 및 클릭 hello에 hello SQL 서버 이름 마우스 오른쪽 단추로 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![SQL Server 속성][14]
   * <span data-ttu-id="98969-164">선택 **데이터베이스 설정** hello에서 **페이지 선택** toohello 왼쪽을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="98969-165">확인 및/또는 hello 변경 **데이터베이스 기본 위치** toohello **데이터 디스크** 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="98969-166">기본 위치 설정을 hello 사용 하 여 만든 경우 새 데이터베이스가 상주 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![SQL 데이터베이스 기본값][15]  
5. <span data-ttu-id="98969-168">toocreate hello 분할 된 테이블, hello 샘플 스크립트를 열거나 새 데이터베이스 및 파일 그룹 toohold 집합이 **만들\_db\_default.sql**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="98969-169">hello 스크립트 라는 새 데이터베이스를 만드는 **TaxiNYC** 및 hello 기본 데이터 위치에 12 파일 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="98969-170">각 파일 그룹에는 한 달 분량의 trip\_data 및 trip\_fare 데이터가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="98969-171">필요한 경우 hello 데이터베이스 이름을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="98969-172">클릭 **! 실행** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="98969-173">다음으로 hello 여정에 대해 하나씩 두 파티션 테이블을 만들고\_데이터와 hello 여정에 대해 다른\_요금입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="98969-174">Hello 샘플 스크립트를 열거나 **만들\_분할\_table.sql**, 것은:</span><span class="sxs-lookup"><span data-stu-id="98969-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="98969-175">월별 파티션 함수 toosplit hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98969-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="98969-176">파티션 구성표 toomap 각 달의 데이터 tooa 다른 파일 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98969-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="98969-177">두 개의 분할 된 테이블의 매핑된 toohello 파티션 구성표 만들기: **nyctaxi\_여행** hello 여행이 포함 될\_데이터 및 **nyctaxi\_요금** hello 여행 보유 \_있어 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="98969-178">클릭 **! 실행** toorun 스크립트 hello 및 hello 분할 된 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98969-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="98969-179">Hello에 **예제 스크립트** 폴더를 두 개의 샘플 PowerShell 스크립트 데이터 tooSQL 서버 테이블의 병렬 대량 가져오기를 toodemonstrate 제공 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="98969-180">**bcp\_병렬\_generic.ps1** 은 일반 스크립트 tooparallel 대량 가져오기 데이터를 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="98969-181">Hello 스크립트에 hello 주석 줄에 표시 된 대로이 스크립트 tooset hello 입력 및 대상 변수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="98969-182">**bcp\_병렬\_nyctaxi.ps1** 미리 구성 된 버전의 hello 일반 스크립트 및 사용 되는 tootooload hello NYC 택시와 데이터에 대 한 두 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="98969-183">마우스 오른쪽 단추로 클릭 hello **bcp\_병렬\_nyctaxi.ps1** 스크립트 이름 및 클릭 **편집** tooopen PowerShell에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="98969-184">검토 hello 변수 기본 설정 및 따라 tooyour 선택한 데이터베이스 이름, 입력된 데이터 폴더, 대상 로그 폴더 및 경로 toohello 예제 서식 파일 수정 **nyctaxi_trip.xml** 및 **nyctaxi\_ fare.xml** (hello에 제공 된 **예제 스크립트** 폴더).</span><span class="sxs-lookup"><span data-stu-id="98969-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![대용량 데이터 가져오기][16]
   
    <span data-ttu-id="98969-186">Hello 인증 모드를 선택할 수 있습니다, 그리고 기본값은 Windows 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="98969-187">도구 모음 toorun hello에에서 hello 녹색 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="98969-188">hello 스크립트는 각 분할 된 테이블에 대 한 병렬, 12에서 24 대량 가져오기 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="98969-189">위의 세트로 hello SQL Server 기본 데이터 폴더를 열어 hello 데이터 가져오기 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="98969-190">hello PowerShell 스크립트 보고서에는 시작 및 종료 시간 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="98969-191">모든 대량 가져오기 완료, 종료 시간 hello 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="98969-192">Hello 대상 로그 폴더에 보고 된 오류 없이 hello 대상 로그 폴더 tooverify hello 대량 가져오기 성공 했음을, 즉, 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="98969-193">이제 데이터베이스에서 탐색, 기능 엔지니어링 및 필요에 따라 다른 작업을 수행할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="98969-194">Hello 테이블이 toohello에 따라 분할 되는 이후 **픽업\_datetime** 필드를 포함 하는 쿼리 **픽업\_datetime** hello에 대 한 조건  **여기서** 절 hello 파티션 구성표에서 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="98969-195">**SQL Server Management Studio**, 제공 된 hello 샘플 스크립트를 탐색 **샘플\_queries.sql**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="98969-196">hello 샘플 쿼리를 강조 표시 hello 줄을 쿼리 한 다음 클릭 toorun **! 실행** hello 도구 모음에서입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="98969-197">hello NYC 택시와 데이터는 두 개의 별도 테이블에 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="98969-198">tooimprove 조인 작업 좋습니다 tooindex hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="98969-199">샘플 스크립트 hello **만들\_분할\_index.sql** hello 복합 조인 키에서 분할 된 인덱스를 만듭니다. **메달 해킹\_라이선스 및 픽업\_datetime**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="98969-200"><a name="dbexplore"></a>SQL Server에서 데이터 탐색 및 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="98969-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="98969-201">이 섹션에서는 hello에서 직접 SQL 쿼리를 실행 하 여 데이터 탐색 및 기능 생성을 수행 합니다 **SQL Server Management Studio** 앞에서 만든 hello SQL Server 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="98969-202">라는 샘플 스크립트 **샘플\_queries.sql** hello에 제공 된 **예제 스크립트** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="98969-203">Hello 기본값과에서 다른 경우 hello 스크립트 toochange hello 데이터베이스 이름, 수정: **TaxiNYC**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="98969-204">이 연습에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-204">In this exercise, we will:</span></span>

* <span data-ttu-id="98969-205">너무 연결**SQL Server Management Studio** Windows 인증을 사용 하거나 SQL 인증 및 hello SQL 로그인 이름 및 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="98969-206">다양한 기간에 걸쳐 몇몇 필드의 데이터 분포를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="98969-207">Hello 경도 및 위도 필드의 데이터 품질을 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="98969-208">이진 및 다중 클래스 분류 레이블을 hello에 따라 생성 **팁\_양**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="98969-209">기능을 생성하고 여정 거리를 계산/비교합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="98969-210">Hello 두 테이블을 조인 하 고 사용 하는 toobuild 모델 될 무작위 샘플링을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="98969-211">준비 tooproceed tooAzure 기계 학습을 있습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="98969-212">Hello 최종 SQL 쿼리 tooextract 및 샘플 hello 데이터 및 복사-붙여넣기 hello에 직접 쿼리를 저장 한 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈 또는</span><span class="sxs-lookup"><span data-stu-id="98969-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="98969-213">샘플링 hello 유지 및 엔지니어링된 데이터 toouse 새 데이터베이스에 작성 하는 모델에 대 한 계획 테이블 고 hello 새 테이블을 사용 하 여 hello에 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="98969-214">이 섹션의 hello 마지막 쿼리 tooextract 및 예제 hello 데이터 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="98969-215">두 번째 방법은 hello hello에 설명 된 [데이터 탐색 및 IPython 전자 필기장의 기능 엔지니어링](#ipnb) 섹션.</span><span class="sxs-lookup"><span data-stu-id="98969-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="98969-216">Hello hello의 행과 열 수의 빠른 확인 하기 위해 테이블 이전 병렬 대량 가져오기를 사용 하 여 입력</span><span class="sxs-lookup"><span data-stu-id="98969-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="98969-217">탐색: medallion별 여정 분포</span><span class="sxs-lookup"><span data-stu-id="98969-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="98969-218">이 예에서는 지정 된 기간 내에서 100 개 이상의 트립을 있는 hello 메달 (택시 번호)를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="98969-219">hello 쿼리는 것이 유리한 hello 분할 된 테이블 액세스에서의 파티션 구성표 hello 전제로 이후 **픽업\_datetime**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="98969-220">Hello 전체 데이터 집합 쿼리 hello 분할 된 테이블의 사용 및/또는 색인 검색 또한 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="98969-221">탐색: medallion 및 hack_license별 여정 분포</span><span class="sxs-lookup"><span data-stu-id="98969-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="98969-222">데이터 품질 평가: 경도 및/또는 위도가 잘못된 레코드 확인</span><span class="sxs-lookup"><span data-stu-id="98969-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="98969-223">이 예제에서는 조사 경우 잘못 된 값을 포함 하거나 hello 위도 및 경도 필드 (라디안 각도-90에서 90 사이의 이어야 함), 수도 있고 (0, 0) 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="98969-224">탐색: 왕복 여정과 비왕복 여정 분포</span><span class="sxs-lookup"><span data-stu-id="98969-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="98969-225">이 예제에서는 비교 크리스마스 된 기간에 (또는 hello 전체 데이터 집합의 hello 연도 포함 하는 경우) 지정된 된 시간에 크리스마스 하지와의 hello 수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="98969-226">이 배포는 나중에 이진 분류 모델링에 사용 하는 hello 이진 레이블 배포 toobe를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="98969-227">탐색: 팁 클래스/범위 분포</span><span class="sxs-lookup"><span data-stu-id="98969-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="98969-228">이 예에서는 기간에 (또는 hello 전체 데이터 집합의 hello 연도 포함 하는 경우) 주어진된 시간에 팁 범위의 hello 분포를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="98969-229">다중 클래스 분류 모델링에 나중에 사용 하는 hello 레이블 클래스의 hello 분포입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

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

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="98969-230">탐색: 여정 거리 계산 및 비교</span><span class="sxs-lookup"><span data-stu-id="98969-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="98969-231">이 예제에서는 hello 픽업 및 자동 전송 경도 변환한 위도 tooSQL geography 가리키는 SQL geography 포인트 차이 사용 하 여 hello 여행 거리를 계산 하 고 비교에 대 한 hello 결과의 무작위 샘플링을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="98969-232">hello 예제 toovalid만 앞에서 설명 하는 hello 데이터 품질 평가 쿼리를 사용 하 여 조정 하는 hello 결과 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

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

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="98969-233">SQL 쿼리의 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="98969-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="98969-234">hello 레이블 생성 및 geography 변환 탐색 쿼리 부분을 계산 하는 hello를 제거 하 여 사용 되는 toogenerate 레이블/기능 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="98969-235">추가 기능 엔지니어링 SQL 예 hello에 제공 됩니다 [데이터 탐색 및 IPython 전자 필기장의 기능 엔지니어링](#ipnb) 섹션.</span><span class="sxs-lookup"><span data-stu-id="98969-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="98969-236">것 hello 전체 데이터 집합 또는 SQL Server 데이터베이스 인스턴스 hello에서 직접 실행 하는 SQL 쿼리를 사용 하 여 큰 하위 집합에 더 효율적인 toorun hello 기능 생성 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="98969-237">hello 쿼리 실행할 수 **SQL Server Management Studio**, 로컬 또는 원격으로 IPython 노트북 또는 임의의 개발 도구/환경에 액세스할 수 있는 hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="98969-238">모델 빌드를 위한 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="98969-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="98969-239">hello 다음 쿼리는 조인 hello **nyctaxi\_여행** 및 **nyctaxi\_요금** 테이블, 이진 분류 레이블이 생성 **크리스마스**, 즉 다중 클래스 분류 레이블을 **팁\_클래스**, hello 전체 조인 된 데이터 집합에서 1% 무작위 샘플링을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="98969-240">이 쿼리를 복사 후 hello에 직접 붙여넣을 수 [Azure 기계 학습 스튜디오](https://studio.azureml.net) [데이터 가져오기] [ import-data] hello SQL Server 데이터베이스에서 직접 데이터 수집에 대 한 모듈 Azure의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="98969-241">잘못 된 레코드를 제외 하는 hello 쿼리 (0, 0) 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

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


## <span data-ttu-id="98969-242"><a name="ipnb"></a>IPython Notebook에서 데이터 탐색 및 기능 엔지니어링</span><span class="sxs-lookup"><span data-stu-id="98969-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="98969-243">이 섹션에서는 데이터 탐색 및 앞에서 만든 hello SQL Server 데이터베이스에 대 한 Python와 SQL 쿼리를 사용 하 여 기능 생성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="98969-244">명명 된 샘플 IPython 노트북 **machine-Learning-data-science-process-sql-story.ipynb** hello에 제공 된 **샘플 IPython 노트북** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="98969-245">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)에서 이 Notebook을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="98969-246">큰 데이터로 작업 하는 경우 시퀀스에 권장 하는 hello는 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="98969-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="98969-247">메모리 내 데이터 프레임으로 hello 데이터의 작은 샘플에서 읽어옵니다.</span><span class="sxs-lookup"><span data-stu-id="98969-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="98969-248">일부 시각화 및 탐색 하는 hello 샘플링 된 데이터를 사용 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="98969-249">데이터를 샘플링 하는 hello를 사용 하 여 기능 엔지니어링 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="98969-250">더 큰 데이터 탐색에 대 한 데이터 조작 및 기능 엔지니어링 hello Azure VM에서에서 Python tooissue SQL 쿼리 hello SQL Server 데이터베이스에 대해 직접 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="98969-251">Azure 기계 학습 모델 작성에 대 한 샘플 크기 toouse hello를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="98969-252">기계 학습 tooproceed tooAzure 준비 되 면, 하거나 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="98969-253">Hello 최종 SQL 쿼리 tooextract 및 샘플 hello 데이터 및 복사-붙여넣기 hello에 직접 쿼리를 저장 한 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="98969-254">이 메서드는 hello에 설명 된 [Azure 기계 학습에서 모델 작성](#mlmodel) 섹션.</span><span class="sxs-lookup"><span data-stu-id="98969-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="98969-255">샘플링 하는 hello와 새 데이터베이스 테이블에 작성 하는 모델에 대 한 toouse 계획 엔지니어링 된 데이터를 유지 다음 hello 새 테이블을 사용 하 여 hello에 [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="98969-256">hello 다음은 몇 가지 데이터 탐색, 데이터 시각화 및 예제 엔지니어링 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="98969-257">더 많은 예제를 hello에서 hello 샘플 SQL IPython 노트북을 참조 하십시오. **샘플 IPython 노트북** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="98969-258">데이터베이스 자격 증명 초기화</span><span class="sxs-lookup"><span data-stu-id="98969-258">Initialize Database Credentials</span></span>
<span data-ttu-id="98969-259">데이터베이스 연결 설정에서 다음 변수는 hello 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="98969-260">데이터베이스 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="98969-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="98969-261">nyctaxi_trip 테이블의 행 및 열 수 보고</span><span class="sxs-lookup"><span data-stu-id="98969-261">Report number of rows and columns in table nyctaxi_trip</span></span>
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

* <span data-ttu-id="98969-262">총 행 수 = 173179759</span><span class="sxs-lookup"><span data-stu-id="98969-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="98969-263">총 열 수 = 14</span><span class="sxs-lookup"><span data-stu-id="98969-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="98969-264">읽기에 hello SQL Server 데이터베이스에서에서 작은 데이터 샘플</span><span class="sxs-lookup"><span data-stu-id="98969-264">Read-in a small data sample from hello SQL Server Database</span></span>
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
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="98969-265">시간 tooread hello 예제 테이블은 6.492000 초</span><span class="sxs-lookup"><span data-stu-id="98969-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="98969-266">검색된 행 및 열 수 = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="98969-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="98969-267">기술 통계</span><span class="sxs-lookup"><span data-stu-id="98969-267">Descriptive Statistics</span></span>
<span data-ttu-id="98969-268">이제는 준비 tooexplore hello 샘플링 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="98969-269">Hello에 대 한 기술 통계를 살펴보면 가장 먼저 **여행\_거리** (또는 다른) 필드:</span><span class="sxs-lookup"><span data-stu-id="98969-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="98969-270">시각화: 상자 그림 예제</span><span class="sxs-lookup"><span data-stu-id="98969-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="98969-271">Hello 여행 거리 toovisualize hello 변 위치에 대 한 hello 상자 그림을 보면 다음</span><span class="sxs-lookup"><span data-stu-id="98969-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![그릴 #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="98969-273">시각화: 분포 그림 예제</span><span class="sxs-lookup"><span data-stu-id="98969-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![그릴 #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="98969-275">시각화: 가로 막대형 및 꺾은선형 차트</span><span class="sxs-lookup"><span data-stu-id="98969-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="98969-276">이 예제에서는 hello 여행 거리 다섯 개의 bin으로 범주화 하 고 결과 범주화 하는 hello를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="98969-277">Bin 분포 막대에서 위에 hello 그릴 하거나 아래와 같이 플롯을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![그릴 #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![그릴 #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="98969-280">시각화: 산점도 예제</span><span class="sxs-lookup"><span data-stu-id="98969-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="98969-281">산 점도 간에 매개 변수를 표시 **여행\_시간\_에\_초** 및 **여행\_거리** toosee 상관 관계 없는 경우</span><span class="sxs-lookup"><span data-stu-id="98969-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![그릴 #6][6]

<span data-ttu-id="98969-283">Hello 관계 확인할 수 있습니다 마찬가지로 **속도\_코드** 및 **여행\_거리**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![그릴 #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="98969-285">하위 샘플링 hello SQL의 데이터</span><span class="sxs-lookup"><span data-stu-id="98969-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="98969-286">모델 빌드에 대 한 데이터를 준비할 때 [Azure 기계 학습 스튜디오](https://studio.azureml.net), 하거나 hello에 결정할 수 있습니다 **hello 데이터 가져오기 모듈에서 직접 SQL 쿼리 toouse** 하거나 hello 엔지니어링 및 샘플링 유지 hello에 사용할 수 있는 새 테이블의 데이터 [데이터 가져오기] [ import-data] 간단한을 사용 하 여 모듈 **선택 * FROM < 프로그램\_새\_테이블\_이름 >**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="98969-287">만듭니다이 섹션에서는 새 테이블 toohold hello 샘플링 하 고 데이터에 맞게 엔지니어링 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="98969-288">Hello에 모델 작성에 대 한 직접 SQL 쿼리의 예제를 보려면 [데이터 탐색 및 SQL Server의 기능 엔지니어링](#dbexplore) 섹션.</span><span class="sxs-lookup"><span data-stu-id="98969-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="98969-289">예제 테이블 및 채우기 hello 조인할 테이블의 1%로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98969-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="98969-290">있는 경우 먼저 해당 테이블 삭제)</span><span class="sxs-lookup"><span data-stu-id="98969-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="98969-291">이 섹션에서는 hello 테이블 조인 **nyctaxi\_여행** 및 **nyctaxi\_요금**1% 무작위 샘플링을 추출 하 고 새 테이블 이름을 hello 샘플링 된 데이터를 유지,  **nyctaxi\_하나의\_%**:</span><span class="sxs-lookup"><span data-stu-id="98969-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

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

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="98969-292">IPython Notebook에서 SQL 쿼리를 사용하여 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="98969-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="98969-293">이 섹션에서는 위에서 만든 hello 새 테이블에서 유지 되는 hello 1% 샘플링 된 데이터를 사용 하 여 데이터 분포 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="98969-294">비슷한 탐색을 사용 하 여 필요에 따라 hello 원래 테이블을 사용 하 여 수행할 수 있도록 참고 **TABLESAMPLE** toolimit hello 탐색 샘플 또는 hello를 제한 하 여 결과 hello를 사용 하 여 시간 간격을 지정 하는 tooa **픽업 \_datetime** hello에 설명 된 대로 분할 [데이터 탐색 및 SQL Server의 기능 엔지니어링](#dbexplore) 섹션.</span><span class="sxs-lookup"><span data-stu-id="98969-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="98969-295">탐색: 일일 여정 분포</span><span class="sxs-lookup"><span data-stu-id="98969-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="98969-296">탐색: medallion당 여정 분포</span><span class="sxs-lookup"><span data-stu-id="98969-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="98969-297">IPython Notebook에서 SQL 쿼리를 사용하여 기능 생성</span><span class="sxs-lookup"><span data-stu-id="98969-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="98969-298">이 섹션에 새 레이블을 생성 합니다 및 hello 이전 섹션에서 만든 SQL 쿼리를 사용 하 여 직접 기능을 hello 1% 예제 테이블에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="98969-299">레이블 생성: 클래스 레이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="98969-300">다음 예제는 hello에서 두 가지 모델링에 대 한 레이블 toouse 생성:</span><span class="sxs-lookup"><span data-stu-id="98969-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="98969-301">이진 클래스 레이블 **tipped** (팁이 제공되는지 예측)</span><span class="sxs-lookup"><span data-stu-id="98969-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="98969-302">다중 클래스 레이블을 **팁\_클래스** (예측 hello 팁 bin 또는 범위)</span><span class="sxs-lookup"><span data-stu-id="98969-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
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

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="98969-303">기능 엔지니어링: 범주 열에 대한 개수 기능</span><span class="sxs-lookup"><span data-stu-id="98969-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="98969-304">이 예제에서는 해당 hello 데이터의 hello 개수와 각 범주를 대체 하 여 숫자 필드에 범주별 필드를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

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

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="98969-305">기능 엔지니어링: 숫자 열에 대한 Bin 기능</span><span class="sxs-lookup"><span data-stu-id="98969-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="98969-306">이 예제에서는 연속 숫자 필드를 사전 설정된 범주 범위로 변환합니다. 즉, 숫자 필드를 범주 필드로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

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

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="98969-307">기능 엔지니어링: 10진수 위도/경도에서 위치 기능 추출</span><span class="sxs-lookup"><span data-stu-id="98969-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="98969-308">이 예제에서는 hello 위도 및 경도 필드의 10 진수 표현으로 분할 다양 한 세분성의 여러 지역 필드와 같은 국가, 도시, 동, 블록 등 됩니다. 아닌 hello 새 지역 필드는 tooactual 위치 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="98969-309">지오코드 위치 매핑에 대한 자세한 내용은 [Bing Maps REST 서비스](https://msdn.microsoft.com/library/ff701710.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98969-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

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

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="98969-310">Hello hello 들어가지 않고 기능화 테이블의 최종 형태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="98969-311">준비 tooproceed toomodel 건물과 모델 배포에는 이제 [Azure 기계 학습](https://studio.azureml.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="98969-312">hello 데이터는 즉 앞에서 확인 하는 hello 예측 문제에 대 한 준비:</span><span class="sxs-lookup"><span data-stu-id="98969-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="98969-313">이진 분류: toopredict 트립이 팁 지불 여부.</span><span class="sxs-lookup"><span data-stu-id="98969-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="98969-314">다중 클래스 분류: toohello 이전에 정의 된 클래스에 따라 지불을 끝의 toopredict hello 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="98969-315">회귀 작업: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="98969-316"><a name="mlmodel"></a>Azure 기계 학습에서 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="98969-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="98969-317">toobegin hello 모델링 연습 tooyour Azure 기계 학습 작업 영역에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="98969-318">기계 학습 작업 영역을 아직 만들지 않은 경우 [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98969-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="98969-319">Azure 기계 학습 시작 tooget 참조 [Azure 기계 학습 스튜디오는 무엇입니까?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="98969-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="98969-320">로그 너무[Azure 기계 학습 스튜디오](https://studio.azureml.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="98969-321">hello Studio 홈 페이지는 다양 한 정보, 비디오, 자습서, 링크 toohello 모듈 참조 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="98969-322">Azure 기계 학습에 대 한 자세한 내용은 hello를 참조 하십시오. [Azure 기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="98969-323">일반적인 학습 실험 hello 다음 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="98969-324">**+새** 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="98969-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="98969-325">Hello 데이터 tooAzure를 기계 학습을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98969-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="98969-326">전처리 하 고, 변환 및 필요에 따라 hello 데이터를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="98969-327">필요에 따라 기능을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-327">Generate features as needed.</span></span>
5. <span data-ttu-id="98969-328">Hello 데이터를 학습 /, 유효성 검사, 테스트 데이터 집합 분할 (별도 데이터 집합 수도 있고 각각에 대해).</span><span class="sxs-lookup"><span data-stu-id="98969-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="98969-329">하나 이상의 기계 학습 문제 toosolve 학습 hello에 따라 알고리즘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="98969-330">이진 분류, 다중 클래스 분류, 회귀)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="98969-331">Hello 학습 데이터 집합을 사용 하 여 하나 이상의 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="98969-332">Hello 학습 된 모델을 사용 하 여 hello 유효성 검사 데이터 집합을 점수를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="98969-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="98969-333">Hello 모델로 toocompute hello 관련 메트릭 hello 학습 문제에 대 한 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="98969-334">Hello 모델 및 선택 hello 최상의 모델 toodeploy 미세 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="98969-335">이 연습에서는 이미 탐색 하 고 SQL Server에서 hello 데이터 엔지니어링 했으며 hello 샘플 크기 tooingest Azure 기계 학습에서 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="98969-336">하나 이상의 hello 예측 모델 toobuild 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="98969-337">Hello 데이터 tooAzure 기계 학습 가져오기 hello를 사용 하 여 [데이터 가져오기] [ import-data] hello에서 사용할 수 있는 모듈 **데이터 입력 및 출력** 섹션.</span><span class="sxs-lookup"><span data-stu-id="98969-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="98969-338">자세한 내용은 참조 hello [데이터 가져오기] [ import-data] 모듈 참조 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Azure 기계 학습 데이터 가져오기][17]
2. <span data-ttu-id="98969-340">선택 **Azure SQL 데이터베이스** hello로 **데이터 소스** hello에 **속성** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="98969-341">Hello에 hello 데이터베이스 DNS 이름을 입력 **데이터베이스 서버 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="98969-342">형식: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="98969-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="98969-343">Hello 입력 **데이터베이스 이름** hello 해당 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="98969-344">Hello 입력 **SQL 사용자 이름** hello에서 * * 서버 사용자 aqccount 이름 및 hello에 hello 암호 **서버 사용자 계정 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="98969-345">**모든 서버 인증서 허용** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="98969-346">Hello에 **데이터베이스 쿼리** 텍스트 영역을 편집, hello 필요한 데이터베이스 필드 (예: hello 레이블 모든 계산된 필드 포함), 아래에 추출 hello 데이터 원하는 toohello 샘플 크기를 샘플링 하는 hello 쿼리를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="98969-347">아래 hello 그림에 hello SQL Server 데이터베이스에서 직접 데이터를 읽는 이진 분류 실험의 예가입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="98969-348">다중 클래스 분류 및 회귀 문제에 대한 유사한 실험을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure 기계 학습][10]

> [!IMPORTANT]
> <span data-ttu-id="98969-350">데이터 추출을 모델링 하 고 이전 섹션에서 제공 하는 쿼리 예제 샘플링 hello에 **hello 3 모델링 연습에 대 한 모든 레이블을 hello 쿼리에 포함 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="98969-351">각 연습을 모델링 하는 hello (필수) 중요 한 단계는 너무**제외** 다른 두 가지 문제 및 기타 hello에 대 한 불필요 한 레이블을 hello **누수 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="98969-352">에 대 한 예: 이진 분류를 사용할 때 사용 하 여 hello 레이블 **크리스마스** hello 필드를 제외 하 고 **팁\_클래스**, **팁\_양**, 및 **총\_양**합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="98969-353">후자의 hello 대상 누수 hello 팁 사실도 지불 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="98969-354">hello tooexclude 불필요 한 열 및/또는 대상 누수를 사용할 수 있습니다 [데이터 집합의 열 선택] [ select-columns] 모듈 또는 hello [메타 데이터 편집] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="98969-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="98969-355">자세한 내용은 [데이터 집합의 열 선택][select-columns] 및 [메타데이터 편집][edit-metadata] 참조 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98969-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="98969-356"><a name="mldeploy"></a>Azure 기계 학습에서 모델 배포</span><span class="sxs-lookup"><span data-stu-id="98969-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="98969-357">모델에 준비 되 면 hello 실험에서 직접 웹 서비스로 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="98969-358">Azure 기계 학습 웹 서비스 배포에 대한 자세한 내용은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98969-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="98969-359">새 웹 서비스 toodeploy 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="98969-360">점수 매기기 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98969-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="98969-361">Hello 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-361">Deploy hello web service.</span></span>

<span data-ttu-id="98969-362">점수 매기기를 실험 toocreate는 **마침** 클릭 실험 교육, **점수 매기기 실험 만들기** hello 아래 작업 표시줄에 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Azure 점수 매기기][18]

<span data-ttu-id="98969-364">Azure 기계 학습 점수 매기기 실험 hello 학습 실험의 hello 구성 요소에 따라 toocreate를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="98969-365">특히 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-365">In particular, it will:</span></span>

1. <span data-ttu-id="98969-366">Hello 학습 된 모델을 저장 하 고 hello 모델 학습 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="98969-367">논리적 식별 **입력 포트** toorepresent hello 입력된 데이터 스키마를 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="98969-368">논리적 식별 **출력 포트** toorepresent hello 예상된 웹 서비스 출력 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="98969-369">실험 점수 매기기 hello 만들어지면 검토 하 고 필요에 따라 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="98969-370">이러한 표시 되지 것입니다 hello 서비스를 호출 하는 경우 일반적인 조정은 tooreplace hello 입력된 데이터 집합 및/또는 레이블 필드를 제외를 사용 하 여 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="98969-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="98969-371">것이 좋습니다 tooreduce hello 크기인 hello 입력 데이터 집합 및/또는 쿼리 tooa 소수의 레코드 데 충분 한 tooindicate hello 입력된 스키마도입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="98969-372">Hello 출력 포트에 대 한 일반적인 tooexclude 모든 입력된 필드 이며 hello 포함 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률** hello hello를 사용 하 여 출력에 [데이터 집합의 열 선택 ] [ select-columns] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="98969-373">샘플 실험을 점수 매기기 아래 hello 그림에 있는 경우</span><span class="sxs-lookup"><span data-stu-id="98969-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="98969-374">Toodeploy, 준비 되 면 hello 클릭 **웹 서비스 게시** hello 낮은 작업 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="98969-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure 기계 학습 게시][11]

<span data-ttu-id="98969-376">toorecap,이 연습에서는 자습서에서 큰 공용 데이터 집합 데이터 취득 toomodel 학습 및 Azure 기계 학습 웹 서비스의 배포에서 모든 hello 방법에 대해 작업 하는 Azure 데이터 과학 환경을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="98969-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="98969-377">라이선스 정보</span><span class="sxs-lookup"><span data-stu-id="98969-377">License Information</span></span>
<span data-ttu-id="98969-378">이 샘플 연습 및 그에 따른 스크립트 및 IPython notebook(s)은 hello MIT 라이선스에 따라 Microsoft에서 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98969-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="98969-379">자세한 내용은 GitHub에서 hello 샘플 코드의 hello 디렉터리에 hello LICENSE.txt 파일 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="98969-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="98969-380">참조</span><span class="sxs-lookup"><span data-stu-id="98969-380">References</span></span>
<span data-ttu-id="98969-381">• [Andrés Monroy NYC Taxi Trips 다운로드 페이지](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="98969-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="98969-382">• [Chris Whong의 FOILing NYC Taxi Trip 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="98969-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="98969-383">• [NYC Taxi 및 Limousine 수수료 연구 및 통계](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="98969-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
