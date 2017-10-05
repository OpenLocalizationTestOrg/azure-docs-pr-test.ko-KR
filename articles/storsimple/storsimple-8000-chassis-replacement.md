---
title: "StorSimple 8000 시리즈 장치의 섀시 교체 | Microsoft Docs"
description: "StorSimple 기본 엔클로저 또는 EBOD 엔클로저에 섀시를 꺼내고 교체하는 방법을 설명합니다."
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 073fcf0064f1d1482f4683d733f00cf918ff2f38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="e6267-103">StorSimple 장치의 섀시 교체</span><span class="sxs-lookup"><span data-stu-id="e6267-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="e6267-104">개요</span><span class="sxs-lookup"><span data-stu-id="e6267-104">Overview</span></span>
<span data-ttu-id="e6267-105">이 자습서에서는 StorSimple 8000 시리즈 장치의 섀시를 꺼내고 교체하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="e6267-106">StorSimple 8100 모델은 단일 엔클로저 장치(섀시 1개)인 반면 8600은 이중 엔클로저 장치(섀시 2개)입니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="e6267-107">8600 모델의 경우 장치에 오류가 발생할 수 있는 두 개의 섀시(기본 엔클로저용 섀시 또는 EBOD 엔클로저용 섀시)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="e6267-108">두 경우 모두 Microsoft에서 제공한 교체 섀시가 비게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="e6267-109">PCM(전원 및 냉각 모듈), 컨트롤러 모듈, SSD(반도체 디스크 드라이브), HDD(하드 디스크 드라이브) 또는 EBOD 모듈은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6267-110">섀시를 꺼내고 교체하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에서 안전 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-chassis"></a><span data-ttu-id="e6267-111">섀시 꺼내기</span><span class="sxs-lookup"><span data-stu-id="e6267-111">Remove the chassis</span></span>
<span data-ttu-id="e6267-112">StorSimple 장치의 섀시를 꺼내려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="e6267-113">섀시를 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="e6267-113">To remove a chassis</span></span>
1. <span data-ttu-id="e6267-114">StorSimple 장치가 종료되고 모든 전원에서 연결이 끊어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="e6267-115">해당하는 경우 모든 네트워크 및 SAS 케이블을 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="e6267-116">랙에서 장치를 꺼냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="e6267-117">각 드라이브를 꺼내고 들어 있던 슬롯을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="e6267-118">자세한 내용은 [디스크 드라이브 꺼내기](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-118">For more information, see [Remove the disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="e6267-119">EBOD 엔클로저에서(이 섀시에서 오류가 발생한 경우) EBOD 컨트롤러 모듈을 꺼냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="e6267-120">자세한 내용은 [EBOD 컨트롤러 꺼내기](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="e6267-121">기본 엔클로저에서(이 섀시에서 오류가 발생한 경우) 컨트롤러를 꺼내고 들어 있던 슬롯을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="e6267-122">자세한 내용은 [컨트롤러 꺼내기](storsimple-8000-controller-replacement.md#remove-a-controller)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="e6267-123">섀시 설치</span><span class="sxs-lookup"><span data-stu-id="e6267-123">Install the chassis</span></span>
<span data-ttu-id="e6267-124">StorSimple 장치에 섀시를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="e6267-125">섀시를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="e6267-125">To install a chassis</span></span>
1. <span data-ttu-id="e6267-126">섀시를 랙에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="e6267-127">자세한 내용은 [StorSimple 8100 장치 랙 탑재](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) 또는 [StorSimple 8600 장치 랙 탑재](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="e6267-128">섀시를 랙에 탑재한 후 이전에 설치된 곳과 동일한 위치에 컨트롤러 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="e6267-129">이전에 설치된 곳과 동일한 위치 및 슬롯에 드라이브를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e6267-130">SSD를 먼저 슬롯에 설치한 다음 HDD를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
  
4. <span data-ttu-id="e6267-131">장치를 랙에 탑재하고 구성 요소를 설치한 후 장치를 해당 전원에 연결하고 장치를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="e6267-132">자세한 내용은 [StorSimple 8100 장치 케이블 연결](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) 또는 [StorSimple 8600 장치 케이블 연결](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6267-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6267-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6267-133">Next steps</span></span>
<span data-ttu-id="e6267-134">[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6267-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

