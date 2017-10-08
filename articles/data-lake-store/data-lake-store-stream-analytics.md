---
title: "데이터 레이크 저장소에 대 한 스트림 분석에서 aaaStream 데이터 | Microsoft Docs"
description: "Azure 스트림 분석 toostream 데이터를 사용 하 여 Azure 데이터 레이크 저장소로"
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
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="359da-103">Azure 스트림 분석을 사용하여 Azure 저장소 Blob에서 Data Lake 저장소에 데이터 스트리밍</span><span class="sxs-lookup"><span data-stu-id="359da-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="359da-104">이 문서에서 toouse Azure 데이터 레이크 저장 되는 방식과 Azure 스트림 분석 작업에 대 한 출력으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="359da-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="359da-105">이 문서에서는 Azure 저장소 blob (입력)에서 데이터를 읽고 하는 간단한 시나리오를 설명 하 고 쓰기 hello 데이터 tooData 레이크 저장소 (출력).</span><span class="sxs-lookup"><span data-stu-id="359da-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="359da-106">이때 데이터 레이크 저장소의 생성 및 구성 출력 스트림 분석 hello 에서만 지원 됩니다 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="359da-107">따라서이 자습서의 일부 hello Azure 클래식 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="359da-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="359da-108">Prerequisites</span></span>
<span data-ttu-id="359da-109">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="359da-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="359da-110">**An Azure subscription**.</span></span> <span data-ttu-id="359da-111">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="359da-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="359da-112">**Azure Storage 계정**.</span><span class="sxs-lookup"><span data-stu-id="359da-112">**Azure Storage account**.</span></span> <span data-ttu-id="359da-113">스트림 분석 작업에 대 한이 계정 tooinput 데이터에서 blob 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="359da-114">이 자습서에서는 가정 라는 저장소 계정이 있는 **storageforasa** hello 계정 내의 컨테이너 및 **storageforasacontainer**합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="359da-115">Hello 컨테이너를 만든 후에 예제 데이터 파일 tooit을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="359da-116">**Azure Data Lake Store 계정**.</span><span class="sxs-lookup"><span data-stu-id="359da-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="359da-117">Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="359da-118">**asadatalakestore**라는 Data Lake Store 계정이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="359da-119">스트림 분석 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="359da-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="359da-120">입력 원본 및 출력 대상을 포함하는 스트림 분석 작업을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="359da-121">이 자습서에 대 한 hello 원본이 Azure blob 컨테이너가 있으며 hello 대상이 데이터 레이크 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="359da-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="359da-122">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="359da-123">Hello 왼쪽된 창에서 클릭 **스트림 분석 작업이**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="359da-124">![Stream Analytics 작업 만들기](./media/data-lake-store-stream-analytics/create.job.png "Stream Analytics 작업 만들기")</span><span class="sxs-lookup"><span data-stu-id="359da-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="359da-125">Hello에서 작업을 만드는 확인 hello 저장소 계정 또는 사용자와 동일한 지역에 지역 간 데이터 이동의 추가 비용 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="359da-126">Hello 작업에 대 한 Blob 입력 만들기</span><span class="sxs-lookup"><span data-stu-id="359da-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="359da-127">Hello 왼쪽된 창에서 hello 스트림 분석 작업에 대 한 열기 hello 페이지 클릭 hello **입력** 탭을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="359da-128">![입력된 tooyour 작업에 추가할](./media/data-lake-store-stream-analytics/create.input.1.png "입력된 tooyour 작업 추가")</span><span class="sxs-lookup"><span data-stu-id="359da-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="359da-129">Hello에 **새 입력** 블레이드에서 hello 다음 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="359da-130">![입력된 tooyour 작업에 추가할](./media/data-lake-store-stream-analytics/create.input.2.png "입력된 tooyour 작업 추가")</span><span class="sxs-lookup"><span data-stu-id="359da-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="359da-131">에 대 한 **입력 별칭**를 작업 입력 hello에 대 한 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="359da-132">**원본 형식**으로 **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="359da-133">**원본**으로 **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="359da-134">**구독**에 대해 **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="359da-135">에 대 한 **저장소 계정**, hello 필수 소프트웨어의 일부로 만든 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="359da-136">에 대 한 **컨테이너**선택, hello 컨테이너에서 hello 만든 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="359da-137">**이벤트 직렬화 형식**으로 **CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="359da-138">**구분 기호**로 **탭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="359da-139">**인코딩**으로 **UTF-8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="359da-140">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-140">Click **Create**.</span></span> <span data-ttu-id="359da-141">이제 hello 포털 hello 입력을 추가 하 고 hello 연결 tooit를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="359da-142">Hello 작업에 대 한 데이터 레이크 저장소 출력 만들기</span><span class="sxs-lookup"><span data-stu-id="359da-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="359da-143">Hello 스트림 분석 작업에 대 한 hello 페이지, hello 클릭 **출력** 탭을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="359da-144">![출력 tooyour 작업을 추가](./media/data-lake-store-stream-analytics/create.output.1.png "출력 tooyour 작업 추가")</span><span class="sxs-lookup"><span data-stu-id="359da-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="359da-145">Hello에 **새 출력** 블레이드에서 hello 다음 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="359da-146">![출력 tooyour 작업을 추가](./media/data-lake-store-stream-analytics/create.output.2.png "출력 tooyour 작업 추가")</span><span class="sxs-lookup"><span data-stu-id="359da-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="359da-147">에 대 한 **출력 별칭**를 입력 한 hello 작업 출력에 대 한 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="359da-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="359da-148">쿼리 toodirect hello 쿼리 출력 toothis Data Lake 저장소에에서 사용 되는 친숙 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="359da-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="359da-149">**싱크**로 **Data Lake Store**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="359da-150">입력 정보 요청된 tooauthorize 됩니다 tooData Lake 저장소 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="359da-151">**권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="359da-152">Hello에 **새 출력** 블레이드에서 tooprovide hello 다음 값을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="359da-153">![출력 tooyour 작업을 추가](./media/data-lake-store-stream-analytics/create.output.3.png "출력 tooyour 작업 추가")</span><span class="sxs-lookup"><span data-stu-id="359da-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="359da-154">에 대 한 **계정 이름**를 전송 하는 hello 작업 출력 toobe 저장할 이미 만든 hello 데이터 레이크 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="359da-155">에 대 한 **경로 접두사 패턴**, 입력 파일에 사용 된 경로 toowrite hello 내에서 파일에 데이터 레이크 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="359da-156">에 대 한 **날짜 형식**, 날짜 토큰을 사용 하는 hello 접두사 경로 있는 경우 파일 구성 됩니다 hello 날짜 형식을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359da-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="359da-157">에 대 한 **시간 형식**시간 토큰을 사용 하는 hello 접두사 경로 있는 경우, 사용자 파일 구성할 지 hello 시간 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="359da-158">**이벤트 직렬화 형식**으로 **CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="359da-159">**구분 기호**로 **탭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="359da-160">**인코딩**으로 **UTF-8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="359da-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-161">Click **Create**.</span></span> <span data-ttu-id="359da-162">이제 hello 포털 hello 출력을 추가 하 고 hello 연결 tooit를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="359da-163">Hello 스트림 분석 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="359da-164">스트림 분석 작업 toorun hello에서 쿼리를 실행 해야 **쿼리** 탭 합니다. 이 자습서에서는 대체 하 여 hello 예제 쿼리를 실행할 수 있습니다 hello 화면 캡처 아래와 같이 hello로 hello 자리 표시자 작업 입력 및 출력 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="359da-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="359da-165">![쿼리 실행](./media/data-lake-store-stream-analytics/run.query.png "쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="359da-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="359da-166">클릭 **저장** 그 다음 hello hello hello 화면 맨 위에서 **개요** 탭을 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="359da-167">Hello 대화 상자에서 선택 **사용자 지정 시간**, hello 현재 날짜 및 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="359da-168">![작업 시간 설정](./media/data-lake-store-stream-analytics/run.query.2.png "작업 시간 설정")</span><span class="sxs-lookup"><span data-stu-id="359da-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="359da-169">클릭 **시작** toostart hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="359da-170">최대 tooa 몇 분 toostart hello 작업을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359da-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="359da-171">hello blob에서 tootrigger hello 작업 toopick hello 데이터 샘플 데이터 파일 toohello blob 컨테이너를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="359da-172">Hello에서 예제 데이터 파일을 가져올 수 있습니다 [Azure 데이터 레이크 Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="359da-173">이 자습서에 대 한 복사 hello 파일 **vehicle1_09142014.csv**합니다.</span><span class="sxs-lookup"><span data-stu-id="359da-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="359da-174">와 같은 다양 한 클라이언트를 사용할 수 [Azure 저장소 탐색기](http://storageexplorer.com/), tooupload 데이터 tooa blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="359da-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="359da-175">Hello에서 **개요** 탭의 **모니터링**, hello 데이터 처리 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="359da-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="359da-176">![작업 모니터링](./media/data-lake-store-stream-analytics/run.query.3.png "작업 모니터링")</span><span class="sxs-lookup"><span data-stu-id="359da-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="359da-177">마지막으로 hello 작업 출력 데이터를 hello Data Lake 저장소 계정에서 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359da-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="359da-178">![출력 확인](./media/data-lake-store-stream-analytics/run.query.4.png "출력 확인")</span><span class="sxs-lookup"><span data-stu-id="359da-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="359da-179">Hello 데이터 탐색기 창에서 해당 hello 출력으로 작성 된 tooa 폴더 경로에 지정 된 hello 데이터 레이크 저장소 출력 설정 확인 (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="359da-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="359da-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="359da-180">See also</span></span>
* [<span data-ttu-id="359da-181">HDInsight 클러스터 toouse 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="359da-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
