---
title: "aaaManage StorSimple 대역폭 템플릿을 | Microsoft Docs"
description: "설명 방법을 toomanage StorSimple 대역폭 템플릿을 toocontrol 대역폭 사용을 허용 합니다."
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
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a><span data-ttu-id="df401-103">Hello StorSimple 관리자 서비스 toomanage StorSimple 대역폭 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="df401-103">Use hello StorSimple Manager service toomanage StorSimple bandwidth templates</span></span>
## <a name="overview"></a><span data-ttu-id="df401-104">개요</span><span class="sxs-lookup"><span data-stu-id="df401-104">Overview</span></span>
<span data-ttu-id="df401-105">대역폭 템플릿을 여러 시간에 일정이 tootier hello 데이터로 hello StorSimple 장치 toohello 클라우드 간에 tooconfigure 네트워크 대역폭 사용량 사용.</span><span class="sxs-lookup"><span data-stu-id="df401-105">Bandwidth templates allow you tooconfigure network bandwidth usage across multiple time-of-day schedules tootier hello data from hello StorSimple device toohello cloud.</span></span>

<span data-ttu-id="df401-106">일정을 제한하는 대역폭을 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="df401-107">Hello 작업 네트워크 사용량에 따라 사용자 지정 된 대역폭 일정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-107">Specify customized bandwidth schedules depending on hello workload network usages.</span></span>
* <span data-ttu-id="df401-108">관리를 중앙 집중화 하 고 쉽고 원활한 방식으로 여러 장치 간에 hello 일정을 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-108">Centralize management and reuse hello schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="df401-109">이 기능은 가상 장치가 아닌 StorSimple 물리적 장치에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-109">This feature is available only for StorSimple physical devices and not for virtual devices.</span></span>
> 
> 

<span data-ttu-id="df401-110">서비스에 대 한 모든 hello 대역폭 템플릿을 표 형식으로 표시 하며 hello 다음 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-110">All hello bandwidth templates for your service are displayed in a tabular format, and contain hello following information:</span></span>

* <span data-ttu-id="df401-111">**이름** -할당 된 고유한 이름 toohello 대역폭 템플릿을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="df401-111">**Name** – A unique name assigned toohello bandwidth template when it was created.</span></span>
* <span data-ttu-id="df401-112">**일정** – hello에 지정된 된 대역폭 템플릿에 포함 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-112">**Schedule** – hello number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="df401-113">**사용 하는** – hello hello 대역폭 템플릿을 사용 하 여 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-113">**Used by** – hello number of volumes using hello bandwidth templates.</span></span>

<span data-ttu-id="df401-114">Hello StorSimple Manager 서비스를 사용 하 여 **구성** hello Azure 클래식 포털 toomanage 대역폭 템플릿의 페이지.</span><span class="sxs-lookup"><span data-stu-id="df401-114">You use hello StorSimple Manager service **Configure** page in hello Azure classic portal toomanage bandwidth templates.</span></span>

<span data-ttu-id="df401-115">또한 toohelp 대역폭 템플릿을 구성 하는 추가 정보를 찾을 수 있습니다에:</span><span class="sxs-lookup"><span data-stu-id="df401-115">You can also find additional information toohelp configure bandwidth templates in:</span></span>

* <span data-ttu-id="df401-116">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="df401-116">Questions and answers about bandwidth templates</span></span>
* <span data-ttu-id="df401-117">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="df401-117">Best practices for bandwidth templates</span></span>

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="df401-118">대역폭 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="df401-118">Add a bandwidth template</span></span>
<span data-ttu-id="df401-119">Hello 단계 toocreate 새 대역폭 템플릿을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-119">Perform hello following steps toocreate a new bandwidth template.</span></span>

#### <a name="tooadd-a-bandwidth-template"></a><span data-ttu-id="df401-120">대역폭 템플릿 tooadd</span><span class="sxs-lookup"><span data-stu-id="df401-120">tooadd a bandwidth template</span></span>
1. <span data-ttu-id="df401-121">Hello StorSimple Manager 서비스에서 **구성** 페이지 **대역폭 템플릿 추가/편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-121">On hello StorSimple Manager service **Configure** page, click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="df401-122">Hello에 **대역폭 템플릿 추가/편집** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="df401-122">In hello **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="df401-123">Hello에서 **템플릿** 드롭 다운 목록 **새로 만들기** tooadd 새 대역폭 템플릿 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-123">From hello **Template** drop-down list, select **Create new** tooadd a new bandwidth template.</span></span>
   2. <span data-ttu-id="df401-124">대역폭 템플릿에 대한 고유 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-124">Specify a unique name for your bandwidth template.</span></span>
3. <span data-ttu-id="df401-125">**대역폭 일정**을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-125">Define a **Bandwidth Schedule**.</span></span> <span data-ttu-id="df401-126">toocreate 일정:</span><span class="sxs-lookup"><span data-stu-id="df401-126">toocreate a schedule:</span></span>
   
   1. <span data-ttu-id="df401-127">Hello 드롭 다운 목록에서에 대해 구성 된 hello 주 hello 일정의 hello 일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-127">From hello drop-down list, choose hello days of hello week hello schedule is configured for.</span></span> <span data-ttu-id="df401-128">Hello hello 목록에서 개별 요일 앞에 있는 hello 확인란을 선택 하 여 여러 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-128">You can select multiple days by selecting hello check boxes located before hello respective days in hello list.</span></span>
   2. <span data-ttu-id="df401-129">선택 hello **하루 종일** 옵션을 하루 종일 hello에 대 한 hello 일정이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-129">Select hello **All Day** option if hello schedule is enforced for hello entire day.</span></span> <span data-ttu-id="df401-130">이 옵션을 선택하면 **시작 시간** 또는 **종료 시간**을 더 이상 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-130">When this option is checked, you can no longer specify a **Start Time** or an **End Time**.</span></span> <span data-ttu-id="df401-131">오전 12시 too11에서 hello 일정이 실행: 59 PM입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-131">hello schedule runs from 12:00 AM too11:59 PM.</span></span>
   3. <span data-ttu-id="df401-132">Hello 드롭 다운 목록에서 선택 된 **시작 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-132">From hello drop-down list, select a **Start Time**.</span></span> <span data-ttu-id="df401-133">이 hello 일정 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-133">This is when hello schedule will begin.</span></span>
   4. <span data-ttu-id="df401-134">Hello 드롭 다운 목록에서 선택 된 **종료 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-134">From hello drop-down list, select an **End Time**.</span></span> <span data-ttu-id="df401-135">이 hello 일정을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-135">This is when hello schedule will stop.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="df401-136">겹치는 일정은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-136">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="df401-137">Hello 시작 및 종료 시간 발생 일정이 겹치면 오류 메시지 toothat 효과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-137">If hello start and end times will result in an overlapping schedule, you will see an error message toothat effect.</span></span>
      > 
      > 
   5. <span data-ttu-id="df401-138">Hello 지정 **대역폭 속도**합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-138">Specify hello **Bandwidth Rate**.</span></span> <span data-ttu-id="df401-139">이 hello 메가 비트 초당 대역폭 (Mbps) (업로드 및 다운로드) hello 클라우드 관련 작업에서 StorSimple 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-139">This is hello bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving hello cloud (both uploads and downloads).</span></span> <span data-ttu-id="df401-140">이 필드에 대해 1에서 1,000 사이의 숫자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-140">Supply a number between 1 and 1,000 for this field.</span></span>
   6. <span data-ttu-id="df401-141">Hello 확인 아이콘을 클릭 ![확인 아이콘](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-141">Click hello check icon ![Check icon](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png).</span></span> <span data-ttu-id="df401-142">사용자가 만든 hello 서식 파일에 추가 됩니다 toohello 대역폭 템플릿 목록이 hello 서비스 **구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="df401-142">hello template that you have created will be added toohello list of bandwidth templates on hello service **Configure** page.</span></span>
      
      ![새 대역폭 템플릿 만들기](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. <span data-ttu-id="df401-144">클릭 **저장** hello 클릭 하 고 hello 페이지 맨 아래에 **예** 확인 메시지가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-144">Click **Save** at hello bottom of hello page and then click **Yes** when prompted for confirmation.</span></span> <span data-ttu-id="df401-145">그러면 hello 구성 변경 내용이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-145">This will save hello configuration changes that you have made.</span></span>

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="df401-146">대역폭 템플릿 편집</span><span class="sxs-lookup"><span data-stu-id="df401-146">Edit a bandwidth template</span></span>
<span data-ttu-id="df401-147">Hello 단계 tooedit 대역폭 템플릿을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-147">Perform hello following steps tooedit a bandwidth template.</span></span>

### <a name="tooedit-a-bandwidth-template"></a><span data-ttu-id="df401-148">대역폭 템플릿 tooedit</span><span class="sxs-lookup"><span data-stu-id="df401-148">tooedit a bandwidth template</span></span>
1. <span data-ttu-id="df401-149">**대역폭 템플릿 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-149">Click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="df401-150">Hello에 **대역폭 템플릿 추가/편집** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="df401-150">In hello **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="df401-151">Hello에서 **템플릿** 드롭 다운 목록에서 기존 대역폭 toomodify 원하는 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-151">From hello **Template** drop-down list, choose an existing bandwidth template that you want toomodify.</span></span>
   2. <span data-ttu-id="df401-152">변경을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-152">Complete your changes.</span></span> <span data-ttu-id="df401-153">(수정 가능 hello 기존 설정을.)</span><span class="sxs-lookup"><span data-stu-id="df401-153">(You can modify any of hello existing settings.)</span></span>
   3. <span data-ttu-id="df401-154">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-154">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)<span data-ttu-id="df401-156">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-156">.</span></span> <span data-ttu-id="df401-157">Hello 서비스 구성 페이지에서 hello 수정 된 템플릿을 hello 대역폭 템플릿 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-157">You will see hello modified template in hello list of bandwidth templates on hello service Configure page.</span></span>
3. <span data-ttu-id="df401-158">변경 내용을 클릭 toosave **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-158">toosave your changes, click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="df401-159">페이지의 아래쪽에서 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-159">Click **Yes** when prompted for confirmation.</span></span>

> [!NOTE]
> <span data-ttu-id="df401-160">Hello 대역폭 서식 파일에 예약 된 기존 hello 편집한 일정이 겹치면 변경 내용을 수정 하는 toosave를 사용할 수 없으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-160">You will not be allowed toosave your changes if hello edited schedule overlaps with an existing schedule in hello bandwidth template that you are modifying.</span></span>
> 
> 

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="df401-161">대역폭 템플릿 삭제</span><span class="sxs-lookup"><span data-stu-id="df401-161">Delete a bandwidth template</span></span>
<span data-ttu-id="df401-162">Hello 단계 toodelete 대역폭 템플릿을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-162">Perform hello following steps toodelete a bandwidth template.</span></span>

#### <a name="toodelete-a-bandwidth-template"></a><span data-ttu-id="df401-163">대역폭 템플릿 toodelete</span><span class="sxs-lookup"><span data-stu-id="df401-163">toodelete a bandwidth template</span></span>
1. <span data-ttu-id="df401-164">서비스에 대 한 hello 대역폭 템플릿의 테이블 형식 목록 hello에서에서 원하는 toodelete hello 서식 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-164">In hello tabular list of hello bandwidth templates for your service, select hello template that you wish toodelete.</span></span> <span data-ttu-id="df401-165">삭제 아이콘 (**x**) toohello hello 선택한 템플릿의 오른쪽 끝에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-165">A delete icon (**x**) will appear toohello extreme right of hello selected template.</span></span> <span data-ttu-id="df401-166">Hello 클릭 **x** 아이콘 toodelete hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="df401-166">Click hello **x** icon toodelete hello template.</span></span>
2. <span data-ttu-id="df401-167">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-167">You will be prompted for confirmation.</span></span> <span data-ttu-id="df401-168">클릭 **확인** tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-168">Click **OK** tooproceed.</span></span>

<span data-ttu-id="df401-169">Hello 서식 파일은 볼륨에서 사용 중인 경우 있습니다 허용 되지 것입니다 toodelete 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-169">If hello template is in use by any volume(s), you will not be allowed toodelete it.</span></span> <span data-ttu-id="df401-170">사용 중인 해당 hello 템플릿은 나타내는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-170">You will see an error message indicating that hello template is in use.</span></span> <span data-ttu-id="df401-171">모든 hello 참조 toohello 서식 파일을 제거 해야 하 라는 오류 메시지 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-171">An error message dialog box will appear advising you that all hello references toohello template should be removed.</span></span>

<span data-ttu-id="df401-172">Hello에 액세스 하 여 모든 hello 참조 toohello 파일을 삭제할 수 **볼륨 컨테이너** 페이지 및 다른 서식 파일을 사용 하거나 사용자 지정 또는 무제한 대역폭을 사용 하 여이 템플릿을 사용 하는 hello 볼륨 컨테이너 수정 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-172">You can delete all hello references toohello template by accessing hello **Volume Containers** page and modifying hello volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="df401-173">모든 hello 참조를 제거한 경우에 hello 서식 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-173">When all hello references have been removed, you can delete hello template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="df401-174">기본 대역폭 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="df401-174">Use a default bandwidth template</span></span>
<span data-ttu-id="df401-175">기본 대역폭 템플릿이 제공 하 고 hello 클라우드를 액세스할 때 기본 tooenforce 대역폭 제어 하 여 볼륨 컨테이너에 의해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-175">A default bandwidth template is provided and is used by volume containers by default tooenforce bandwidth controls when accessing hello cloud.</span></span> <span data-ttu-id="df401-176">hello 기본 템플릿은 템플릿을 직접 만드는 사용자에 대 한 준비를 참조로도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-176">hello default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="df401-177">이 기본 템플릿의 hello 세부 정보는.</span><span class="sxs-lookup"><span data-stu-id="df401-177">hello details of this default template are:</span></span>

* <span data-ttu-id="df401-178">**이름** – 무제한 저녁 시간 및 주말</span><span class="sxs-lookup"><span data-stu-id="df401-178">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="df401-179">**일정** – 월요일 tooFriday 오전 8 시 ~ 오후 5 시 장치 시간 1mbps의 대역폭 속도 적용 하는 단일 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-179">**Schedule** – A single schedule from Monday tooFriday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="df401-180">hello 대역폭 tooUnlimited hello 주 hello 나머지에 대해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-180">hello bandwidth is set tooUnlimited for hello remainder of hello week.</span></span>

<span data-ttu-id="df401-181">hello 기본 서식 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-181">hello default template can be edited.</span></span> <span data-ttu-id="df401-182">(편집 된 버전 포함)이 서식이 파일의 hello 사용량 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-182">hello usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="df401-183">지정된 시간에 시작되는 하루 종일 대역폭 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="df401-183">Create an all-day bandwidth template that starts at a specified time</span></span>
<span data-ttu-id="df401-184">이 절차 toocreate 지정된 된 시간에 시작 되어 하루 종일 실행 되는 일정에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-184">Follow this procedure toocreate a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="df401-185">Hello 예에서 hello 일정 hello 아침 오전 9 시에 시작 하 고 오전 9 시 hello 다음 날 아침 될 때까지 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-185">In hello example, hello schedule starts at 9 AM in hello morning and runs until 9 AM hello next morning.</span></span> <span data-ttu-id="df401-186">시작 hello 중요 toonote 이며 지정된 된 일정에 대 한 종료 시간 둘 다에 포함 되어야 합니다 hello 동일 24 시간을 예약 하 고 일정 기간에 걸쳐 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-186">It's important toonote that hello start and end times for a given schedule must both be contained on hello same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="df401-187">여러 날짜를 포함 하는 대역폭 템플릿은를 tooset 해야 할 경우 (hello 예제 에서처럼) 일정을 여러 개 toouse 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-187">If you need tooset up bandwidth templates that span multiple days, you will need toouse multiple schedules (as shown in hello example).</span></span>

#### <a name="toocreate-an-all-day-bandwidth-template"></a><span data-ttu-id="df401-188">toocreate는 하루 종일 대역폭 템플릿</span><span class="sxs-lookup"><span data-stu-id="df401-188">toocreate an all-day bandwidth template</span></span>
1. <span data-ttu-id="df401-189">Hello 아침 오전 9 시에 시작 되어 자정까지 실행 되는 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df401-189">Create a schedule that starts at 9 AM in hello morning and runs until midnight.</span></span>
2. <span data-ttu-id="df401-190">다른 일정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-190">Add another schedule.</span></span> <span data-ttu-id="df401-191">Hello 아침에 오전 9 시까지 자정에서 두 번째 일정 toorun hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-191">Configure hello second schedule toorun from midnight until 9 AM in hello morning.</span></span>
3. <span data-ttu-id="df401-192">Hello 대역폭 템플릿을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-192">Save hello bandwidth template.</span></span>

<span data-ttu-id="df401-193">hello 복합 일정이 선택한 시간에 시작 및 하루 종일 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-193">hello composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="df401-194">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="df401-194">Questions and answers about bandwidth templates</span></span>
<span data-ttu-id="df401-195">**Q**.</span><span class="sxs-lookup"><span data-stu-id="df401-195">**Q**.</span></span> <span data-ttu-id="df401-196">Toobandwidth 컨트롤 hello 일정 사이는 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="df401-196">What happens toobandwidth controls when you are in between hello schedules?</span></span> <span data-ttu-id="df401-197">(하나의 일정이 종료되고 다른 일정이 아직 시작되지 않았습니다.)</span><span class="sxs-lookup"><span data-stu-id="df401-197">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="df401-198">**A**.</span><span class="sxs-lookup"><span data-stu-id="df401-198">**A**.</span></span> <span data-ttu-id="df401-199">이러한 경우 적용되는 대역폭 제어는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-199">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="df401-200">즉, 데이터 toohello 클라우드 계층을 지정할 때 해당 hello 장치 무제한 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-200">This means that hello device can use unlimited bandwidth when tiering data toohello cloud.</span></span>

<span data-ttu-id="df401-201">**Q**.</span><span class="sxs-lookup"><span data-stu-id="df401-201">**Q**.</span></span> <span data-ttu-id="df401-202">오프라인 장치에서 대역폭 템플릿을 수정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="df401-202">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="df401-203">**A**.</span><span class="sxs-lookup"><span data-stu-id="df401-203">**A**.</span></span> <span data-ttu-id="df401-204">Hello 해당 장치가 오프 라인 이면 볼륨 컨테이너에서 대역폭 템플릿 수 toomodify 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-204">You will not be able toomodify bandwidth templates on volumes containers if hello corresponding device is offline.</span></span>

<span data-ttu-id="df401-205">**Q**.</span><span class="sxs-lookup"><span data-stu-id="df401-205">**Q**.</span></span> <span data-ttu-id="df401-206">Hello 연결 된 볼륨이 오프 라인일 때는 볼륨 컨테이너와 연결 된 대역폭 템플릿을 편집할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="df401-206">Can you edit a bandwidth template associated with a volume container when hello associated volumes are offline?</span></span>

<span data-ttu-id="df401-207">**A**.</span><span class="sxs-lookup"><span data-stu-id="df401-207">**A**.</span></span> <span data-ttu-id="df401-208">볼륨이 오프라인 상태인 볼륨 컨테이너와 연결된 대역폭 템플릿을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-208">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="df401-209">참고 볼륨이 오프 라인일 때 데이터가 없는 hello 장치 toohello 클라우드에서 계층이지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-209">Note that when volumes are offline, no data will be tiered from hello device toohello cloud.</span></span>

<span data-ttu-id="df401-210">**Q**.</span><span class="sxs-lookup"><span data-stu-id="df401-210">**Q**.</span></span> <span data-ttu-id="df401-211">기본 템플릿을 삭제할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="df401-211">Can you delete a default template?</span></span>

<span data-ttu-id="df401-212">**A**.</span><span class="sxs-lookup"><span data-stu-id="df401-212">**A**.</span></span> <span data-ttu-id="df401-213">기본 서식 파일을 삭제할 수 있지만 않습니다 것이 좋습니다 toodo 하므로.</span><span class="sxs-lookup"><span data-stu-id="df401-213">Although you can delete a default template, it is not a good idea toodo so.</span></span> <span data-ttu-id="df401-214">편집 된 버전을 포함 하 여 기본 서식 파일의 hello 사용량 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-214">hello usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="df401-215">hello 추적 데이터를 분석 하 고 hello 시간이 흐름에 사용 되는 tooimprove hello에 대 한 기본 서식 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-215">hello tracking data is analyzed and over hello course of time, is used tooimprove hello default template.</span></span>

<span data-ttu-id="df401-216">**Q**.</span><span class="sxs-lookup"><span data-stu-id="df401-216">**Q**.</span></span> <span data-ttu-id="df401-217">대역폭 템플릿을 수정 toobe 필요 하다는 어떻게 확인 합니까?</span><span class="sxs-lookup"><span data-stu-id="df401-217">How do you determine that your bandwidth templates need toobe modified?</span></span>

<span data-ttu-id="df401-218">**A**.</span><span class="sxs-lookup"><span data-stu-id="df401-218">**A**.</span></span> <span data-ttu-id="df401-219">속도가 저하 또는 하루에 여러 번 억제 hello 네트워크 표시 toomodify hello 대역폭 템플릿을 사용 해야 하는 기호는 시작할 때 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-219">One of hello signs that you need toomodify hello bandwidth templates is when you start seeing hello network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="df401-220">이 경우 hello I/O 성능 및 네트워크 처리량 차트를 보면 hello 저장소 및 사용 현황 네트워크를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-220">If this happens, monitor hello storage and usage network by looking at hello I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="df401-221">Hello 네트워크 처리량 데이터에서 hello 시간을 확인 하 고 볼륨 컨테이너 네트워크 병목 현상이 발생 하는 hello에 hello.</span><span class="sxs-lookup"><span data-stu-id="df401-221">From hello network throughput data, identify hello time of day and hello volume containers in which hello network bottleneck occurs.</span></span> <span data-ttu-id="df401-222">경우 이런 데이터를 계층화 된 toohello 클라우드 중인 경우 (이 정보를 가져올 모든 볼륨 컨테이너에 대 한 I/O 성능에서 toocloud 장치에 대 한), toomodify hello 대역폭 템플릿이 볼륨 컨테이너와 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-222">If this happens when data is being tiered toohello cloud (get this information from I/O performance for all volume containers for device toocloud), then you will need toomodify hello bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="df401-223">Hello 수정 후 사용 중인 템플릿은가 toomonitor hello 네트워크 다시 상당한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-223">After hello modified templates are in use, you will need toomonitor hello network again for significant latencies.</span></span> <span data-ttu-id="df401-224">계속 발생 하는 경우 해야 합니다 toorevisit 대역폭 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-224">If these still exist, then you will need toorevisit your bandwidth templates.</span></span>

<span data-ttu-id="df401-225">**Q**.</span><span class="sxs-lookup"><span data-stu-id="df401-225">**Q**.</span></span> <span data-ttu-id="df401-226">겹치는 일정이 다 수 볼륨 컨테이너가 장치에 있는 경우 어떤 일이 생기 하지만 서로 다른 제한이 적용 tooeach?</span><span class="sxs-lookup"><span data-stu-id="df401-226">What happens if multiple volume containers on my device have schedules that overlap but different limits apply tooeach?</span></span>

<span data-ttu-id="df401-227">**A**.</span><span class="sxs-lookup"><span data-stu-id="df401-227">**A**.</span></span> <span data-ttu-id="df401-228">3개의 볼륨 컨테이너가 있는 장치가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-228">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="df401-229">hello 완전히 이러한 컨테이너와 연결 된 일정이 겹칩니다.</span><span class="sxs-lookup"><span data-stu-id="df401-229">hello schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="df401-230">각이 컨테이너에 대 한 hello 대역폭 사용은 5, 10, 15mbps 각각입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-230">For each of these containers, hello bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="df401-231">이러한 모든 컨테이너에서 hello 동시 hello 최소 3 hello 대역폭 제한 적용할 수에서 i/o가 발생 하는 경우:이 경우 이러한 나가는 I/O 요청이 공유 하므로 5mbps hello 동일한 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="df401-231">When I/Os are occurring on all of these containers at hello same time, hello minimum of hello 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share hello same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="df401-232">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="df401-232">Best practices for bandwidth templates</span></span>
<span data-ttu-id="df401-233">StorSimple 장치에 대해 이 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="df401-233">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="df401-234">사용자 장치 tooenable 처리량의 가변 제한을 hello 네트워크 hello 장치별 hello 일의 서로 다른 시간에 대역폭 템플릿을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-234">Configure bandwidth templates on your device tooenable variable throttling of hello network throughput by hello device at different times of hello day.</span></span> <span data-ttu-id="df401-235">백업 일정을 함께 사용하면 이 대역폭 템플릿은 사용량이 가장 적을 때 클라우드 작업에 대해 효과적으로 추가 네트워크 대역폭을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df401-235">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="df401-236">Hello 배포 및 hello 필요한 복구 시간 목표 (RTO) hello 크기를 기준으로 특정 배포에 필요한 hello 실제 대역폭을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-236">Calculate hello actual bandwidth required for a particular deployment based on hello size of hello deployment and hello required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="df401-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df401-237">Next steps</span></span>
<span data-ttu-id="df401-238">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df401-238">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

