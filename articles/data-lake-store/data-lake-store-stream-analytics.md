---
title: "Stream Analytics에서 Data Lake Store로 데이터 스트리밍 | Microsoft 문서"
description: "Azure 스트림 분석을 사용하여 Azure Data Lake 저장소에 데이터 스트리밍"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="25beb-103">Azure 스트림 분석을 사용하여 Azure 저장소 Blob에서 Data Lake 저장소에 데이터 스트리밍</span><span class="sxs-lookup"><span data-stu-id="25beb-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="25beb-104">이 문서는 Azure 스트림 분석 작업에 대한 출력으로 Azure Data Lake 저장소를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="25beb-105">이 문서에서는 Azure 저장소 Blob(입력)에서 데이터를 읽고 Data Lake 저장소(출력)에 데이터를 기록하는 간단한 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="25beb-106">이 때 [Azure 클래식 포털](https://manage.windowsazure.com)에서만 스트림 분석에 대한 Data Lake Store 출력을 만들고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="25beb-107">따라서 이 자습서의 일부는 Azure 클래식 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="25beb-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="25beb-108">Prerequisites</span></span>
<span data-ttu-id="25beb-109">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="25beb-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="25beb-110">**An Azure subscription**.</span></span> <span data-ttu-id="25beb-111">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25beb-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="25beb-112">**Azure Storage 계정**.</span><span class="sxs-lookup"><span data-stu-id="25beb-112">**Azure Storage account**.</span></span> <span data-ttu-id="25beb-113">이 계정에서 Blob 컨테이너를 사용하여 스트림 분석 작업에 대한 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="25beb-114">이 자습서의 경우 **storageforasa**라는 저장소 계정 및 **storageforasacontainer**라는 계정 내의 컨테이너가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="25beb-115">컨테이너를 만든 후에 샘플 데이터 파일을 거기에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="25beb-116">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="25beb-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="25beb-117">[Azure Portal을 사용하여 Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)에 있는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="25beb-118">**asadatalakestore**라는 Data Lake Store 계정이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="25beb-119">스트림 분석 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="25beb-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="25beb-120">입력 원본 및 출력 대상을 포함하는 스트림 분석 작업을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="25beb-121">이 자습서의 경우 원본은 Azure blob 컨테이너이고 대상은 Data Lake 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="25beb-122">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="25beb-123">왼쪽 창에서 **Stream Analytics 작업**을 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="25beb-124">![Stream Analytics 작업 만들기](./media/data-lake-store-stream-analytics/create.job.png "Stream Analytics 작업 만들기")</span><span class="sxs-lookup"><span data-stu-id="25beb-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="25beb-125">저장소 계정과 동일한 지역에 작업을 만들지 않으면 지역 간에 데이터를 이동하는 데 추가 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="25beb-126">작업에 대한 Blob 입력 만들기</span><span class="sxs-lookup"><span data-stu-id="25beb-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="25beb-127">Stream Analytics 작업 페이지를 열고 왼쪽 창에서 **입력** 탭을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="25beb-128">![작업에 입력 추가](./media/data-lake-store-stream-analytics/create.input.1.png "작업에 입력 추가")</span><span class="sxs-lookup"><span data-stu-id="25beb-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="25beb-129">**새 입력** 블레이드에서 다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="25beb-130">![작업에 입력 추가](./media/data-lake-store-stream-analytics/create.input.2.png "작업에 입력 추가")</span><span class="sxs-lookup"><span data-stu-id="25beb-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="25beb-131">**입력 별칭**에 작업 입력에 대한 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="25beb-132">**원본 형식**으로 **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="25beb-133">**원본**으로 **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="25beb-134">**구독**에 대해 **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="25beb-135">**저장소 계정**에서 필수 조건의 일부로 만든 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="25beb-136">**컨테이너**에 대해 선택한 저장소 계정에서 만든 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="25beb-137">**이벤트 직렬화 형식**으로 **CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="25beb-138">**구분 기호**로 **탭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="25beb-139">**인코딩**으로 **UTF-8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="25beb-140">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-140">Click **Create**.</span></span> <span data-ttu-id="25beb-141">이제 포털에 입력이 추가되고 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="25beb-142">작업에 대한 Data Lake 저장소 출력 만들기</span><span class="sxs-lookup"><span data-stu-id="25beb-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="25beb-143">Stream Analytics 작업에 대한 페이지를 열고 **출력** 탭을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="25beb-144">![작업에 출력 추가](./media/data-lake-store-stream-analytics/create.output.1.png "작업에 출력 추가")</span><span class="sxs-lookup"><span data-stu-id="25beb-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="25beb-145">**새 출력** 블레이드에서 다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="25beb-146">![작업에 출력 추가](./media/data-lake-store-stream-analytics/create.output.2.png "작업에 출력 추가")</span><span class="sxs-lookup"><span data-stu-id="25beb-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="25beb-147">**입력 별칭**에 작업 출력에 대한 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="25beb-148">쿼리 출력을 이 Data Lake 저장소로 직접 보내기 위해 쿼리에서 사용되는 식별 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="25beb-149">**싱크**로 **Data Lake Store**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="25beb-150">Data Lake Store 계정에 대한 액세스 권한을 부여하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="25beb-151">**권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="25beb-152">**새 출력** 블레이드에서 계속 다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="25beb-153">![작업에 출력 추가](./media/data-lake-store-stream-analytics/create.output.3.png "작업에 출력 추가")</span><span class="sxs-lookup"><span data-stu-id="25beb-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="25beb-154">**계정 이름**에는 작업 출력을 전송하려는 위치에 미리 만든 Data Lake Store 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="25beb-155">**경로 접두사 패턴**에는 지정된 Data Lake Store 계정 내에서 파일을 작성하는 데 사용되는 파일 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="25beb-156">**날짜 형식**의 경우, 접두사 경로에 날짜 토큰을 사용한 경우 파일을 구성하는 날짜 형식을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="25beb-157">**시간 형식**의 경우, 접두사 경로에 시간 토큰을 사용한 경우 파일을 구성하는 시간 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="25beb-158">**이벤트 직렬화 형식**으로 **CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="25beb-159">**구분 기호**로 **탭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="25beb-160">**인코딩**으로 **UTF-8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="25beb-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-161">Click **Create**.</span></span> <span data-ttu-id="25beb-162">이제 포털에 출력이 추가되고 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="25beb-163">스트림 분석 작업 실행</span><span class="sxs-lookup"><span data-stu-id="25beb-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="25beb-164">Stream Analytics 작업을 실행하려면 **쿼리** 탭에서 쿼리를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="25beb-165">이 자습서에서는 아래의 화면 캡처와 같이 작업 입력 및 출력 별칭으로 자리 표시자를 대체하여 샘플 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="25beb-166">![쿼리 실행](./media/data-lake-store-stream-analytics/run.query.png "쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="25beb-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="25beb-167">화면 맨 위에서 **저장**을 클릭한 다음 **개요** 탭에서 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="25beb-168">대화 상자에서 **사용자 지정 시간**을 선택한 다음 현재 날짜 및 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="25beb-169">![작업 시간 설정](./media/data-lake-store-stream-analytics/run.query.2.png "작업 시간 설정")</span><span class="sxs-lookup"><span data-stu-id="25beb-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="25beb-170">**시작**을 클릭하여 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-170">Click **Start** to start the job.</span></span> <span data-ttu-id="25beb-171">작업을 시작하는 데 최대 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="25beb-172">Blob에서 데이터를 선택하는 작업을 트리거하려면 샘플 데이터 파일을 Blob 컨테이너에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="25beb-173">[Azure Data Lake Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)에서 샘플 데이터 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="25beb-174">이 자습서에서는 **vehicle1_09142014.csv** 파일을 복사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="25beb-175">[Azure 저장소 탐색기](http://storageexplorer.com/)와 같은 다양한 클라이언트를 사용하여 Blob 컨테이너에 데이터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="25beb-176">**개요** 탭의 **모니터링** 아래에서 데이터가 처리된 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="25beb-177">![작업 모니터링](./media/data-lake-store-stream-analytics/run.query.3.png "작업 모니터링")</span><span class="sxs-lookup"><span data-stu-id="25beb-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="25beb-178">마지막으로 Data Lake Store 계정에서 작업 출력 데이터가 제공되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="25beb-179">![출력 확인](./media/data-lake-store-stream-analytics/run.query.4.png "출력 확인")</span><span class="sxs-lookup"><span data-stu-id="25beb-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="25beb-180">데이터 탐색기 창에서 Data Lake Store 출력 설정(`streamanalytics/job/output/{date}/{time}`)에 지정된 대로 출력이 폴더 경로에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="25beb-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="25beb-181">참고 항목</span><span class="sxs-lookup"><span data-stu-id="25beb-181">See also</span></span>
* [<span data-ttu-id="25beb-182">HDInsight 클러스터를 만들어 Data Lake 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="25beb-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
