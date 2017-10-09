---
title: "Azure 데이터 레이크 저장소에 이벤트 허브에서 aaaCapture 데이터 | Microsoft Docs"
description: "이벤트 허브에서 사용 하 여 Azure 데이터 레이크 저장소 toocapture 데이터"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="a1f08-103">이벤트 허브에서 사용 하 여 Azure 데이터 레이크 저장소 toocapture 데이터</span><span class="sxs-lookup"><span data-stu-id="a1f08-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="a1f08-104">Azure 데이터 레이크 저장소 toocapture 데이터 toouse Azure 이벤트 허브에서 수신 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1f08-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a1f08-105">Prerequisites</span></span>

* <span data-ttu-id="a1f08-106">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="a1f08-106">**An Azure subscription**.</span></span> <span data-ttu-id="a1f08-107">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1f08-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a1f08-108">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="a1f08-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="a1f08-109">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="a1f08-110">**Event Hubs 네임스페이스**.</span><span class="sxs-lookup"><span data-stu-id="a1f08-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="a1f08-111">자세한 내용은 [Event Hubs 네임스페이스 만들기](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1f08-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="a1f08-112">Hello 데이터 레이크 저장소 계정 및 hello 이벤트 허브 네임 스페이스에에서 있어야 hello 동일한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a1f08-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="a1f08-113">TooEvent 허브 사용 권한 할당</span><span class="sxs-lookup"><span data-stu-id="a1f08-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="a1f08-114">이 섹션에서는 이벤트 허브에서 toocapture hello 데이터 hello 계정 내에서 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="a1f08-115">또한 권한을 할당할 있습니다 tooEvent 허브 데이터 레이크 저장소 계정으로 데이터를 쓸 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="a1f08-116">이벤트 허브에서 toocapture 데이터 및 클릭 hello 데이터 레이크 저장소 계정 열기 **데이터 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="a1f08-117">![Data Lake Store 데이터 탐색기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store 데이터 탐색기")</span><span class="sxs-lookup"><span data-stu-id="a1f08-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="a1f08-118">클릭 **새 폴더** toocapture hello 데이터를 원하는 폴더에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="a1f08-119">![Data Lake Store에 새 폴더 만들기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Data Lake Store에 새 폴더 만들기")</span><span class="sxs-lookup"><span data-stu-id="a1f08-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="a1f08-120">Hello 데이터 레이크 저장소의 hello 루트에서 사용 권한을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="a1f08-121">a.</span><span class="sxs-lookup"><span data-stu-id="a1f08-121">a.</span></span> <span data-ttu-id="a1f08-122">클릭 **데이터 탐색기**hello 루트 hello Data Lake 저장소 계정에 선택한 다음 클릭 **액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="a1f08-123">![Data Lake Store 루트에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Data Lake Store 루트에 대한 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a1f08-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="a1f08-124">b.</span><span class="sxs-lookup"><span data-stu-id="a1f08-124">b.</span></span> <span data-ttu-id="a1f08-125">**액세스** 아래에서 **추가**를 클릭하고 **사용자 또는 그룹 선택**을 클릭한 후 `Microsoft.EventHubs`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="a1f08-126">![Data Lake Store 루트에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store 루트에 대한 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a1f08-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="a1f08-127">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-127">Click **Select**.</span></span>

    <span data-ttu-id="a1f08-128">c.</span><span class="sxs-lookup"><span data-stu-id="a1f08-128">c.</span></span> <span data-ttu-id="a1f08-129">**권한 할당**에서 **권한 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="a1f08-130">설정 **권한을** 너무**Execute**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="a1f08-131">설정 **추가할** 너무**이 폴더와 모든 자식**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="a1f08-132">설정 **로 추가** 너무**액세스 권한 항목 및 기본 권한 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="a1f08-133">![Data Lake Store 루트에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Data Lake Store 루트에 대한 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a1f08-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="a1f08-134">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-134">Click **OK**.</span></span>

4. <span data-ttu-id="a1f08-135">Toocapture 데이터 Data Lake 저장소 계정에서 hello 폴더에 대 한 권한을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="a1f08-136">a.</span><span class="sxs-lookup"><span data-stu-id="a1f08-136">a.</span></span> <span data-ttu-id="a1f08-137">클릭 **데이터 탐색기**hello Data Lake 저장소 계정에서에서 hello 폴더를 선택 하 고 클릭 한 다음, **액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="a1f08-138">![Data Lake Store 폴더에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Data Lake Store 폴더에 대한 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a1f08-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="a1f08-139">b.</span><span class="sxs-lookup"><span data-stu-id="a1f08-139">b.</span></span> <span data-ttu-id="a1f08-140">**액세스** 아래에서 **추가**를 클릭하고 **사용자 또는 그룹 선택**을 클릭한 후 `Microsoft.EventHubs`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="a1f08-141">![Data Lake Store 폴더에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store 폴더에 대한 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a1f08-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="a1f08-142">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-142">Click **Select**.</span></span>

    <span data-ttu-id="a1f08-143">c.</span><span class="sxs-lookup"><span data-stu-id="a1f08-143">c.</span></span> <span data-ttu-id="a1f08-144">**권한 할당**에서 **권한 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="a1f08-145">설정 **권한을** 너무**읽기, 쓰기,** 및 **Execute**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="a1f08-146">설정 **추가할** 너무**이 폴더와 모든 자식**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="a1f08-147">마지막으로, 설정 **로 추가** 너무**액세스 권한 항목 및 기본 권한 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="a1f08-148">![Data Lake Store 폴더에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Data Lake Store 폴더에 대한 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a1f08-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="a1f08-149">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="a1f08-150">이벤트 허브 toocapture 데이터 tooData 레이크 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="a1f08-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="a1f08-151">이 섹션에서는 Event Hubs 네임스페이스 내에 Event Hubs를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="a1f08-152">Hello 이벤트 허브 toocapture 데이터 tooan Azure 데이터 레이크 저장소 계정을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="a1f08-153">이 섹션에서는 Event Hubs 네임스페이스를 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="a1f08-154">Hello에서 **개요** 창의 hello 이벤트 허브 네임 스페이스의 클릭 **+ 이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="a1f08-155">![이벤트 허브 만들기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "이벤트 허브 만들기")</span><span class="sxs-lookup"><span data-stu-id="a1f08-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="a1f08-156">Hello 다음 tooconfigure 이벤트 허브 toocapture 데이터 tooData 레이크 저장소 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="a1f08-157">![이벤트 허브 만들기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "이벤트 허브 만들기")</span><span class="sxs-lookup"><span data-stu-id="a1f08-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="a1f08-158">a.</span><span class="sxs-lookup"><span data-stu-id="a1f08-158">a.</span></span> <span data-ttu-id="a1f08-159">이벤트 허브 hello에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="a1f08-160">b.</span><span class="sxs-lookup"><span data-stu-id="a1f08-160">b.</span></span> <span data-ttu-id="a1f08-161">이 자습서에 대 한 설정 **파티션 수** 및 **메시지 보존** toohello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="a1f08-162">c.</span><span class="sxs-lookup"><span data-stu-id="a1f08-162">c.</span></span> <span data-ttu-id="a1f08-163">설정 **캡처** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="a1f08-164">집합 hello **시간 창** (얼마나 자주 toocapture) 및 **크기 창** (데이터 크기 toocapture).</span><span class="sxs-lookup"><span data-stu-id="a1f08-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="a1f08-165">d.</span><span class="sxs-lookup"><span data-stu-id="a1f08-165">d.</span></span> <span data-ttu-id="a1f08-166">에 대 한 **캡처 공급자**선택, **Azure 데이터 레이크 저장소** hello 선택 hello 앞에서 만든 데이터 레이크 저장소 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="a1f08-167">에 대 한 **데이터 레이크 경로**, hello Data Lake 저장소 계정에서에서 만든 hello 폴더의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="a1f08-168">Tooprovide hello 상대 경로 toohello 폴더를 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="a1f08-169">e.</span><span class="sxs-lookup"><span data-stu-id="a1f08-169">e.</span></span> <span data-ttu-id="a1f08-170">Hello 둡니다 **샘플 캡처 파일 이름 형식을** toohello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="a1f08-171">이 옵션은 hello 캡처 폴더 아래에 생성 된 hello 폴더 구조를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="a1f08-172">f.</span><span class="sxs-lookup"><span data-stu-id="a1f08-172">f.</span></span> <span data-ttu-id="a1f08-173">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="a1f08-174">테스트 hello 설정</span><span class="sxs-lookup"><span data-stu-id="a1f08-174">Test hello setup</span></span>

<span data-ttu-id="a1f08-175">이제 데이터 toohello Azure 이벤트 허브를 전송 하 여 hello 솔루션을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="a1f08-176">Hello 지침에 따라 [tooAzure 이벤트 허브 이벤트를 보내는](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="a1f08-177">Hello 데이터를 보내기 시작 되 면 hello 데이터가 표시 Data Lake 저장소에 반영 지정한 hello 폴더 구조를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="a1f08-178">예를 들어 hello 스크린 샷 데이터 레이크 저장소의 뒤에 표시 된 대로 폴더 구조를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="a1f08-179">![Data Lake Store의 샘플 EventHub 데이터](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store의 샘플 EventHub 데이터")</span><span class="sxs-lookup"><span data-stu-id="a1f08-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="a1f08-180">이벤트 허브로 들어오는 메시지가 없는 경우에 이벤트 허브 hello Data Lake 저장소 계정에만 hello 헤더를 사용 하 여 빈 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="a1f08-181">hello이 파일은 hello에 동일한 사용자가 제공한 hello 이벤트 허브를 만드는 동안 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="a1f08-182">Data Lake 저장소의 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="a1f08-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="a1f08-183">데이터 레이크 저장소의 hello 데이터를 tooprocess 및 수치 연산 hello 데이터 분석 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="a1f08-184">참조 [USQL Avro 예제](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) 방법은 toodo이 Azure 데이터 레이크 분석을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1f08-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="a1f08-185">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a1f08-185">See also</span></span>
* [<span data-ttu-id="a1f08-186">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="a1f08-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a1f08-187">Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="a1f08-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
