---
title: "aaaStorSimple 관리자 서비스 대시보드 | Microsoft Docs"
description: "Hello StorSimple 관리자 서비스 대시보드를 설명 하 고 설명 어떻게 toouse 것 StorSimple 솔루션의 toomonitor hello 상태입니다."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a><span data-ttu-id="d7b1c-103">Hello StorSimple 관리자 서비스 대시보드 사용</span><span class="sxs-lookup"><span data-stu-id="d7b1c-103">Use hello StorSimple Manager service dashboard</span></span>
## <a name="overview"></a><span data-ttu-id="d7b1c-104">개요</span><span class="sxs-lookup"><span data-stu-id="d7b1c-104">Overview</span></span>
<span data-ttu-id="d7b1c-105">hello StorSimple 관리자 서비스 대시보드 페이지 모든 hello 장치 연결된 toohello 시스템 관리자의 주의가 필요한 사용자를 강조 표시 되는 StorSimple Manager 서비스에 대 한 요약 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-105">hello StorSimple Manager service dashboard page provides a summary view of all hello devices that are connected toohello StorSimple Manager service, highlighting those that need a system administrator's attention.</span></span> <span data-ttu-id="d7b1c-106">이 자습서 hello 대시보드 페이지를 소개 하 고 hello 대시보드 콘텐츠 및 함수를 설명 하며이 페이지에서 수행할 수 있는 hello 작업에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-106">This tutorial introduces hello dashboard page, explains hello dashboard content and function, and describes hello tasks that you can perform from this page.</span></span>

![서비스 대시보드](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

<span data-ttu-id="d7b1c-108">hello StorSimple 관리자 서비스 대시보드는 hello 다음 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-108">hello StorSimple Manager service dashboard displays hello following information:</span></span>

* <span data-ttu-id="d7b1c-109">Hello에 **차트** 영역을 표시 하는 장치에 대 한 hello 관련 메트릭 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-109">In hello **chart** area, you can see hello relevant metrics chart for your devices.</span></span> <span data-ttu-id="d7b1c-110">Hello 기본 저장소 (로컬로 고정 된 및 계층)를 볼 수 시간 동안 장치에서 사용 하는 hello 클라우드 저장소 뿐만 아니라 모든 hello 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-110">You can view hello primary storage (locally pinned and tiered) used across all hello devices, as well as hello cloud storage consumed by devices over a period of time.</span></span> <span data-ttu-id="d7b1c-111">Hello 차트 toospecify 1 주, 1 개월, 3 개월 또는 1 년 간 시간 간격의 hello 오른쪽 위 모서리에서 hello 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-111">Use hello controls in hello top-right corner of hello chart toospecify a 1-week, 1-month, 3-month, or 1-year time scale.</span></span>
* <span data-ttu-id="d7b1c-112">hello **사용 개요** 프로 비전 되 고 모든 장치에서 모든 장치 상대 toohello 총 사용 가능한 저장소에서 사용 되는 기본 저장소를 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-112">hello **usage overview** shows hello primary storage that is provisioned and consumed by all devices relative toohello total storage available across all devices.</span></span> <span data-ttu-id="d7b1c-113">**사용자를 프로 비전** toohello 양의 준비 되 고 사용 하기 위해 할당 된 저장소 참조 **사용** toohello 연결된 장치로 되는 hello 초기자에 의해 표시 된 대로 toousage 볼륨의를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-113">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, while **Used** refers toousage of volumes as viewed by hello initiators that are connected toohello devices.</span></span>
* <span data-ttu-id="d7b1c-114">hello **경고** 영역 경고 심각도 별로 그룹화 하는 모든 hello 장치에서 모든 hello 활성 경고에 대 한 스냅숏을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-114">hello **alerts** area provides a snapshot of all hello active alerts across all hello devices, grouped by alert severity.</span></span> <span data-ttu-id="d7b1c-115">Hello 열립니다 hello 심각도 수준을 클릭 하면 **경고** 페이지, 범위가 지정 된 tooshow 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-115">Clicking hello severity level opens hello **Alerts** page, scoped tooshow those alerts.</span></span> <span data-ttu-id="d7b1c-116">Hello에 **경고** 페이지 권장된 조치를 포함 하 여 해당 경고에 대 한 개별 경고 tooview 추가 세부 정보 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-116">On hello **Alerts** page, you can click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="d7b1c-117">Hello 문제가 해결 된 경우에 hello 경고를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-117">You can also clear hello alert if hello issue has been resolved.</span></span>
* <span data-ttu-id="d7b1c-118">hello **작업** 영역에는 연결 된 모든 장치에서 최근 작업 스냅숏이 제공 tooyour 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-118">hello **jobs** area provides a snapshot of recent jobs across all devices that are connected tooyour service.</span></span> <span data-ttu-id="d7b1c-119">Toolook 현재 지난 24 시간 동안 hello에 실패 하는 진행 중인 작업에 사용할 수 있는 링크 또는 다음 24 시간 동안 toorun hello에 예약 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-119">There are links that you can use toolook at jobs that are currently in progress, those that failed in hello last 24 hours, or those that are scheduled toorun in hello next 24 hours.</span></span>
* <span data-ttu-id="d7b1c-120">hello **눈에 보는** 영역에서는 서비스 상태, 장치 연결 된 toohello 서비스, hello 서비스의 위치와 hello 서비스와 관련 된 hello 구독 세부 정보와 수 등 유용한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-120">hello **quick glance** area provides useful information such as service status, number of devices connected toohello service, location of hello service, and details of hello subscription that is associated with hello service.</span></span> <span data-ttu-id="d7b1c-121">링크 toohello 작업 로그 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-121">There is also a link toohello operations log.</span></span> <span data-ttu-id="d7b1c-122">Hello 링크 toosee 목록이 완료 된 모든 StorSimple Manager 서비스 작업을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-122">Click hello link toosee a list of all completed StorSimple Manager service operations.</span></span>

<span data-ttu-id="d7b1c-123">Hello StorSimple 관리자 서비스 대시보드 페이지 tooinitiate hello 다음 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-123">You can use hello StorSimple Manager service dashboard page tooinitiate hello following tasks:</span></span>

* <span data-ttu-id="d7b1c-124">보거나 hello 서비스 등록 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-124">View or regenerate hello service registration key.</span></span>
* <span data-ttu-id="d7b1c-125">Hello 서비스 데이터 암호화 키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-125">Change hello service data encryption key.</span></span>
* <span data-ttu-id="d7b1c-126">Hello 작업 로그를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-126">View hello operation logs.</span></span>

## <a name="view-or-regenerate-hello-service-registration-key"></a><span data-ttu-id="d7b1c-127">보거나 hello 서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="d7b1c-127">View or regenerate hello service registration key</span></span>
<span data-ttu-id="d7b1c-128">hello 서비스 등록 키는 hello 장치에에서 표시 되도록 hello 추가 관리 작업을 위해 Azure 클래식 포털 사용 되는 tooregister hello StorSimple Manager 서비스를 사용 하 여 Microsoft Azure StorSimple 장치를입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-128">hello service registration key is used tooregister a Microsoft Azure StorSimple device with hello StorSimple Manager service, so that hello device appears in hello Azure classic portal for further management actions.</span></span> <span data-ttu-id="d7b1c-129">hello 키 hello 첫 번째 장치에 만들어지고 나머지 장치 hello와 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-129">hello key is created on hello first device and shared with hello rest of your devices.</span></span>

<span data-ttu-id="d7b1c-130">클릭 하면 **등록 키** (hello hello 페이지 맨) hello 열립니다 **서비스 등록 키** 어느 hello 현재 서비스 등록 키 toohello 클립보드로 복사를 수행할 수 있는 대화 상자 또는 hello 서비스 등록 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-130">Clicking **Registration Key** (at hello bottom of hello page) opens hello **Service Registration Key** dialog box, where you can either copy hello current service registration key toohello clipboard or regenerate hello service registration key.</span></span>

<span data-ttu-id="d7b1c-131">Hello 키 다시 생성 이전에 등록 된 장치에는 영향을 주지: hello 장치 서비스에 등록 된 hello hello 키가 다시 생성 한 후에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-131">Regenerating hello key does not affect previously registered devices: it affects only hello devices that are registered with hello service after hello key is regenerated.</span></span>

<span data-ttu-id="d7b1c-132">보기 및 너무 hello 서비스 등록 키를 이동 생성 하는 방법에 대 한 자세한 내용은[Get hello 서비스 등록 키](storsimple-manage-service.md#get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-132">For more information about viewing and generating hello service registration key, go too[Get hello service registration key](storsimple-manage-service.md#get-the-service-registration-key).</span></span>

## <a name="change-hello-service-data-encryption-key"></a><span data-ttu-id="d7b1c-133">Hello 서비스 데이터 암호화 키 변경</span><span class="sxs-lookup"><span data-stu-id="d7b1c-133">Change hello service data encryption key</span></span>
<span data-ttu-id="d7b1c-134">서비스 데이터 암호화 키는 StorSimple 관리자 서비스 toohello StorSimple 장치에서 전송 된 저장소 계정 자격 증명과 같은 사용 되는 tooencrypt 고객 기밀 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-134">Service data encryption keys are used tooencrypt confidential customer data, such as storage account credentials, that are sent from your StorSimple Manager service toohello StorSimple device.</span></span> <span data-ttu-id="d7b1c-135">필요 합니다 toochange 이러한 키는 정기적으로 IT 조직 hello 저장 장치에 대 한 키 순환 정책을 경우.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-135">You will need toochange these keys periodically if your IT organization has a key rotation policy on hello storage devices.</span></span> <span data-ttu-id="d7b1c-136">hello 키 변경 프로세스 수 약간 다를 수 있는지에 따라 장치를 하나 또는 여러 장치 hello StorSimple Manager 서비스에서 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-136">hello key change process can be slightly different depending on whether there is a single device or multiple devices managed by hello StorSimple Manager service.</span></span>

<span data-ttu-id="d7b1c-137">Hello 서비스 데이터 암호화 키 변경 3 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-137">Changing hello service data encryption key is a 3-step process:</span></span>

1. <span data-ttu-id="d7b1c-138">Azure 클래식 포털 hello using, 장치 toochange hello 서비스 데이터 암호화 키 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-138">Using hello Azure classic portal, authorize a device toochange hello service data encryption key.</span></span>
2. <span data-ttu-id="d7b1c-139">StorSimple 용 Windows PowerShell을 사용 하 여, hello 서비스 데이터 암호화 키 변경을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-139">Using Windows PowerShell for StorSimple, initiate hello service data encryption key change.</span></span>
3. <span data-ttu-id="d7b1c-140">하나 이상의 StorSimple 장치가 있는 경우 hello 서비스 데이터 암호화 키 hello에 다른 장치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-140">If you have more than one StorSimple device, update hello service data encryption key on hello other devices.</span></span>

<span data-ttu-id="d7b1c-141">hello 다음 단계에서는 hello 서비스 데이터 암호화 키에 대 한 hello 롤오버 프로세스.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-141">hello following steps describe hello rollover process for hello service data encryption key.</span></span>

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a><span data-ttu-id="d7b1c-142">Hello 작업 로그 보기</span><span class="sxs-lookup"><span data-stu-id="d7b1c-142">View hello operations logs</span></span>
<span data-ttu-id="d7b1c-143">Hello에서 사용할 수 있는 hello 작업 로그 링크를 클릭 하 여 hello 작업 로그를 볼 수 **눈에 보는** hello 대시보드의 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-143">You can view hello operation logs by clicking hello operation logs link available in hello **quick glance** pane of hello dashboard.</span></span> <span data-ttu-id="d7b1c-144">그러면 toohello 관리 서비스 페이지에서 필터링 하 고 hello 참조 수 로그 특정 tooyour StorSimple Manager 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-144">This will take you toohello management services page, where you can filter and see hello logs specific tooyour StorSimple Manager service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7b1c-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7b1c-145">Next steps</span></span>
* <span data-ttu-id="d7b1c-146">너무 방법에 대해 알아봅니다[StorSimple 장치 문제 해결](storsimple-troubleshoot-operational-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-146">Learn how too[troubleshoot a StorSimple device](storsimple-troubleshoot-operational-device.md).</span></span>
* <span data-ttu-id="d7b1c-147">너무 방법에 대 한 자세한[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7b1c-147">Learn more about how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

