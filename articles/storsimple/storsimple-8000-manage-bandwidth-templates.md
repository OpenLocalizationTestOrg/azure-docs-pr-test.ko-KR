---
title: "StorSimple 8000 시리즈에 대 한 대역폭 템플릿을 aaaManage | Microsoft Docs"
description: "설명 방법을 toomanage StorSimple 대역폭 템플릿을 toocontrol 대역폭 사용을 허용 합니다."
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
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a><span data-ttu-id="f51c3-103">Hello StorSimple 장치 관리자 서비스 toomanage StorSimple 대역폭 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f51c3-103">Use hello StorSimple Device Manager service toomanage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="f51c3-104">개요</span><span class="sxs-lookup"><span data-stu-id="f51c3-104">Overview</span></span>

<span data-ttu-id="f51c3-105">대역폭 템플릿을 여러 시간에 일정이 tootier hello 데이터로 hello StorSimple 장치 toohello 클라우드 간에 tooconfigure 네트워크 대역폭 사용량 사용.</span><span class="sxs-lookup"><span data-stu-id="f51c3-105">Bandwidth templates allow you tooconfigure network bandwidth usage across multiple time-of-day schedules tootier hello data from hello StorSimple device toohello cloud.</span></span>

<span data-ttu-id="f51c3-106">일정을 제한하는 대역폭을 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="f51c3-107">Hello 작업 네트워크 사용량에 따라 사용자 지정 된 대역폭 일정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-107">Specify customized bandwidth schedules depending on hello workload network usages.</span></span>
* <span data-ttu-id="f51c3-108">관리를 중앙 집중화 하 고 쉽고 원활한 방식으로 여러 장치 간에 hello 일정을 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-108">Centralize management and reuse hello schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="f51c3-109">이 기능은 StorSimple 물리적 장치(모델 8100 및 8600)에 대해서만 사용할 수 있으며 StorSimple Cloud Appliance(모델 8010 및 8020)에 대해서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="hello-bandwidth-templates-blade"></a><span data-ttu-id="f51c3-110">hello 대역폭 템플릿 블레이드</span><span class="sxs-lookup"><span data-stu-id="f51c3-110">hello Bandwidth templates blade</span></span>

<span data-ttu-id="f51c3-111">hello **대역폭 템플릿** 블레이드를 표 형식에서 서비스에 대 한 모든 hello 대역폭 템플릿을 개이고 hello 다음 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-111">hello **Bandwidth templates** blade has all hello bandwidth templates for your service in a tabular format, and contains hello following information:</span></span>

* <span data-ttu-id="f51c3-112">**이름** -할당 된 고유한 이름 toohello 대역폭 템플릿을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="f51c3-112">**Name** – A unique name assigned toohello bandwidth template when it was created.</span></span>
* <span data-ttu-id="f51c3-113">**일정** – hello에 지정된 된 대역폭 템플릿에 포함 된 일정의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-113">**Schedule** – hello number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="f51c3-114">**사용 하는** – hello hello 대역폭 템플릿을 사용 하 여 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-114">**Used by** – hello number of volumes using hello bandwidth templates.</span></span>

<span data-ttu-id="f51c3-115">또한 toohelp 대역폭 템플릿을 구성 하는 추가 정보를 찾을 수 있습니다에:</span><span class="sxs-lookup"><span data-stu-id="f51c3-115">You can also find additional information toohelp configure bandwidth templates in:</span></span>

* [<span data-ttu-id="f51c3-116">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="f51c3-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="f51c3-117">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="f51c3-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="f51c3-118">대역폭 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="f51c3-118">Add a bandwidth template</span></span>

<span data-ttu-id="f51c3-119">Hello 단계 toocreate 새 대역폭 템플릿을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-119">Perform hello following steps toocreate a new bandwidth template.</span></span>

#### <a name="tooadd-a-bandwidth-template"></a><span data-ttu-id="f51c3-120">대역폭 템플릿 tooadd</span><span class="sxs-lookup"><span data-stu-id="f51c3-120">tooadd a bandwidth template</span></span>

1. <span data-ttu-id="f51c3-121">Tooyour StorSimple 장치 관리자 서비스를 이동 **대역폭 템플릿을** 클릭 하 고 **+ 추가 대역폭 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-121">Go tooyour StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![+대역폭 템플릿 추가 클릭](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="f51c3-123">Hello에 **대역폭 템플릿 추가** 블레이드에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-123">In hello **Add bandwidth template** blade, do hello following steps:</span></span>
   
    1. <span data-ttu-id="f51c3-124">대역폭 템플릿에 대한 고유 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="f51c3-125">대역폭 일정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="f51c3-126">toocreate 일정:</span><span class="sxs-lookup"><span data-stu-id="f51c3-126">toocreate a schedule:</span></span>
   
        1. <span data-ttu-id="f51c3-127">Hello 드롭 다운 목록에서 선택 hello **일** hello 주 hello의 일정에 대해 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-127">From hello drop-down list, choose hello **Days** of hello week hello schedule is configured for.</span></span> <span data-ttu-id="f51c3-128">여러 요일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="f51c3-129">**시작 시간**을 _hh:mm_ 형식으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="f51c3-130">이 hello 일정 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-130">This is when hello schedule will begin.</span></span>

        3. <span data-ttu-id="f51c3-131">**종료 시간**을 _hh:mm_ 형식으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="f51c3-132">이 hello 일정을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-132">This is when hello schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="f51c3-133">겹치는 일정은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="f51c3-134">Hello 시작 및 종료 시간 발생 일정이 겹치면 오류 메시지 toothat 효과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-134">If hello start and end times will result in an overlapping schedule, you will see an error message toothat effect.</span></span>

        4. <span data-ttu-id="f51c3-135">Hello 지정 **대역폭 속도**합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-135">Specify hello **Bandwidth Rate**.</span></span> <span data-ttu-id="f51c3-136">이 hello 메가 비트 초당 대역폭 (Mbps) (업로드 및 다운로드) hello 클라우드 관련 작업에서 StorSimple 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-136">This is hello bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving hello cloud (both uploads and downloads).</span></span> <span data-ttu-id="f51c3-137">이 필드에 대해 1에서 1,000 사이의 숫자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![대역폭 일정 정의](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="f51c3-139">반복 단계 toodefine 위에 hello 여러 일정 서식 파일에 대 한 완료 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-139">Repeat hello above steps toodefine multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="f51c3-140">클릭 **추가** toostart 대역폭 템플릿 만들기.</span><span class="sxs-lookup"><span data-stu-id="f51c3-140">Click **Add** toostart creating a bandwidth template.</span></span> <span data-ttu-id="f51c3-141">서식 파일을 생성 하는 hello toohello 대역폭 템플릿 목록이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-141">hello created template is added toohello list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="f51c3-142">대역폭 템플릿 편집</span><span class="sxs-lookup"><span data-stu-id="f51c3-142">Edit a bandwidth template</span></span>

<span data-ttu-id="f51c3-143">Hello 단계 tooedit 대역폭 템플릿을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-143">Perform hello following steps tooedit a bandwidth template.</span></span>

### <a name="tooedit-a-bandwidth-template"></a><span data-ttu-id="f51c3-144">대역폭 템플릿 tooedit</span><span class="sxs-lookup"><span data-stu-id="f51c3-144">tooedit a bandwidth template</span></span>

1. <span data-ttu-id="f51c3-145">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **대역폭 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-145">Go tooyour StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="f51c3-146">Hello 대역폭 템플릿 목록에서 toodelete hello 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-146">In hello list of bandwidth templates, select hello template you wish toodelete.</span></span> <span data-ttu-id="f51c3-147">마우스 오른쪽 단추로 클릭 하 고 hello 상황에 맞는 메뉴에서 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-147">Right-click and from hello context menu, select **Delete**.</span></span>
3. <span data-ttu-id="f51c3-148">확인하라는 메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="f51c3-149">이 hello 대역폭 템플릿을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-149">This should delete hello bandwidth template.</span></span> 
4. <span data-ttu-id="f51c3-150">대역폭 템플릿 목록이 hello tooreflect hello 삭제를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-150">hello list of bandwidth templates updates tooreflect hello deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="f51c3-151">수정 중인 hello 대역폭 템플릿의 기존 일정과 일정 overlaps를 편집 하는 hello 경우 변경 내용을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-151">You cannot save your changes if hello edited schedule overlaps with an existing schedule in hello bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="f51c3-152">대역폭 템플릿 삭제</span><span class="sxs-lookup"><span data-stu-id="f51c3-152">Delete a bandwidth template</span></span>

<span data-ttu-id="f51c3-153">Hello 단계 toodelete 대역폭 템플릿을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-153">Perform hello following steps toodelete a bandwidth template.</span></span>

#### <a name="toodelete-a-bandwidth-template"></a><span data-ttu-id="f51c3-154">대역폭 템플릿 toodelete</span><span class="sxs-lookup"><span data-stu-id="f51c3-154">toodelete a bandwidth template</span></span>

1. <span data-ttu-id="f51c3-155">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **대역폭 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-155">Go tooyour StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="f51c3-156">Hello 대역폭 템플릿 목록에서 toodelete hello 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-156">In hello list of bandwidth templates, select hello template you wish toodelete.</span></span> <span data-ttu-id="f51c3-157">마우스 오른쪽 단추로 클릭 하 고 hello 상황에 맞는 메뉴에서 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-157">Right-click and from hello context menu, select Delete.</span></span>
3. <span data-ttu-id="f51c3-158">확인하라는 메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="f51c3-159">이 hello 대역폭 템플릿을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-159">This should delete hello bandwidth template.</span></span>
4. <span data-ttu-id="f51c3-160">대역폭 템플릿 목록이 hello tooreflect hello 삭제를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-160">hello list of bandwidth templates updates tooreflect hello deletion.</span></span>

<span data-ttu-id="f51c3-161">Hello 서식 파일은 볼륨에서 사용 중인 경우 있습니다 허용 되지 것입니다 toodelete 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-161">If hello template is in use by any volume(s), you will not be allowed toodelete it.</span></span> <span data-ttu-id="f51c3-162">사용 중인 해당 hello 템플릿은 나타내는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-162">You will see an error message indicating that hello template is in use.</span></span> <span data-ttu-id="f51c3-163">모든 hello 참조 toohello 서식 파일을 제거 해야 하 라는 오류 메시지 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-163">An error message dialog box will appear advising you that all hello references toohello template should be removed.</span></span>

<span data-ttu-id="f51c3-164">Hello에 액세스 하 여 모든 hello 참조 toohello 파일을 삭제할 수 **볼륨 컨테이너** 페이지 및 다른 서식 파일을 사용 하거나 사용자 지정 또는 무제한 대역폭을 사용 하 여이 템플릿을 사용 하는 hello 볼륨 컨테이너 수정 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-164">You can delete all hello references toohello template by accessing hello **Volume Containers** page and modifying hello volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="f51c3-165">모든 hello 참조를 제거한 경우에 hello 서식 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-165">When all hello references have been removed, you can delete hello template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="f51c3-166">기본 대역폭 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="f51c3-166">Use a default bandwidth template</span></span>

<span data-ttu-id="f51c3-167">기본 대역폭 템플릿이 제공 하 고 hello 클라우드를 액세스할 때 기본 tooenforce 대역폭 제어 하 여 볼륨 컨테이너에 의해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-167">A default bandwidth template is provided and is used by volume containers by default tooenforce bandwidth controls when accessing hello cloud.</span></span> <span data-ttu-id="f51c3-168">hello 기본 템플릿은 템플릿을 직접 만드는 사용자에 대 한 준비를 참조로도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-168">hello default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="f51c3-169">이 기본 템플릿의 hello 세부 정보는.</span><span class="sxs-lookup"><span data-stu-id="f51c3-169">hello details of this default template are:</span></span>

* <span data-ttu-id="f51c3-170">**이름** – 무제한 저녁 시간 및 주말</span><span class="sxs-lookup"><span data-stu-id="f51c3-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="f51c3-171">**일정** – 월요일 tooFriday 오전 8 시 ~ 오후 5 시 장치 시간 1mbps의 대역폭 속도 적용 하는 단일 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-171">**Schedule** – A single schedule from Monday tooFriday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="f51c3-172">hello 대역폭 tooUnlimited hello 주 hello 나머지에 대해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-172">hello bandwidth is set tooUnlimited for hello remainder of hello week.</span></span>

<span data-ttu-id="f51c3-173">hello 기본 서식 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-173">hello default template can be edited.</span></span> <span data-ttu-id="f51c3-174">(편집 된 버전 포함)이 서식이 파일의 hello 사용량 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-174">hello usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="f51c3-175">지정된 시간에 시작되는 하루 종일 대역폭 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="f51c3-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="f51c3-176">이 절차 toocreate 지정된 된 시간에 시작 되어 하루 종일 실행 되는 일정에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-176">Follow this procedure toocreate a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="f51c3-177">Hello 예에서 hello 일정 hello 아침 오전 9 시에 시작 하 고 오전 9 시 hello 다음 날 아침 될 때까지 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-177">In hello example, hello schedule starts at 9 AM in hello morning and runs until 9 AM hello next morning.</span></span> <span data-ttu-id="f51c3-178">시작 hello 중요 toonote 이며 지정된 된 일정에 대 한 종료 시간 둘 다에 포함 되어야 합니다 hello 동일 24 시간을 예약 하 고 일정 기간에 걸쳐 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-178">It's important toonote that hello start and end times for a given schedule must both be contained on hello same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="f51c3-179">여러 날짜를 포함 하는 대역폭 템플릿은를 tooset 해야 할 경우 (hello 예제 에서처럼) 일정을 여러 개 toouse 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-179">If you need tooset up bandwidth templates that span multiple days, you will need toouse multiple schedules (as shown in hello example).</span></span>

#### <a name="toocreate-an-all-day-bandwidth-template"></a><span data-ttu-id="f51c3-180">toocreate는 하루 종일 대역폭 템플릿</span><span class="sxs-lookup"><span data-stu-id="f51c3-180">toocreate an all-day bandwidth template</span></span>

1. <span data-ttu-id="f51c3-181">Hello 아침 오전 9 시에 시작 되어 자정까지 실행 되는 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-181">Create a schedule that starts at 9 AM in hello morning and runs until midnight.</span></span>
2. <span data-ttu-id="f51c3-182">다른 일정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-182">Add another schedule.</span></span> <span data-ttu-id="f51c3-183">Hello 아침에 오전 9 시까지 자정에서 두 번째 일정 toorun hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-183">Configure hello second schedule toorun from midnight until 9 AM in hello morning.</span></span>
3. <span data-ttu-id="f51c3-184">Hello 대역폭 템플릿을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-184">Save hello bandwidth template.</span></span>

<span data-ttu-id="f51c3-185">hello 복합 일정이 선택한 시간에 시작 및 하루 종일 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-185">hello composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="f51c3-186">대역폭 템플릿에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="f51c3-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="f51c3-187">**Q**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-187">**Q**.</span></span> <span data-ttu-id="f51c3-188">Toobandwidth 컨트롤 hello 일정 사이는 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="f51c3-188">What happens toobandwidth controls when you are in between hello schedules?</span></span> <span data-ttu-id="f51c3-189">(하나의 일정이 종료되고 다른 일정이 아직 시작되지 않았습니다.)</span><span class="sxs-lookup"><span data-stu-id="f51c3-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="f51c3-190">**A**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-190">**A**.</span></span> <span data-ttu-id="f51c3-191">이러한 경우 적용되는 대역폭 제어는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="f51c3-192">즉, 데이터 toohello 클라우드 계층을 지정할 때 해당 hello 장치 무제한 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-192">This means that hello device can use unlimited bandwidth when tiering data toohello cloud.</span></span>

<span data-ttu-id="f51c3-193">**Q**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-193">**Q**.</span></span> <span data-ttu-id="f51c3-194">오프라인 장치에서 대역폭 템플릿을 수정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f51c3-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="f51c3-195">**A**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-195">**A**.</span></span> <span data-ttu-id="f51c3-196">Hello 해당 장치가 오프 라인 이면 볼륨 컨테이너에서 대역폭 템플릿 수 toomodify 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-196">You will not be able toomodify bandwidth templates on volumes containers if hello corresponding device is offline.</span></span>

<span data-ttu-id="f51c3-197">**Q**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-197">**Q**.</span></span> <span data-ttu-id="f51c3-198">Hello 연결 된 볼륨이 오프 라인일 때는 볼륨 컨테이너와 연결 된 대역폭 템플릿을 편집할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f51c3-198">Can you edit a bandwidth template associated with a volume container when hello associated volumes are offline?</span></span>

<span data-ttu-id="f51c3-199">**A**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-199">**A**.</span></span> <span data-ttu-id="f51c3-200">볼륨이 오프라인 상태인 볼륨 컨테이너와 연결된 대역폭 템플릿을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="f51c3-201">참고 볼륨이 오프 라인일 때 데이터가 없는 hello 장치 toohello 클라우드에서 계층이지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-201">Note that when volumes are offline, no data will be tiered from hello device toohello cloud.</span></span>

<span data-ttu-id="f51c3-202">**Q**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-202">**Q**.</span></span> <span data-ttu-id="f51c3-203">기본 템플릿을 삭제할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f51c3-203">Can you delete a default template?</span></span>

<span data-ttu-id="f51c3-204">**A**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-204">**A**.</span></span> <span data-ttu-id="f51c3-205">기본 서식 파일을 삭제할 수 있지만 않습니다 것이 좋습니다 toodo 하므로.</span><span class="sxs-lookup"><span data-stu-id="f51c3-205">Although you can delete a default template, it is not a good idea toodo so.</span></span> <span data-ttu-id="f51c3-206">편집 된 버전을 포함 하 여 기본 서식 파일의 hello 사용량 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-206">hello usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="f51c3-207">hello 추적 데이터를 분석 하 고 hello 시간이 흐름에 사용 되는 tooimprove hello에 대 한 기본 서식 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-207">hello tracking data is analyzed and over hello course of time, is used tooimprove hello default template.</span></span>

<span data-ttu-id="f51c3-208">**Q**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-208">**Q**.</span></span> <span data-ttu-id="f51c3-209">대역폭 템플릿을 수정 toobe 필요 하다는 어떻게 확인 합니까?</span><span class="sxs-lookup"><span data-stu-id="f51c3-209">How do you determine that your bandwidth templates need toobe modified?</span></span>

<span data-ttu-id="f51c3-210">**A**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-210">**A**.</span></span> <span data-ttu-id="f51c3-211">속도가 저하 또는 하루에 여러 번 억제 hello 네트워크 표시 toomodify hello 대역폭 템플릿을 사용 해야 하는 기호는 시작할 때 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-211">One of hello signs that you need toomodify hello bandwidth templates is when you start seeing hello network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="f51c3-212">이 경우 hello I/O 성능 및 네트워크 처리량 차트를 보면 hello 저장소 및 사용 현황 네트워크를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-212">If this happens, monitor hello storage and usage network by looking at hello I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="f51c3-213">Hello 네트워크 처리량 데이터에서 hello 시간을 확인 하 고 볼륨 컨테이너 네트워크 병목 현상이 발생 하는 hello에 hello.</span><span class="sxs-lookup"><span data-stu-id="f51c3-213">From hello network throughput data, identify hello time of day and hello volume containers in which hello network bottleneck occurs.</span></span> <span data-ttu-id="f51c3-214">경우 이런 데이터를 계층화 된 toohello 클라우드 중인 경우 (이 정보를 가져올 모든 볼륨 컨테이너에 대 한 I/O 성능에서 toocloud 장치에 대 한), toomodify hello 대역폭 템플릿이 볼륨 컨테이너와 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-214">If this happens when data is being tiered toohello cloud (get this information from I/O performance for all volume containers for device toocloud), then you will need toomodify hello bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="f51c3-215">Hello 수정 후 사용 중인 템플릿은가 toomonitor hello 네트워크 다시 상당한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-215">After hello modified templates are in use, you will need toomonitor hello network again for significant latencies.</span></span> <span data-ttu-id="f51c3-216">계속 발생 하는 경우 해야 합니다 toorevisit 대역폭 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-216">If these still exist, then you will need toorevisit your bandwidth templates.</span></span>

<span data-ttu-id="f51c3-217">**Q**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-217">**Q**.</span></span> <span data-ttu-id="f51c3-218">겹치는 일정이 다 수 볼륨 컨테이너가 장치에 있는 경우 어떤 일이 생기 하지만 서로 다른 제한이 적용 tooeach?</span><span class="sxs-lookup"><span data-stu-id="f51c3-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply tooeach?</span></span>

<span data-ttu-id="f51c3-219">**A**.</span><span class="sxs-lookup"><span data-stu-id="f51c3-219">**A**.</span></span> <span data-ttu-id="f51c3-220">3개의 볼륨 컨테이너가 있는 장치가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="f51c3-221">hello 완전히 이러한 컨테이너와 연결 된 일정이 겹칩니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-221">hello schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="f51c3-222">각이 컨테이너에 대 한 hello 대역폭 사용은 5, 10, 15mbps 각각입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-222">For each of these containers, hello bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="f51c3-223">이러한 모든 컨테이너에서 hello 동시 hello 최소 3 hello 대역폭 제한 적용할 수에서 I/O 발생 하는 경우:이 경우 이러한 나가는 I/O 요청이 공유 하므로 5mbps hello 동일한 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-223">When I/O are occurring on all of these containers at hello same time, hello minimum of hello 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share hello same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="f51c3-224">대역폭 템플릿에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="f51c3-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="f51c3-225">StorSimple 장치에 대해 이 모범 사례를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="f51c3-226">사용자 장치 tooenable 처리량의 가변 제한을 hello 네트워크 hello 장치별 hello 일의 서로 다른 시간에 대역폭 템플릿을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-226">Configure bandwidth templates on your device tooenable variable throttling of hello network throughput by hello device at different times of hello day.</span></span> <span data-ttu-id="f51c3-227">백업 일정을 함께 사용하면 이 대역폭 템플릿은 사용량이 가장 적을 때 클라우드 작업에 대해 효과적으로 추가 네트워크 대역폭을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="f51c3-228">Hello 배포 및 hello 필요한 복구 시간 목표 (RTO) hello 크기를 기준으로 특정 배포에 필요한 hello 실제 대역폭을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-228">Calculate hello actual bandwidth required for a particular deployment based on hello size of hello deployment and hello required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f51c3-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f51c3-229">Next steps</span></span>

<span data-ttu-id="f51c3-230">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f51c3-230">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

