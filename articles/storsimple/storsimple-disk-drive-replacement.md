---
title: "StorSimple 장치에 디스크 드라이브 aaaReplace | Microsoft Docs"
description: "StorSimple 기본 인클로저 또는 EBOD 인클로저 tooreplace 디스크 드라이브 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="42cb5-103">StorSimple 장치의 디스크 드라이브 교체</span><span class="sxs-lookup"><span data-stu-id="42cb5-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="42cb5-104">개요</span><span class="sxs-lookup"><span data-stu-id="42cb5-104">Overview</span></span>
<span data-ttu-id="42cb5-105">이 자습서에서는 Microsoft Azure StorSimple 장치에서 오작동하거나 오류가 발생한 하드 디스크 드라이브를 꺼내고 교체하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="42cb5-106">디스크 드라이브 tooreplace 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="42cb5-107">Hello 변조 방지 잠금 해제</span><span class="sxs-lookup"><span data-stu-id="42cb5-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="42cb5-108">Hello 디스크 드라이브를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-108">Remove hello disk drive</span></span>
* <span data-ttu-id="42cb5-109">Hello 대체 디스크 드라이브를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42cb5-110">제거 하 고 디스크 드라이브의 교체에 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="42cb5-111">Hello 변조 방지 잠금 해제</span><span class="sxs-lookup"><span data-stu-id="42cb5-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="42cb5-112">어떻게 StorSimple 장치에 대 한 hello 변조 방지 잠금을 수 설정 또는 해제 hello 디스크 드라이브를 교체 하는 경우이 절차에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="42cb5-113">hello 변조 방지 잠금은 hello 드라이브 캐리어 핸들에 맞추는 고 hello 핸들의 래치 섹션 hello에에서 있는 작은 구멍을 통해 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="42cb5-114">드라이브는 hello 잠금 세트 toohello 잠긴 위치와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="42cb5-115">toounlock hello 변조 방지 잠금</span><span class="sxs-lookup"><span data-stu-id="42cb5-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="42cb5-116">Hello 핸들에 hello 구멍에 및 해당 소켓에 조심 스럽게 hello 잠금 키 (Microsoft에서 제공한 "변조 방지" T10 드라이버)를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="42cb5-117">Hello 변조 방지 잠금이 활성화 되 면 hello에 빨간색 표시기 hello 구멍에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
   > 
   > 
   
    ![잠긴 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="42cb5-119">**그림 1** 조작 방지 잠금 사용</span><span class="sxs-lookup"><span data-stu-id="42cb5-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="42cb5-120">레이블</span><span class="sxs-lookup"><span data-stu-id="42cb5-120">Label</span></span> | <span data-ttu-id="42cb5-121">설명</span><span class="sxs-lookup"><span data-stu-id="42cb5-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="42cb5-122">1</span><span class="sxs-lookup"><span data-stu-id="42cb5-122">1</span></span> |<span data-ttu-id="42cb5-123">표시기 입구</span><span class="sxs-lookup"><span data-stu-id="42cb5-123">Indicator aperture</span></span> |
   | <span data-ttu-id="42cb5-124">2</span><span class="sxs-lookup"><span data-stu-id="42cb5-124">2</span></span> |<span data-ttu-id="42cb5-125">조작 방지 잠금</span><span class="sxs-lookup"><span data-stu-id="42cb5-125">Antitamper lock</span></span> |
2. <span data-ttu-id="42cb5-126">Hello에 빨간색 표시기가 hello 키 위의 구멍 hello에에서 표시 되지 않을 때까지 반대 방향으로 돌립니다에 hello 키를 회전 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="42cb5-127">Hello 키를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-127">Remove hello key.</span></span>
   
    ![잠금 해제된 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="42cb5-129">**그림 2** 잠금 해제된 디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="42cb5-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="42cb5-130">이제 hello 디스크 드라이브를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="42cb5-131">역방향 tooengage hello 잠금의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="42cb5-132">Hello 디스크 드라이브를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-132">Remove hello disk drive</span></span>
<span data-ttu-id="42cb5-133">StorSimple 장치는 RAID 10과 유사한 저장소 공간 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="42cb5-134">이는 오류가 발생한 하나의 디스크, SSD(반도체 드라이브) 또는 HDD(하드 디스크 드라이브)에서 정상적으로 작동할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="42cb5-135">시스템에 둘 이상의 실패 한 디스크를 제거 하지 마십시오 둘 이상의 SSD 또는 HDD 언제 든 지 hello 시스템에서 시간.</span><span class="sxs-lookup"><span data-stu-id="42cb5-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="42cb5-136">이렇게 하면 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="42cb5-137">이전에 SSD가 포함된 슬롯에는 교체 SSD를 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="42cb5-138">마찬가지로, 이전에 HDD가 포함된 슬롯에는 교체 HDD를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="42cb5-139">Azure 클래식 포털 hello 슬롯 0 – 번호는 11입니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-139">In hello Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="42cb5-140">따라서 hello 포털 hello 장치에서 슬롯 2의에서 디스크에 오류가 표시 되 면 hello hello 세 번째 슬롯에서 오류가 발생 한 디스크에서에서 찾습니다 hello 창의 상단 왼쪽.</span><span class="sxs-lookup"><span data-stu-id="42cb5-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="42cb5-141">드라이브를 제거 하 고 hello 시스템 작동 하는 동안 대체 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="42cb5-142">tooremove 드라이브</span><span class="sxs-lookup"><span data-stu-id="42cb5-142">tooremove a drive</span></span>
1. <span data-ttu-id="42cb5-143">tooidentify 실패 한 디스크 hello hello Azure 클래식 포털에서 너무 이동**장치** > **유지 관리** > **하드웨어 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-143">tooidentify hello failed disk, in hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="42cb5-144">디스크에서 hello 기본 인클로저 및/또는 EBOD 인클로저 (8600 모델을 사용 하는 경우) 하는 경우 실패할 수 있습니다, 때문에 아래 hello 디스크의 hello 상태 확인 **공유 구성 요소의** 고 **EBOD 인클로저 공유 구성 요소**.</span><span class="sxs-lookup"><span data-stu-id="42cb5-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="42cb5-145">엔클로저 중 하나에서 오류가 발생한 디스크는 빨간색 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="42cb5-146">Hello 기본 인클로저 또는 EBOD 인클로저의 hello hello 앞에서 hello 드라이브를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="42cb5-147">Hello 디스크가 잠금 해제 된 경우 toohello 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="42cb5-148">Hello 디스크 잠겨 있으면 잠금을 해제할 hello 절차에 따라 [hello 변조 방지 잠금 해제](#disengage-the-antitamper-lock)합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="42cb5-149">키를 눌러 hello 검정 hello 드라이브 캐리어 모듈에 대 한 래치 및 hello 섀시 hello 앞에서 끌어오기 hello 드라이브 캐리어 핸들이 자리를 비울 / 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span> 
   
    ![디스크 드라이브 핸들 해제](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="42cb5-151">**그림 3** hello 드라이브 핸들 해제</span><span class="sxs-lookup"><span data-stu-id="42cb5-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="42cb5-152">Hello 드라이브 캐리어 핸들이 완전히 확장 하는 경우에 hello 드라이브 캐리어를 hello 섀시 밖으로 밉니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![디스크 드라이브 밖으로 디스크 밀기](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="42cb5-154">**그림 4** 슬라이딩 hello carrier hello 디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="42cb5-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="42cb5-155">Hello 대체 디스크 드라이브를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="42cb5-156">StorSimple 장치에는 드라이브에 오류가 발생 한 후 제거 했기 프로시저 tooreplace이에 따라 새 드라이브로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="42cb5-157">tooinsert 드라이브</span><span class="sxs-lookup"><span data-stu-id="42cb5-157">tooinsert a drive</span></span>
1. <span data-ttu-id="42cb5-158">다음 이미지는 hello와 같이 hello 드라이브 캐리어 핸들이 완전히 확장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![핸들이 확장된 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="42cb5-160">**그림 5** 핸들이 확장된 드라이브</span><span class="sxs-lookup"><span data-stu-id="42cb5-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="42cb5-161">Hello 드라이브 캐리어를 모든 hello 방식으로 hello 섀시 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-161">Slide hello drive carrier all hello way into hello chassis.</span></span> 
   
    ![디스크 드라이브 캐리어 안으로 디스크 밀기](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="42cb5-163">**그림 6** hello 섀시 안으로 슬라이딩 hello 드라이브 캐리어</span><span class="sxs-lookup"><span data-stu-id="42cb5-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="42cb5-164">Hello 드라이브 캐리어 삽입, 닫기 hello 드라이브 캐리어 핸들이 hello 드라이브 캐리어 핸들이 잠긴된 위치에 고정 될 때까지 hello 섀시에 계속 toopush hello 드라이브 캐리어 하는 동안와.</span><span class="sxs-lookup"><span data-stu-id="42cb5-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="42cb5-165">제공한 Microsoft (변조 방지 Torx 드라이버) toosecure hello 캐리어 핸들에 설정 하 여 잠금 나사 hello는 1/4 시계 반대 방향으로 사용 하 여 hello 잠금 키입니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="42cb5-166">Hello 교체에 성공 했 고 hello 드라이브 작동 하는지 hello Azure 클래식 포털에 액세스 하 여 너무 탐색 확인**유지 관리** > **하드웨어 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-166">Verify that hello replacement was successful and hello drive is operational by accessing hello Azure classic portal and navigating too**Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="42cb5-167">아래 **공유 구성 요소의** 또는 **EBOD 인클로저 공유 구성 요소**, hello 드라이브 상태가 정상 인지를 나타내는 녹색으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-167">Under **Shared Components** or **EBOD enclosure Shared Components**, hello drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42cb5-168">소요 몇 시간 정도 hello 디스크 상태 tooturn 녹색 hello 교체 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-168">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="42cb5-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42cb5-169">Next steps</span></span>
<span data-ttu-id="42cb5-170">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="42cb5-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

