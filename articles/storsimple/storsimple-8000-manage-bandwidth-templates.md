---
title: "StorSimple 8000 시리즈의 대역폭 템플릿 관리 | Microsoft Docs"
description: "대역폭 소비를 제어할 수 있도록 StorSimple 대역폭 템플릿을 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 50d0a920bef097013feddc828d2c37133b9057b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="8f442-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 대역폭 템플릿 관리</span><span class="sxs-lookup"><span data-stu-id="8f442-103">Use the StorSimple Device Manager service to manage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="8f442-104">개요</span><span class="sxs-lookup"><span data-stu-id="8f442-104">Overview</span></span>

<span data-ttu-id="8f442-105">대역폭 템플릿을 사용하면 데이터를 StorSimple 장치에서 클라우드로 티어하도록 여러 시간의 일정에서 네트워크 대역폭 사용을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="8f442-106">일정을 제한하는 대역폭을 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="8f442-107">워크로드 네트워크 사용량에 따라 사용자 지정 대역폭 일정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="8f442-108">쉽고 원활한 방식으로 여러 장치에서 중앙 관리하고 일정을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="8f442-109">이 기능은 StorSimple 물리적 장치(모델 8100 및 8600)에 대해서만 사용할 수 있으며 StorSimple Cloud Appliance(모델 8010 및 8020)에 대해서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="the-bandwidth-templates-blade"></a><span data-ttu-id="8f442-110">대역폭 템플릿 블레이드</span><span class="sxs-lookup"><span data-stu-id="8f442-110">The Bandwidth templates blade</span></span>

<span data-ttu-id="8f442-111">**대역폭 템플릿** 블레이드에는 서비스에 대한 모든 대역폭 템플릿이 테이블 형식으로 표시되며 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-111">The **Bandwidth templates** blade has all the bandwidth templates for your service in a tabular format, and contains the following information:</span></span>

* <span data-ttu-id="8f442-112">**이름** – 만들어졌을 때 대역폭 템플릿에 할당된 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-112">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="8f442-113">**일정** – 주어진 대역폭 템플릿에 포함 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-113">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="8f442-114">**사용 볼륨** – 대역폭 템플릿을 사용하는 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-114">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="8f442-115">다음에서 대역폭 템플릿을 구성하는 데 도움이 되는 추가 정보를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* [<span data-ttu-id="8f442-116">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="8f442-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="8f442-117">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8f442-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="8f442-118">대역폭 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="8f442-118">Add a bandwidth template</span></span>

<span data-ttu-id="8f442-119">새 대역폭 템플릿을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="8f442-120">대역폭 템플릿을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="8f442-120">To add a bandwidth template</span></span>

1. <span data-ttu-id="8f442-121">StorSimple 장치 관리자 서비스로 이동한 후 **대역폭 템플릿**을 클릭하고 **+ 대역폭 템플릿 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-121">Go to your StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![+대역폭 템플릿 추가 클릭](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="8f442-123">**대역폭 템플릿 추가** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-123">In the **Add bandwidth template** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="8f442-124">대역폭 템플릿에 대한 고유 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="8f442-125">대역폭 일정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="8f442-126">일정을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="8f442-126">To create a schedule:</span></span>
   
        1. <span data-ttu-id="8f442-127">드롭다운 목록에서 일정에 대해 구성되는 **요일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-127">From the drop-down list, choose the **Days** of the week the schedule is configured for.</span></span> <span data-ttu-id="8f442-128">여러 요일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="8f442-129">**시작 시간**을 _hh:mm_ 형식으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="8f442-130">일정이 시작되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-130">This is when the schedule will begin.</span></span>

        3. <span data-ttu-id="8f442-131">**종료 시간**을 _hh:mm_ 형식으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="8f442-132">일정이 중지되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-132">This is when the schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="8f442-133">겹치는 일정은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="8f442-134">시작 및 종료 시간이 겹치는 경우 그에 대한 오류 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-134">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>

        4. <span data-ttu-id="8f442-135">**대역폭 속도**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-135">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="8f442-136">클라우드와 관련된 작업(업로드 및 다운로드 모두)에서 StorSimple가 사용하는 초당 메가 비트(Mbps)의 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-136">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="8f442-137">이 필드에 대해 1에서 1,000 사이의 숫자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![대역폭 일정 정의](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="8f442-139">완료될 때까지 위 단계를 반복하여 템플릿에 대해 여러 일정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-139">Repeat the above steps to define multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="8f442-140">**추가**를 클릭하여 대역폭 템플릿 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-140">Click **Add** to start creating a bandwidth template.</span></span> <span data-ttu-id="8f442-141">만든 템플릿이 대역폭 템플릿 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-141">The created template is added to the list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="8f442-142">대역폭 템플릿 편집</span><span class="sxs-lookup"><span data-stu-id="8f442-142">Edit a bandwidth template</span></span>

<span data-ttu-id="8f442-143">대역폭 템플릿을 편집하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-143">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="8f442-144">대역폭 템플릿을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="8f442-144">To edit a bandwidth template</span></span>

1. <span data-ttu-id="8f442-145">StorSimple 장치 관리자 서비스로 이동한 다음 **대역폭 템플릿**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-145">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="8f442-146">대역폭 템플릿 목록에서 삭제하려는 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-146">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="8f442-147">마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-147">Right-click and from the context menu, select **Delete**.</span></span>
3. <span data-ttu-id="8f442-148">확인하라는 메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="8f442-149">대역폭 템플릿이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-149">This should delete the bandwidth template.</span></span> 
4. <span data-ttu-id="8f442-150">삭제를 반영하도록 대역폭 템플릿 목록이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-150">The list of bandwidth templates updates to reflect the deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="8f442-151">편집한 일정이 수정하려는 대역폭 템플릿의 기존 일정과 겹치는 경우, 변경 내용을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-151">You cannot save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="8f442-152">대역폭 템플릿 삭제</span><span class="sxs-lookup"><span data-stu-id="8f442-152">Delete a bandwidth template</span></span>

<span data-ttu-id="8f442-153">대역폭 템플릿을 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-153">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="8f442-154">대역폭 템플릿을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="8f442-154">To delete a bandwidth template</span></span>

1. <span data-ttu-id="8f442-155">StorSimple 장치 관리자 서비스로 이동한 다음 **대역폭 템플릿**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-155">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="8f442-156">대역폭 템플릿 목록에서 삭제하려는 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-156">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="8f442-157">마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 삭제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-157">Right-click and from the context menu, select Delete.</span></span>
3. <span data-ttu-id="8f442-158">확인하라는 메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="8f442-159">대역폭 템플릿이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-159">This should delete the bandwidth template.</span></span>
4. <span data-ttu-id="8f442-160">삭제를 반영하도록 대역폭 템플릿 목록이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-160">The list of bandwidth templates updates to reflect the deletion.</span></span>

<span data-ttu-id="8f442-161">템플릿이 모든 볼륨에서 사용 중인 경우 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-161">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="8f442-162">템플릿이 사용 중임을 나타내는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-162">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="8f442-163">템플릿에 대한 모든 참조를 제거하도록 조언하는 오류 메시지 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-163">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="8f442-164">다른 템플릿을 사용하거나 사용자 지정 또는 무제한 대역폭 설정을 사용하도록 **볼륨 컨테이너** 페이지에 엑세스하고 이 템플릿을 사용하는 볼륨 컨테이너를 수정하여 템플릿에 대한 모든 참조를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-164">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="8f442-165">모든 참조를 제거한 경우 템플릿을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-165">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="8f442-166">기본 대역폭 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="8f442-166">Use a default bandwidth template</span></span>

<span data-ttu-id="8f442-167">기본 대역폭 템플릿이 제공되며 기본값으로 볼륨 컨테이너에서 사용되어 클라우드에 액세스할 때 대역폭 제어를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-167">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="8f442-168">기본 템플릿은 자신의 템플릿을 만드는 사용자를 위한 준비 참조로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-168">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="8f442-169">이 기본 템플릿의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-169">The details of this default template are:</span></span>

* <span data-ttu-id="8f442-170">**이름** – 무제한 저녁 시간 및 주말</span><span class="sxs-lookup"><span data-stu-id="8f442-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="8f442-171">**일정** – 오전 8시와 오후 5시 장치 시간 사이의 1Mbps의 대역폭 속도를 적용하는 월요일에서부터 금요일까지의 단일 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-171">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="8f442-172">대역폭은 그 주의 나머지 부분에 대해 무제한으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-172">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="8f442-173">기본 템플릿은 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-173">The default template can be edited.</span></span> <span data-ttu-id="8f442-174">이 템플릿의 사용(편집된 버전 포함)을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-174">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="8f442-175">지정된 시간에 시작되는 하루 종일 대역폭 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="8f442-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="8f442-176">지정된 시간에 시작하고 하루 종일 실행되는 일정을 만들려면 이 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-176">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="8f442-177">이 예제에서 일정은 아침에 오전 9시에 시작하고 다음 날 오전 9시까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-177">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="8f442-178">지정된 일정에 대한 시작 시간과 종료 시간 모두 동일한 24시간 일정에 포함 되어야 하며 여러 날에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-178">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="8f442-179">여러 날에 걸쳐 있는 대역폭 템플릿을 설정 해야하는 경우, 여러 일정을 사용해야 합니다(예에서와 같이) .</span><span class="sxs-lookup"><span data-stu-id="8f442-179">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="8f442-180">하루 종일 대역폭 템플릿을 만들려면</span><span class="sxs-lookup"><span data-stu-id="8f442-180">To create an all-day bandwidth template</span></span>

1. <span data-ttu-id="8f442-181">아침 오전 9시에 시작되고 자정 때까지 실행되는 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-181">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="8f442-182">다른 일정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-182">Add another schedule.</span></span> <span data-ttu-id="8f442-183">자정에서부터 오전 9시까지 두 번째 일정을 실행하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-183">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="8f442-184">대역폭 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-184">Save the bandwidth template.</span></span>

<span data-ttu-id="8f442-185">복합 일정은 선택한 시간에 시작되며 하루 종일 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-185">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="8f442-186">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="8f442-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="8f442-187">**Q**.</span><span class="sxs-lookup"><span data-stu-id="8f442-187">**Q**.</span></span> <span data-ttu-id="8f442-188">일정 사이에 있는 경우 대역폭 제어에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="8f442-188">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="8f442-189">(하나의 일정이 종료되고 다른 일정이 아직 시작되지 않았습니다.)</span><span class="sxs-lookup"><span data-stu-id="8f442-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="8f442-190">**A**.</span><span class="sxs-lookup"><span data-stu-id="8f442-190">**A**.</span></span> <span data-ttu-id="8f442-191">이러한 경우 적용되는 대역폭 제어는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="8f442-192">즉, 데이터를 클라우드로 티어링할 때 장치는 무제한 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-192">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="8f442-193">**Q**.</span><span class="sxs-lookup"><span data-stu-id="8f442-193">**Q**.</span></span> <span data-ttu-id="8f442-194">오프라인 장치에서 대역폭 템플릿을 수정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8f442-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="8f442-195">**A**.</span><span class="sxs-lookup"><span data-stu-id="8f442-195">**A**.</span></span> <span data-ttu-id="8f442-196">해당 장치가 오프라인 상태인 경우 볼륨 컨테이너에서 대역폭 템플릿을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-196">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="8f442-197">**Q**.</span><span class="sxs-lookup"><span data-stu-id="8f442-197">**Q**.</span></span> <span data-ttu-id="8f442-198">연결된 볼륨이 오프라인 상태인 경우 볼륨 컨테이너와 연결된 대역폭 템플릿을 편집할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8f442-198">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="8f442-199">**A**.</span><span class="sxs-lookup"><span data-stu-id="8f442-199">**A**.</span></span> <span data-ttu-id="8f442-200">볼륨이 오프라인 상태인 볼륨 컨테이너와 연결된 대역폭 템플릿을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="8f442-201">볼륨이 오프라인 상태인 경우, 장치에서 클라우드로 티어링된 데이터는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-201">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="8f442-202">**Q**.</span><span class="sxs-lookup"><span data-stu-id="8f442-202">**Q**.</span></span> <span data-ttu-id="8f442-203">기본 템플릿을 삭제할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8f442-203">Can you delete a default template?</span></span>

<span data-ttu-id="8f442-204">**A**.</span><span class="sxs-lookup"><span data-stu-id="8f442-204">**A**.</span></span> <span data-ttu-id="8f442-205">기본 템플릿을 삭제할 수 있지만 좋은 생각은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-205">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="8f442-206">편집된 버전을 포함하여 기본 템플릿의 사용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-206">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="8f442-207">추적 데이터가 분석되고 시간이 지나면서 기본 템플릿을 개선하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-207">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="8f442-208">**Q**.</span><span class="sxs-lookup"><span data-stu-id="8f442-208">**Q**.</span></span> <span data-ttu-id="8f442-209">대역폭 템플릿을 수정해야 하는지 어떻게 확인합니까?</span><span class="sxs-lookup"><span data-stu-id="8f442-209">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="8f442-210">**A**.</span><span class="sxs-lookup"><span data-stu-id="8f442-210">**A**.</span></span> <span data-ttu-id="8f442-211">대역폭 템플릿을 수정해야 하는 경우 중 하나는 네트워크 속도가 느려지거나 하루에 여러 번 억제됨이 보이기 시작하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-211">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="8f442-212">이 문제가 발생하면 I/O 성능 및 네트워크 처리량 차트를 보고 저장소 및 사용 네트워크를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-212">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="8f442-213">네트워크 처리량 데이터에서, 네트워크 병목 현상이 발생하는 시간 및 볼륨 컨테이너를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-213">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="8f442-214">클라우드로 데이터를 티어링하면 발생하는 경우(클라우드에 대한 장치에 대한 모든 볼륨 컨테이너의 경우 I/O 성능에서 이 정보를 가져오기), 볼륨 컨테이너와 연결 된 대역폭 템플릿을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-214">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="8f442-215">수정된 템플릿이 사용된 후, 중요한 대기 시간에 대해 다시 네트워크를 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-215">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="8f442-216">여전히 존재하는 경우 대역폭 템플릿을 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-216">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="8f442-217">**Q**.</span><span class="sxs-lookup"><span data-stu-id="8f442-217">**Q**.</span></span> <span data-ttu-id="8f442-218">내 장치의 여러 볼륨 컨테이너에 겹치는 일정이 있지만 다른 제한이 각각에 대해 적용되는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="8f442-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="8f442-219">**A**.</span><span class="sxs-lookup"><span data-stu-id="8f442-219">**A**.</span></span> <span data-ttu-id="8f442-220">3개의 볼륨 컨테이너가 있는 장치가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="8f442-221">이 컨테이너와 연관된 일정이 완전하게 겹칩니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-221">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="8f442-222">각각의 이 컨테이너에 대해, 사용된 대역폭 제한은 5, 10 및 15 Mbps 각각입니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-222">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="8f442-223">I/O가 동시에 이 모든 컨테이너에서 발생하면, 최소 3개 대역폭 제한이 적용됩니다. 이 경우, 나가는 I/O 요청으로 5Mbps는 동일한 큐를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-223">When I/O are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="8f442-224">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8f442-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="8f442-225">StorSimple 장치에 대해 이 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="8f442-226">다른 시간에 장치에서 네트워크 처리량을 제한하는 변수를 사용하도록 사용자 장치에 대역폭 템플릿을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-226">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="8f442-227">백업 일정을 함께 사용하면 이 대역폭 템플릿은 사용량이 가장 적을 때 클라우드 작업에 대해 효과적으로 추가 네트워크 대역폭을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="8f442-228">배포 및 필요한 복구 시간 목표(RTO)의 크기에 따라 특정 배포에 필요한 실제 대역폭을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-228">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f442-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f442-229">Next steps</span></span>

<span data-ttu-id="8f442-230">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f442-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

