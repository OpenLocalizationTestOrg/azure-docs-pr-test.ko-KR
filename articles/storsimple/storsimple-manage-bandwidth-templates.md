---
title: "StorSimple 대역폭 템플릿 관리 | Microsoft Docs"
description: "대역폭 소비를 제어할 수 있도록 StorSimple 대역폭 템플릿을 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: df3ae8bf775370432b3648459a7c942afe69fb17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="01934-103">StorSimple 관리자 서비스를 사용하여 StorSimple 대역폭 템플릿 관리</span><span class="sxs-lookup"><span data-stu-id="01934-103">Use the StorSimple Manager service to manage StorSimple bandwidth templates</span></span>
## <a name="overview"></a><span data-ttu-id="01934-104">개요</span><span class="sxs-lookup"><span data-stu-id="01934-104">Overview</span></span>
<span data-ttu-id="01934-105">대역폭 템플릿을 사용하면 데이터를 StorSimple 장치에서 클라우드로 티어하도록 여러 시간의 일정에서 네트워크 대역폭 사용을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="01934-106">일정을 제한하는 대역폭을 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="01934-107">워크로드 네트워크 사용량에 따라 사용자 지정 대역폭 일정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="01934-108">쉽고 원활한 방식으로 여러 장치에서 중앙 관리하고 일정을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="01934-109">이 기능은 가상 장치가 아닌 StorSimple 물리적 장치에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-109">This feature is available only for StorSimple physical devices and not for virtual devices.</span></span>
> 
> 

<span data-ttu-id="01934-110">서비스에 대한 모든 대역폭 템플릿은 테이블 형식으로 표시되며 다음 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-110">All the bandwidth templates for your service are displayed in a tabular format, and contain the following information:</span></span>

* <span data-ttu-id="01934-111">**이름** – 만들어졌을 때 대역폭 템플릿에 할당된 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-111">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="01934-112">**일정** – 주어진 대역폭 템플릿에 포함 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-112">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="01934-113">**사용 볼륨** – 대역폭 템플릿을 사용하는 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-113">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="01934-114">Azure 클래식 포털의 StorSimple Manager 서비스 **구성** 페이지를 사용하여 대역폭 템플릿을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-114">You use the StorSimple Manager service **Configure** page in the Azure classic portal to manage bandwidth templates.</span></span>

<span data-ttu-id="01934-115">다음에서 대역폭 템플릿을 구성하는 데 도움이 되는 추가 정보를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* <span data-ttu-id="01934-116">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="01934-116">Questions and answers about bandwidth templates</span></span>
* <span data-ttu-id="01934-117">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="01934-117">Best practices for bandwidth templates</span></span>

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="01934-118">대역폭 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="01934-118">Add a bandwidth template</span></span>
<span data-ttu-id="01934-119">새 대역폭 템플릿을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="01934-120">대역폭 템플릿을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="01934-120">To add a bandwidth template</span></span>
1. <span data-ttu-id="01934-121">StorSimple Manager 서비스 **구성** 페이지에서 **대역폭 템플릿 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-121">On the StorSimple Manager service **Configure** page, click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="01934-122">**대역폭 템플릿 추가/편집** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="01934-122">In the **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="01934-123">**템플릿** 드롭다운 목록에서 **새로 만들기**를 선택하여 새 대역폭 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-123">From the **Template** drop-down list, select **Create new** to add a new bandwidth template.</span></span>
   2. <span data-ttu-id="01934-124">대역폭 템플릿에 대한 고유 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-124">Specify a unique name for your bandwidth template.</span></span>
3. <span data-ttu-id="01934-125">**대역폭 일정**을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-125">Define a **Bandwidth Schedule**.</span></span> <span data-ttu-id="01934-126">일정을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="01934-126">To create a schedule:</span></span>
   
   1. <span data-ttu-id="01934-127">드롭다운 목록에서 일정에 대해 구성되는 요일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-127">From the drop-down list, choose the days of the week the schedule is configured for.</span></span> <span data-ttu-id="01934-128">목록에서 해당 일보다 앞에 있는 확인란을 선택하여 여러 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-128">You can select multiple days by selecting the check boxes located before the respective days in the list.</span></span>
   2. <span data-ttu-id="01934-129">하루 전체에 대해 일정이 적용되는 경우 **하루 종일** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-129">Select the **All Day** option if the schedule is enforced for the entire day.</span></span> <span data-ttu-id="01934-130">이 옵션을 선택하면 **시작 시간** 또는 **종료 시간**을 더 이상 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-130">When this option is checked, you can no longer specify a **Start Time** or an **End Time**.</span></span> <span data-ttu-id="01934-131">일정은 오전 12시에서 오후 11시 59분에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-131">The schedule runs from 12:00 AM to 11:59 PM.</span></span>
   3. <span data-ttu-id="01934-132">드롭다운 목록에서 **시작 시간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-132">From the drop-down list, select a **Start Time**.</span></span> <span data-ttu-id="01934-133">일정이 시작되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-133">This is when the schedule will begin.</span></span>
   4. <span data-ttu-id="01934-134">드롭다운 목록에서 **종료 시간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-134">From the drop-down list, select an **End Time**.</span></span> <span data-ttu-id="01934-135">일정이 중지되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-135">This is when the schedule will stop.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="01934-136">겹치는 일정은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-136">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="01934-137">시작 및 종료 시간이 겹치는 경우 그에 대한 오류 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-137">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>
      > 
      > 
   5. <span data-ttu-id="01934-138">**대역폭 속도**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-138">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="01934-139">클라우드와 관련된 작업(업로드 및 다운로드 모두)에서 StorSimple가 사용하는 초당 메가 비트(Mbps)의 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-139">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="01934-140">이 필드에 대해 1에서 1,000 사이의 숫자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-140">Supply a number between 1 and 1,000 for this field.</span></span>
   6. <span data-ttu-id="01934-141">확인 아이콘 ![확인 아이콘](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-141">Click the check icon ![Check icon](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png).</span></span> <span data-ttu-id="01934-142">사용자가 만든 템플릿이 서비스 **구성** 페이지의 대역폭 템플릿 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-142">The template that you have created will be added to the list of bandwidth templates on the service **Configure** page.</span></span>
      
      ![새 대역폭 템플릿 만들기](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. <span data-ttu-id="01934-144">페이지의 아래쪽에서 **저장**을 클릭한 다음 확인 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-144">Click **Save** at the bottom of the page and then click **Yes** when prompted for confirmation.</span></span> <span data-ttu-id="01934-145">변경한 구성 변경 내용이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-145">This will save the configuration changes that you have made.</span></span>

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="01934-146">대역폭 템플릿 편집</span><span class="sxs-lookup"><span data-stu-id="01934-146">Edit a bandwidth template</span></span>
<span data-ttu-id="01934-147">대역폭 템플릿을 편집하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-147">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="01934-148">대역폭 템플릿을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="01934-148">To edit a bandwidth template</span></span>
1. <span data-ttu-id="01934-149">**대역폭 템플릿 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-149">Click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="01934-150">**대역폭 템플릿 추가/편집** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="01934-150">In the **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="01934-151">**템플릿** 드롭다운 목록에서 수정할 기존 대역폭 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-151">From the **Template** drop-down list, choose an existing bandwidth template that you want to modify.</span></span>
   2. <span data-ttu-id="01934-152">변경을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-152">Complete your changes.</span></span> <span data-ttu-id="01934-153">(기존 설정을 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="01934-153">(You can modify any of the existing settings.)</span></span>
   3. <span data-ttu-id="01934-154">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="01934-154">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)<span data-ttu-id="01934-156">을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-156">.</span></span> <span data-ttu-id="01934-157">서비스 구성 페이지의 대역폭 템플릿 목록에 수정된 템플릿이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-157">You will see the modified template in the list of bandwidth templates on the service Configure page.</span></span>
3. <span data-ttu-id="01934-158">변경 내용을 저장하려면 페이지 아래쪽에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-158">To save your changes, click **Save** at the bottom of the page.</span></span> <span data-ttu-id="01934-159">페이지의 아래쪽에서 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-159">Click **Yes** when prompted for confirmation.</span></span>

> [!NOTE]
> <span data-ttu-id="01934-160">편집한 일정이 수정하려는 대역폭 템플릿의 기존 일정와 겹치는 경우, 변경 내용을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-160">You will not be allowed to save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>
> 
> 

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="01934-161">대역폭 템플릿 삭제</span><span class="sxs-lookup"><span data-stu-id="01934-161">Delete a bandwidth template</span></span>
<span data-ttu-id="01934-162">대역폭 템플릿을 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-162">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="01934-163">대역폭 템플릿을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="01934-163">To delete a bandwidth template</span></span>
1. <span data-ttu-id="01934-164">서비스에 대한 대역폭 템플릿의 테이블 형식 목록에서 삭제할 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-164">In the tabular list of the bandwidth templates for your service, select the template that you wish to delete.</span></span> <span data-ttu-id="01934-165">삭제 아이콘(**x**)이 선택한 템플릿의 맨 오른쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-165">A delete icon (**x**) will appear to the extreme right of the selected template.</span></span> <span data-ttu-id="01934-166">**x** 아이콘을 클릭하여 자격 증명을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-166">Click the **x** icon to delete the template.</span></span>
2. <span data-ttu-id="01934-167">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-167">You will be prompted for confirmation.</span></span> <span data-ttu-id="01934-168">**확인** 을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-168">Click **OK** to proceed.</span></span>

<span data-ttu-id="01934-169">템플릿이 모든 볼륨에서 사용 중인 경우 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-169">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="01934-170">템플릿이 사용 중임을 나타내는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-170">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="01934-171">템플릿에 대한 모든 참조를 제거하도록 조언하는 오류 메시지 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-171">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="01934-172">다른 템플릿을 사용하거나 사용자 지정 또는 무제한 대역폭 설정을 사용하도록 **볼륨 컨테이너** 페이지에 엑세스하고 이 템플릿을 사용하는 볼륨 컨테이너를 수정하여 템플릿에 대한 모든 참조를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-172">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="01934-173">모든 참조를 제거한 경우 템플릿을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-173">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="01934-174">기본 대역폭 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="01934-174">Use a default bandwidth template</span></span>
<span data-ttu-id="01934-175">기본 대역폭 템플릿이 제공되며 기본값으로 볼륨 컨테이너에서 사용되어 클라우드에 액세스할 때 대역폭 제어를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-175">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="01934-176">기본 템플릿은 자신의 템플릿을 만드는 사용자를 위한 준비 참조로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-176">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="01934-177">이 기본 템플릿의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-177">The details of this default template are:</span></span>

* <span data-ttu-id="01934-178">**이름** – 무제한 저녁 시간 및 주말</span><span class="sxs-lookup"><span data-stu-id="01934-178">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="01934-179">**일정** – 오전 8시와 오후 5시 장치 시간 사이의 1Mbps의 대역폭 속도를 적용하는 월요일에서부터 금요일까지의 단일 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-179">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="01934-180">대역폭은 그 주의 나머지 부분에 대해 무제한으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-180">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="01934-181">기본 템플릿은 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-181">The default template can be edited.</span></span> <span data-ttu-id="01934-182">이 템플릿의 사용(편집된 버전 포함)을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-182">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="01934-183">지정된 시간에 시작되는 하루 종일 대역폭 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="01934-183">Create an all-day bandwidth template that starts at a specified time</span></span>
<span data-ttu-id="01934-184">지정된 시간에 시작하고 하루 종일 실행되는 일정을 만들려면 이 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="01934-184">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="01934-185">이 예제에서 일정은 아침에 오전 9시에 시작하고 다음 날 오전 9시까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-185">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="01934-186">지정된 일정에 대한 시작 시간과 종료 시간 모두 동일한 24시간 일정에 포함 되어야 하며 여러 날에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-186">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="01934-187">여러 날에 걸쳐 있는 대역폭 템플릿을 설정 해야하는 경우, 여러 일정을 사용해야 합니다(예에서와 같이) .</span><span class="sxs-lookup"><span data-stu-id="01934-187">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="01934-188">하루 종일 대역폭 템플릿을 만들려면</span><span class="sxs-lookup"><span data-stu-id="01934-188">To create an all-day bandwidth template</span></span>
1. <span data-ttu-id="01934-189">아침 오전 9시에 시작되고 자정 때까지 실행되는 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01934-189">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="01934-190">다른 일정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-190">Add another schedule.</span></span> <span data-ttu-id="01934-191">자정에서부터 오전 9시까지 두 번째 일정을 실행하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-191">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="01934-192">대역폭 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-192">Save the bandwidth template.</span></span>

<span data-ttu-id="01934-193">복합 일정은 선택한 시간에 시작되며 하루 종일 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-193">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="01934-194">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="01934-194">Questions and answers about bandwidth templates</span></span>
<span data-ttu-id="01934-195">**Q**.</span><span class="sxs-lookup"><span data-stu-id="01934-195">**Q**.</span></span> <span data-ttu-id="01934-196">일정 사이에 있는 경우 대역폭 제어에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="01934-196">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="01934-197">(하나의 일정이 종료되고 다른 일정이 아직 시작되지 않았습니다.)</span><span class="sxs-lookup"><span data-stu-id="01934-197">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="01934-198">**A**.</span><span class="sxs-lookup"><span data-stu-id="01934-198">**A**.</span></span> <span data-ttu-id="01934-199">이러한 경우 적용되는 대역폭 제어는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-199">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="01934-200">즉, 데이터를 클라우드로 티어링할 때 장치는 무제한 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-200">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="01934-201">**Q**.</span><span class="sxs-lookup"><span data-stu-id="01934-201">**Q**.</span></span> <span data-ttu-id="01934-202">오프라인 장치에서 대역폭 템플릿을 수정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="01934-202">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="01934-203">**A**.</span><span class="sxs-lookup"><span data-stu-id="01934-203">**A**.</span></span> <span data-ttu-id="01934-204">해당 장치가 오프라인 상태인 경우 볼륨 컨테이너에서 대역폭 템플릿을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-204">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="01934-205">**Q**.</span><span class="sxs-lookup"><span data-stu-id="01934-205">**Q**.</span></span> <span data-ttu-id="01934-206">연결된 볼륨이 오프라인 상태인 경우 볼륨 컨테이너와 연결된 대역폭 템플릿을 편집할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="01934-206">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="01934-207">**A**.</span><span class="sxs-lookup"><span data-stu-id="01934-207">**A**.</span></span> <span data-ttu-id="01934-208">볼륨이 오프라인 상태인 볼륨 컨테이너와 연결된 대역폭 템플릿을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-208">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="01934-209">볼륨이 오프라인 상태인 경우, 장치에서 클라우드로 티어링된 데이터는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-209">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="01934-210">**Q**.</span><span class="sxs-lookup"><span data-stu-id="01934-210">**Q**.</span></span> <span data-ttu-id="01934-211">기본 템플릿을 삭제할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="01934-211">Can you delete a default template?</span></span>

<span data-ttu-id="01934-212">**A**.</span><span class="sxs-lookup"><span data-stu-id="01934-212">**A**.</span></span> <span data-ttu-id="01934-213">기본 템플릿을 삭제할 수 있지만 좋은 생각은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="01934-213">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="01934-214">편집된 버전을 포함하여 기본 템플릿의 사용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-214">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="01934-215">추적 데이터가 분석되고 시간이 지나면서 기본 템플릿을 개선하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-215">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="01934-216">**Q**.</span><span class="sxs-lookup"><span data-stu-id="01934-216">**Q**.</span></span> <span data-ttu-id="01934-217">대역폭 템플릿을 수정해야 하는지 어떻게 확인합니까?</span><span class="sxs-lookup"><span data-stu-id="01934-217">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="01934-218">**A**.</span><span class="sxs-lookup"><span data-stu-id="01934-218">**A**.</span></span> <span data-ttu-id="01934-219">대역폭 템플릿을 수정해야 하는 경우 중 하나는 네트워크 속도가 느려지거나 하루에 여러 번 억제됨이 보이기 시작하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-219">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="01934-220">이 문제가 발생하면 I/O 성능 및 네트워크 처리량 차트를 보고 저장소 및 사용 네트워크를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-220">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="01934-221">네트워크 처리량 데이터에서, 네트워크 병목 현상이 발생하는 시간 및 볼륨 컨테이너를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-221">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="01934-222">클라우드로 데이터를 티어링하면 발생하는 경우(클라우드에 대한 장치에 대한 모든 볼륨 컨테이너의 경우 I/O 성능에서 이 정보를 가져오기), 볼륨 컨테이너와 연결 된 대역폭 템플릿을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-222">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="01934-223">수정된 템플릿이 사용된 후, 중요한 대기 시간에 대해 다시 네트워크를 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-223">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="01934-224">여전히 존재하는 경우 대역폭 템플릿을 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-224">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="01934-225">**Q**.</span><span class="sxs-lookup"><span data-stu-id="01934-225">**Q**.</span></span> <span data-ttu-id="01934-226">내 장치의 여러 볼륨 컨테이너에 겹치는 일정이 있지만 다른 제한이 각각에 대해 적용되는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="01934-226">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="01934-227">**A**.</span><span class="sxs-lookup"><span data-stu-id="01934-227">**A**.</span></span> <span data-ttu-id="01934-228">3개의 볼륨 컨테이너가 있는 장치가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-228">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="01934-229">이 컨테이너와 연관된 일정이 완전하게 겹칩니다.</span><span class="sxs-lookup"><span data-stu-id="01934-229">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="01934-230">각각의 이 컨테이너에 대해, 사용된 대역폭 제한은 5, 10 및 15 Mbps 각각입니다.</span><span class="sxs-lookup"><span data-stu-id="01934-230">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="01934-231">I/O가 동시에 이 모든 컨테이너에서 발생하면, 최소 3개 대역폭 제한이 적용됩니다. 이 경우, 나가는 I/O 요청으로 5Mbps는 동일한 큐를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-231">When I/Os are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="01934-232">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="01934-232">Best practices for bandwidth templates</span></span>
<span data-ttu-id="01934-233">StorSimple 장치에 대해 이 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="01934-233">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="01934-234">다른 시간에 장치에서 네트워크 처리량을 제한하는 변수를 사용하도록 사용자 장치에 대역폭 템플릿을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-234">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="01934-235">백업 일정을 함께 사용하면 이 대역폭 템플릿은 사용량이 가장 적을 때 클라우드 작업에 대해 효과적으로 추가 네트워크 대역폭을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01934-235">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="01934-236">배포 및 필요한 복구 시간 목표(RTO)의 크기에 따라 특정 배포에 필요한 실제 대역폭을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="01934-236">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01934-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01934-237">Next steps</span></span>
<span data-ttu-id="01934-238">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="01934-238">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

