---
title: "StorSimple 8000 시리즈 장치의 디스크 드라이브 교체 | Microsoft Docs"
description: "StorSimple 기본 인클로저 또는 EBOD 엔클로저의 디스크 드라이브를 교체하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: bb259b626ecd4dcbaa8f1c465f1ece4516aa8881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="50f99-103">StorSimple 8000 시리즈 장치의 디스크 드라이브 교체</span><span class="sxs-lookup"><span data-stu-id="50f99-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="50f99-104">개요</span><span class="sxs-lookup"><span data-stu-id="50f99-104">Overview</span></span>
<span data-ttu-id="50f99-105">이 자습서에서는 Microsoft Azure StorSimple 장치에서 오작동하거나 오류가 발생한 하드 디스크 드라이브를 꺼내고 교체하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="50f99-106">디스크 드라이브를 교체하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="50f99-107">조작 방지 잠금 해제</span><span class="sxs-lookup"><span data-stu-id="50f99-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="50f99-108">디스크 드라이브 꺼내기</span><span class="sxs-lookup"><span data-stu-id="50f99-108">Remove the disk drive</span></span>
* <span data-ttu-id="50f99-109">교체 디스크 드라이브 설치</span><span class="sxs-lookup"><span data-stu-id="50f99-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50f99-110">디스크 드라이브를 꺼내고 교체하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에서 안전 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="50f99-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="50f99-111">조작 방지 잠금 해제</span><span class="sxs-lookup"><span data-stu-id="50f99-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="50f99-112">이 절차에서는 디스크 드라이브를 교체할 때 StorSimple 장치의 조작 방지 잠금을 사용 또는 해제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="50f99-113">조작 방지 잠금은 드라이브 캐리어 핸들에 있으며 핸들의 래치 섹션에 있는 작은 입구를 통해 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="50f99-114">드라이브는 잠금이 잠긴 위치로 설정되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="50f99-115">조작 방지 잠금을 해제하려면</span><span class="sxs-lookup"><span data-stu-id="50f99-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="50f99-116">핸들의 입구와 해당 소켓에 잠금 키(Microsoft에서 제공한 "조작 방지" T10 드라이버)를 조심해서 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   <span data-ttu-id="50f99-117">조작 방지 잠금이 활성화되면 입구에 빨간색 표시기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
  
    ![잠긴 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="50f99-119">**그림 1** 조작 방지 잠금 사용</span><span class="sxs-lookup"><span data-stu-id="50f99-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="50f99-120">레이블</span><span class="sxs-lookup"><span data-stu-id="50f99-120">Label</span></span> | <span data-ttu-id="50f99-121">설명</span><span class="sxs-lookup"><span data-stu-id="50f99-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="50f99-122">1</span><span class="sxs-lookup"><span data-stu-id="50f99-122">1</span></span> |<span data-ttu-id="50f99-123">표시기 입구</span><span class="sxs-lookup"><span data-stu-id="50f99-123">Indicator aperture</span></span> |
   | <span data-ttu-id="50f99-124">2</span><span class="sxs-lookup"><span data-stu-id="50f99-124">2</span></span> |<span data-ttu-id="50f99-125">조작 방지 잠금</span><span class="sxs-lookup"><span data-stu-id="50f99-125">Antitamper lock</span></span> |
2. <span data-ttu-id="50f99-126">키 위의 입구에 빨간색 표시기가 표시되지 않을 때까지 키를 시계 반대 방향으로 돌립니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="50f99-127">키를 꺼냅니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-127">Remove the key.</span></span>
   
    ![잠금 해제된 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="50f99-129">**그림 2** 잠금 해제된 디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="50f99-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="50f99-130">이제 디스크 드라이브를 꺼낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="50f99-131">잠금을 사용하려면 단계를 역순으로 따르세요.</span><span class="sxs-lookup"><span data-stu-id="50f99-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="50f99-132">디스크 드라이브 꺼내기</span><span class="sxs-lookup"><span data-stu-id="50f99-132">Remove the disk drive</span></span>
<span data-ttu-id="50f99-133">StorSimple 장치는 RAID 10과 유사한 저장소 공간 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="50f99-134">이는 오류가 발생한 하나의 디스크, SSD(반도체 드라이브) 또는 HDD(하드 디스크 드라이브)에서 정상적으로 작동할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="50f99-135">시스템에 오류가 발생한 디스크가 둘 이상 있는 경우 항상 시스템에서 SSD 또는 HDD를 둘 이상 꺼내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="50f99-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="50f99-136">이렇게 하면 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="50f99-137">이전에 SSD가 포함된 슬롯에는 교체 SSD를 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="50f99-138">마찬가지로, 이전에 HDD가 포함된 슬롯에는 교체 HDD를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="50f99-139">Azure Portal에서 슬롯에는 0 – 11 사이의 번호가 매겨져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-139">In the Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="50f99-140">따라서 포털에 슬롯 2의 디스크에서 오류가 발생했다고 표시되면 장치 왼쪽 위에서 세 번째 슬롯에서 오류가 발생한 디스크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="50f99-141">시스템 작동하는 동안 드라이브를 꺼내고 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="50f99-142">드라이브를 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="50f99-142">To remove a drive</span></span>
1. <span data-ttu-id="50f99-143">실패한 디스크를 식별하려면 Azure Portal에서 장치의 **설정 > 하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-143">To identify the failed disk, in the Azure portal, go to your device **Settings > Hardware health**.</span></span> <span data-ttu-id="50f99-144">기본 엔클로저 및/또는 EBOD 엔클로저에서 디스크 오류가 발생할 수 있으므로(8600 모델을 사용하는 경우) **공유 구성 요소** 및 **EBOD 공유 구성 요소** 아래에서 디스크 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="50f99-145">엔클로저 중 하나에서 오류가 발생한 디스크는 빨간색 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="50f99-146">기본 엔클로저 또는 EBOD 엔클로저 앞에 있는 드라이브를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="50f99-147">디스크가 잠금 해제된 경우 다음 단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="50f99-148">디스크가 잠긴 경우 [조작 방지 잠금 해제](#disengage-the-antitamper-lock)의 절차에 따라 잠금 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="50f99-149">드라이브 캐리어 모듈의 검은색 래치를 누르고 섀시 앞에서 드라이브 캐리어 핸들을 밖으로 잡아당깁니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span>
   
    ![디스크 드라이브 핸들 해제](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="50f99-151">**그림 3** 드라이브 핸들 해제</span><span class="sxs-lookup"><span data-stu-id="50f99-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="50f99-152">드라이브 캐리어 핸들이 완전히 확장되면 드라이브 캐리어를 섀시 밖으로 밉니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![디스크 드라이브 밖으로 디스크 밀기](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="50f99-154">**그림 4** 캐리어 밖으로 디스크 드라이브 밀기</span><span class="sxs-lookup"><span data-stu-id="50f99-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="50f99-155">교체 디스크 드라이브 설치</span><span class="sxs-lookup"><span data-stu-id="50f99-155">Install the replacement disk drive</span></span>
<span data-ttu-id="50f99-156">StorSimple 장치에서 드라이브 오류가 발생하고 드라이브를 꺼낸 후에 새 드라이브로 교체하려면 이 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="50f99-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="50f99-157">드라이브를 삽입하려면</span><span class="sxs-lookup"><span data-stu-id="50f99-157">To insert a drive</span></span>
1. <span data-ttu-id="50f99-158">다음 그림과 같이 드라이브 캐리어 핸들이 완전히 확장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![핸들이 확장된 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="50f99-160">**그림 5** 핸들이 확장된 드라이브</span><span class="sxs-lookup"><span data-stu-id="50f99-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="50f99-161">드라이브 캐리어를 섀시에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-161">Slide the drive carrier all the way into the chassis.</span></span>
   
    ![디스크 드라이브 캐리어 안으로 디스크 밀기](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="50f99-163">**그림 6** 섀시에 드라이브 캐리어 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="50f99-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="50f99-164">드라이브 캐리어를 삽입한 후 드라이브 캐리어 핸들이 잠긴 위치에 올 때까지 드라이브 캐리어를 섀시 안으로 계속 누르면서 드라이브 캐리어 핸들을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="50f99-165">Microsoft에서 제공한 잠금 키(조작 방지 Torx 드라이버)로 잠금 나사를 시계 방향으로 1/4 돌려 캐리어 핸들을 제자리에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="50f99-166">교체에 성공했고 드라이브가 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-166">Verify that the replacement was successful and the drive is operational.</span></span> <span data-ttu-id="50f99-167">Azure Portal에 액세스하고 **설정** > **하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-167">Access the Azure portal and navigate to **Settings** > **Hardware health**.</span></span> <span data-ttu-id="50f99-168">**공유 구성 요소** 또는 **EBOD 공유 구성 요소** 아래에서 드라이브 상태가 정상임을 나타내는 녹색이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-168">Under **Shared components** or **EBOD shared components**, the drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="50f99-169">교체 후 디스크 상태가 녹색으로 바뀌는 데 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-169">It may take several hours for the disk status to turn green after the replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="50f99-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50f99-170">Next steps</span></span>
<span data-ttu-id="50f99-171">[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="50f99-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

