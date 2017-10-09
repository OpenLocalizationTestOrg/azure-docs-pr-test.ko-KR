---
title: Azure StorSimple Data Manager UI aaaMicrosoft | Microsoft Docs
description: "설명 방법을 toouse 데이터 StorSimple 관리자 서비스 UI (비공개 미리 보기)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="5e680-103">Hello 데이터 StorSimple Manager 서비스 UI (비공개 미리 보기)를 사용 하 여 관리</span><span class="sxs-lookup"><span data-stu-id="5e680-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="5e680-104">이 문서에서는 hello StorSimple 8000 시리즈 장치에 있는 데이터에 StorSimple Data Manager UI tooperform 데이터 변환 hello를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="5e680-105">hello 변환 된 데이터가 다음에서 사용할 수 Azure 미디어 서비스, Azure HDInsight, Azure 기계 학습 및 Azure 검색 등 다른 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="5e680-106">StorSimple 데이터 변환 사용</span><span class="sxs-lookup"><span data-stu-id="5e680-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="5e680-107">hello StorSimple 데이터 관리자는 hello 리소스는 데이터 변환을 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="5e680-108">데이터 변환 서비스 hello를 사용 하면 Azure 저장소에 StorSimple 온-프레미스 장치 tooblobs 프로그램에서 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="5e680-109">따라서 워크플로에서 toospecify hello 세부 정보에 대해 필요한 toomove toohello 저장소 계정 관심 StorSimple 장치와 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="5e680-110">StorSimple 데이터 관리자 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5e680-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="5e680-111">Hello 단계 toocreate 데이터 StorSimple Manager 서비스를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="5e680-112">데이터 StorSimple 관리자 서비스 toocreate 너무 이동[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="5e680-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="5e680-113">Hello 클릭  **+**  아이콘과 StorSimple 데이터 관리자에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="5e680-114">StorSimple 데이터 관리자 서비스를 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="5e680-115">구독을 하도록 구성 되어이 서비스를 만드는 다음 블레이드 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![StorSimple 데이터 관리자 리소스 만들기](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="5e680-117">Hello 입력을 입력 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="5e680-118">hello 지정 위치 hello 저장소 계정 및 StorSimple Manager 서비스를 저장 하는 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="5e680-119">현재 미국 서부 및 유럽 서부에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="5e680-120">따라서 StorSimple Manager 서비스, 데이터 관리자 서비스 및 hello 연결 된 저장소 계정 모두 hello 위의 지원 영역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="5e680-121">분 toocreate hello 서비스에 대 한 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="5e680-122">데이터 변환 작업 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="5e680-122">Create a data transformation job definition</span></span>

<span data-ttu-id="5e680-123">데이터 StorSimple 관리자 서비스 내에서 toocreate 데이터 변환 작업 정의 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="5e680-124">작업 정의 hello 네이티브 형식에서 저장소 계정에 이동 하 여 관심 있는 hello 데이터의 세부 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="5e680-125">Hello 단계 toocreate 새 데이터 변환 작업 정의 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="5e680-126">Toohello 만든 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="5e680-127">**+작업 정의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-127">Click **+ Job Definition**.</span></span>

    ![+작업 정의 클릭](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="5e680-129">hello 새 작업 정의 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="5e680-130">작업 정의에 이름을 지정하고 **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="5e680-131">Hello에 **구성 데이터 원본** 블레이드에서 StorSimple 장치의 hello 세부 정보를 지정 하 고 관심 있는 데이터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![작업 정의 만들기](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="5e680-133">새 데이터 관리자 서비스이기 때문에 데이터 리포지토리가 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="5e680-134">tooadd을 데이터 저장소로 StorSimple Manager 클릭 **새로 추가** 데이터 저장소 드롭다운 hello와 클릭 **데이터 저장소 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="5e680-135">선택 **StorSimple 8000 시리즈 관리자** hello 저장소로 입력 하 고 hello 속성을 입력 하면 **StorSimple Manager**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="5e680-136">Hello에 대 한 **리소스 Id** tooenter hello 번호 hello 하기 전에 필요한 필드 **:** StorSimple manager의 hello 등록 키에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![데이터 원본 만들기](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="5e680-138">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-138">Click **OK** when done.</span></span> <span data-ttu-id="5e680-139">이렇게 하면 데이터 리포지토리를 절약하고 이러한 매개 변수를 다시 입력하지 않고 다른 작업 정의에서 이 StorSimple Manager를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="5e680-140">클릭 한 후 몇 초 **확인** hello 드롭다운에서 StorSimple Manager tooshow hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="5e680-141">Hello에 **구성 데이터 원본** 블레이드에서 hello 장치 이름을 입력 하 고 hello 관심 있는 데이터에 있는 볼륨 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="5e680-142">Hello에 **필터** 하위 섹션에서 관심 있는 데이터를 포함 하는 hello 루트 디렉터리를 입력 (로 시작 해야이 필드는 `\`).</span><span class="sxs-lookup"><span data-stu-id="5e680-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="5e680-143">여기에서 파일 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="5e680-144">hello 데이터 변환 서비스 toohello Azure 통해 스냅숏이 푸시됩니다 hello 데이터에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="5e680-145">이 작업을 실행할 때 선택할 수 있습니다 tootake 백업 될 때마다 (최신 데이터에 대해 toowork)를 실행 되는이 작업 또는 toouse hello hello 클라우드의 마지막 기존 백업을 (보관 된 일부 데이터에서 작업 하는) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5e680-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![새 데이터 원본 세부 정보](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="5e680-147">다음으로 hello 대상 설정 구성 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="5e680-148">지원되는 대상에는 Azure Storage 계정 및 Azure Media Services 계정이라는 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="5e680-149">해당 계정에 blob을 저장소 계정 tooput 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="5e680-150">해당 계정에 자산에 미디어 서비스 계정 tooput 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="5e680-151">다시, tooadd 리포지토리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="5e680-152">Hello 드롭다운에서 선택 **새로 추가** 차례로 **설정을 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![데이터 싱크 만들기](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="5e680-154">여기에서는 hello 유형의 저장소 tooadd 및 hello hello 리포지토리와 연결 된 다른 매개 변수를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="5e680-155">두 경우 모두 저장소 큐 hello 작업이 실행 될 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="5e680-156">이 큐는 준비가 완료된 변환 Blob에 대한 메시지로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="5e680-157">이 큐의 hello 이름 hello 작업 정의의 hello 이름과 달라 서 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="5e680-158">선택 하는 경우 **미디어 서비스** hello 리포지토리 유형으로 다음을 입력할 수도 있습니다 저장소 계정 자격 증명 hello 큐를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![새 데이터 싱크 세부 정보](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="5e680-160">(적용 하는 몇 초 정도) hello 데이터 저장소를 추가한 후 hello에 hello 드롭다운에서에서 hello 리포지토리를 찾을 수 있습니다 **대상 계정 이름이**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="5e680-161">필요한 hello 대상을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="5e680-162">클릭 **확인** toocreate hello 작업 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="5e680-163">이제 작업 정의가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-163">Your job definition is now set up.</span></span> <span data-ttu-id="5e680-164">이 작업 정의 hello UI 통해 여러 번 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-164">You can use this job definition multiple times via hello UI.</span></span>

    ![새 작업 정의 추가](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="5e680-166">Hello 작업 정의 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-166">Run hello job definition</span></span>

<span data-ttu-id="5e680-167">Tooinvoke 해야는 hello 작업 정의에 지정 된 StorSimple toohello 저장소 계정에서 toomove 데이터를 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="5e680-168">Hello 작업을 호출할 때마다 hello 매개 변수 변경에 더 일부 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="5e680-169">hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="5e680-170">데이터 StorSimple Manager 서비스를 선택 하 고 너무 이동**모니터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="5e680-171">**지금 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-171">Click **Run Now**.</span></span>

    ![작업 정의 트리거](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="5e680-173">Hello 작업 정의 선택 toorun 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="5e680-174">클릭 **실행 설정** toomodify이이 작업 실행에 대해 toochange 수도 있는 모든 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![작업 설정 실행](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="5e680-176">클릭 **확인** 클릭 하 고 **실행** toolaunch 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="5e680-177">toomonitor이 작업을 이동 toohello **작업** 프로그램 StorSimple 데이터 관리자의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![작업 목록 및 상태](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="5e680-179">Hello에 더하기 toomonitoring에서 **작업** 블레이드에서 있습니다도에서 수신할 수 hello 저장소 큐 StorSimple toohello 저장소 계정에서 파일을 이동 될 때마다 메시지가 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5e680-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e680-180">Next steps</span></span>

<span data-ttu-id="5e680-181">[.NET SDK toolaunch StorSimple Data Manager 작업을 사용 하 여](storsimple-data-manager-dotnet-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
