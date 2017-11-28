---
title: "Microsoft Azure StorSimple 데이터 관리자 UI | Microsoft Docs"
description: "StorSimple 데이터 관리자 서비스 UI를 사용하는 방법 설명(비공개 미리 보기)"
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
ms.openlocfilehash: 53a8599df2c647613122cd791b680e2e658586b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-using-the-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="549a7-103">StorSimple 데이터 관리자 서비스 UI를 사용하여 관리(비공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="549a7-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="549a7-104">이 문서에서는 StorSimple 데이터 관리자 UI를 사용하여 StorSimple 8000 시리즈 장치에 있는 데이터에 대한 데이터 변환을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="549a7-105">그러면 Azure Media Services, Azure HDInsight, Azure Machine Learning 및 Azure Search와 같은 다른 Azure 서비스에서 변환된 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="549a7-106">StorSimple 데이터 변환 사용</span><span class="sxs-lookup"><span data-stu-id="549a7-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="549a7-107">StorSimple 데이터 관리자는 데이터 변환을 인스턴스화할 수 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="549a7-108">데이터 변환 서비스를 사용하면 데이터를 StorSimple 온-프레미스 장치에서 Azure Storage의 Blob로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span></span> <span data-ttu-id="549a7-109">따라서 워크플로에서 저장소 계정으로 이동하려는 StorSimple 장치 및 대상 데이터에 대한 세부 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="549a7-110">StorSimple 데이터 관리자 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="549a7-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="549a7-111">StorSimple 데이터 관리자 서비스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="549a7-112">StorSimple 데이터 관리자 서비스를 만들려면 [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="549a7-113">**+** 아이콘을 클릭하고 StorSimple 데이터 관리자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-113">Click the **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="549a7-114">StorSimple 데이터 관리자 서비스를 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="549a7-115">이 서비스를 만들기 위해 구독을 사용하도록 설정하면 다음 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-115">If your subscription is enabled for creating this service, you see the following blade.</span></span>

    ![StorSimple 데이터 관리자 리소스 만들기](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="549a7-117">입력 항목을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-117">Enter the inputs and click **Create**.</span></span> <span data-ttu-id="549a7-118">지정된 위치는 저장소 계정 및 StorSimple Manager 서비스를 저장한 위치여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="549a7-119">현재 미국 서부 및 유럽 서부에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="549a7-120">따라서 StorSimple Manager 서비스, 데이터 관리자 서비스 및 연결된 저장소 계정은 모두 앞서 지원되는 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span></span> <span data-ttu-id="549a7-121">서비스를 만들려면 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-121">It takes about a minute to create the service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="549a7-122">데이터 변환 작업 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="549a7-122">Create a data transformation job definition</span></span>

<span data-ttu-id="549a7-123">StorSimple 데이터 관리자 서비스 내에서 데이터 변환 작업 정의를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="549a7-124">작업 정의는 저장소 계정에 이동하는 데 관심이 있는 데이터의 세부 정보를 네이티브 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span></span> 

<span data-ttu-id="549a7-125">새 데이터 변환 작업 정의를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-125">Perform the following steps to create a new data transformation job definition.</span></span>

1.  <span data-ttu-id="549a7-126">만든 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-126">Navigate to the service that you created.</span></span> <span data-ttu-id="549a7-127">**+작업 정의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-127">Click **+ Job Definition**.</span></span>

    ![+작업 정의 클릭](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="549a7-129">새 작업 정의 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-129">The new job definition blade opens up.</span></span> <span data-ttu-id="549a7-130">작업 정의에 이름을 지정하고 **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="549a7-131">**구성 데이터 원본** 블레이드에서 StorSimple 장치 및 대상 데이터에 대한 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span></span>

    ![작업 정의 만들기](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="549a7-133">새 데이터 관리자 서비스이기 때문에 데이터 리포지토리가 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="549a7-134">StorSimple Manager를 데이터 리포지토리로 추가하려면 데이터 리포지토리 드롭다운에서 **새로 추가**를 클릭한 다음에 **데이터 리포지토리 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="549a7-135">**StorSimple 8000 시리즈 관리자**를 리포지토리 유형으로 선택하고 **StorSimple Manager**의 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="549a7-136">**리소스 ID** 필드에 StorSimple Manager의 등록 키에 있는 **:** 앞의 숫자를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span></span>

    ![데이터 원본 만들기](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="549a7-138">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-138">Click **OK** when done.</span></span> <span data-ttu-id="549a7-139">이렇게 하면 데이터 리포지토리를 절약하고 이러한 매개 변수를 다시 입력하지 않고 다른 작업 정의에서 이 StorSimple Manager를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="549a7-140">**확인**을 클릭한 후에 StorSimple Manager가 드롭다운 목록에 표시되는 데 몇 초 정도가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span></span>

6.  <span data-ttu-id="549a7-141">**구성 데이터 원본** 블레이드에서 관련 데이터를 가진 장치 이름 및 볼륨 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="549a7-142">**필터** 하위 섹션에서 관련 데이터를 포함하는 루트 디렉터리를 입력합니다(이 필드는 `\`으로 시작해야 함).</span><span class="sxs-lookup"><span data-stu-id="549a7-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="549a7-143">여기에서 파일 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="549a7-144">데이터 변환 서비스는 스냅숏을 통해 Azure까지 푸시되는 데이터에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="549a7-145">이 작업을 실행할 때 최신 데이터에서 작동하도록 작업을 실행할 때마다 백업을 사용하거나 보관된 데이터를 사용하는 경우 클라우드에서 최신 기존 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    ![새 데이터 원본 세부 정보](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="549a7-147">다음으로 대상 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-147">Next, the Target settings need to be configured.</span></span> <span data-ttu-id="549a7-148">지원되는 대상에는 Azure Storage 계정 및 Azure Media Services 계정이라는 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="549a7-149">저장소 계정을 선택하여 해당 계정에서 Blob에 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-149">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="549a7-150">Media Services 계정을 선택하여 해당 계정에서 자산에 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-150">Choose media services account to put files into assets in that account.</span></span> <span data-ttu-id="549a7-151">다시 리포지토리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-151">Again, we need to add a repository.</span></span> <span data-ttu-id="549a7-152">드롭다운 목록에서 **새로 추가** 및 **설정 구성** 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-152">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![데이터 싱크 만들기](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="549a7-154">여기에서 추가하려는 리포지토리의 유형 및 리포지토리와 관련된 다른 매개 변수 유형을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span></span> <span data-ttu-id="549a7-155">두 경우 모두 저장소 큐는 작업이 실행될 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-155">In both cases, a storage queue is created when the job runs.</span></span> <span data-ttu-id="549a7-156">이 큐는 준비가 완료된 변환 Blob에 대한 메시지로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="549a7-157">이 큐의 이름은 작업 정의의 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-157">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="549a7-158">**Media Services**를 리포지토리 유형으로 선택하는 경우 큐가 만들어질 저장소 계정 자격 증명을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span></span>

    ![새 데이터 싱크 세부 정보](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="549a7-160">몇 초 정도 걸리는 작업인 데이터 리포지토리를 추가한 후에 **대상 계정 이름**의 드롭다운에서 리포지토리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span></span>  <span data-ttu-id="549a7-161">필요한 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-161">Choose the target that you need.</span></span>

12. <span data-ttu-id="549a7-162">**확인**을 클릭하여 작업 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-162">Click **OK** to create the job definition.</span></span> <span data-ttu-id="549a7-163">이제 작업 정의가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-163">Your job definition is now set up.</span></span> <span data-ttu-id="549a7-164">UI를 통해 이 작업 정의를 여러 번 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-164">You can use this job definition multiple times via the UI.</span></span>

    ![새 작업 정의 추가](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-the-job-definition"></a><span data-ttu-id="549a7-166">작업 정의 실행</span><span class="sxs-lookup"><span data-stu-id="549a7-166">Run the job definition</span></span>

<span data-ttu-id="549a7-167">StorSimple에서 작업 정의에 지정된 저장소 계정으로 데이터를 이동할 때마다 해당 데이터를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span></span> <span data-ttu-id="549a7-168">작업을 호출할 때마다 매개 변수를 변경하는 유연성이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-168">There is some flexibility in changing the parameters every time you invoke the job.</span></span> <span data-ttu-id="549a7-169">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-169">The steps are as follows:</span></span>

1. <span data-ttu-id="549a7-170">StorSimple 데이터 관리자 서비스를 선택한 다음 **모니터링**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span></span> <span data-ttu-id="549a7-171">**지금 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-171">Click **Run Now**.</span></span>

    ![작업 정의 트리거](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="549a7-173">실행하려는 작업 정의를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-173">Choose the job definition that you want to run.</span></span> <span data-ttu-id="549a7-174">**실행 설정**을 클릭하여 이 작업 실행에 대해 변경하려는 모든 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span>

    ![작업 설정 실행](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="549a7-176">**확인**을 클릭한 다음 **실행**을 클릭하여 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-176">Click **OK** and then click **Run** to launch your job.</span></span> <span data-ttu-id="549a7-177">이 작업을 모니터링하려면 StorSimple 데이터 관리자에서 **작업** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span></span>

    ![작업 목록 및 상태](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="549a7-179">또한 **작업** 블레이드의 모니터링 외에도 StorSimple에서 저장소 계정으로 파일을 이동할 때마다 메시지가 추가되는 저장소 큐에 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="549a7-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="549a7-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="549a7-180">Next steps</span></span>

<span data-ttu-id="549a7-181">[.NET SDK를 사용하여 StorSimple 데이터 관리자 작업을 시작합니다](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="549a7-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>