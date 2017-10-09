---
title: "StorSimple 8000 시리즈 장치에 섀시 aaaReplace | Microsoft Docs"
description: "Tooremove 및 바꾸기 StorSimple 기본 인클로저 또는 EBOD 인클로저 섀시 hello 방법을 설명 합니다."
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
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="df66b-103">StorSimple 장치에 hello 섀시 교체</span><span class="sxs-lookup"><span data-stu-id="df66b-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="df66b-104">개요</span><span class="sxs-lookup"><span data-stu-id="df66b-104">Overview</span></span>
<span data-ttu-id="df66b-105">이 자습서에 설명 어떻게 tooremove StorSimple 8000 시리즈 장치에 섀시를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="df66b-106">StorSimple 8100 hello 모델 반면 hello 8600 이중 인클로저 장치 (두 개의 섀시)는 단일 인클로저 장치 (하나의 섀시)은입니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="df66b-107">8600 모델의 경우는 hello 장치에서 장애 사용할 수 있는 두 개의 섀시 잠재적으로: hello 기본 인클로저의 섀시 또는 EBOD 인클로저의 hello에 대 한 hello 섀시 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="df66b-108">어떤 경우 든 Microsoft에서 제공 되는 hello 교체 섀시 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="df66b-109">PCM(전원 및 냉각 모듈), 컨트롤러 모듈, SSD(반도체 디스크 드라이브), HDD(하드 디스크 드라이브) 또는 EBOD 모듈은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df66b-110">분리 및 교체 hello 섀시 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-chassis"></a><span data-ttu-id="df66b-111">Hello 섀시를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-111">Remove hello chassis</span></span>
<span data-ttu-id="df66b-112">Hello 단계 tooremove hello 섀시 StorSimple 장치에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="df66b-113">tooremove 섀시</span><span class="sxs-lookup"><span data-stu-id="df66b-113">tooremove a chassis</span></span>
1. <span data-ttu-id="df66b-114">Hello StorSimple 장치 종료 되 고 모든 hello 전원에서 연결이 해제 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="df66b-115">해당 하는 경우 모든 hello 네트워크 및 SAS 케이블을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="df66b-116">Hello 랙에서 hello 단위를 제거 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df66b-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="df66b-117">각 hello 드라이브를 제거 하 고 제거 되는 hello 슬롯을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="df66b-118">자세한 내용은 참조 [hello 디스크 드라이브를 제거](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive)합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-118">For more information, see [Remove hello disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="df66b-119">Hello EBOD 인클로저 (hello 발생 한 섀시 인 경우), hello EBOD 컨트롤러 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="df66b-120">자세한 내용은 [EBOD 컨트롤러 꺼내기](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df66b-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="df66b-121">Hello에 기본 인클로저 (hello 발생 한 섀시 인 경우) hello 컨트롤러를 제거 하 고 확인 hello 슬롯 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="df66b-122">자세한 내용은 [컨트롤러 꺼내기](storsimple-8000-controller-replacement.md#remove-a-controller)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df66b-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="df66b-123">Hello 섀시를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-123">Install hello chassis</span></span>
<span data-ttu-id="df66b-124">Hello 단계 tooinstall hello 섀시 StorSimple 장치에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="df66b-125">tooinstall 섀시</span><span class="sxs-lookup"><span data-stu-id="df66b-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="df66b-126">Hello 섀시 hello 랙에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="df66b-127">자세한 내용은 [StorSimple 8100 장치 랙 탑재](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) 또는 [StorSimple 8600 장치 랙 탑재](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df66b-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="df66b-128">Hello 섀시, hello 랙에 탑재 한 후에 이전에 설치한에 배치 동일 hello hello 컨트롤러 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="df66b-129">설치 hello는 이전에 설치한에 배치 하 고 슬롯이 동일한 hello에서 구동 합니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="df66b-130">Hello Ssd hello 슬롯을 먼저 설치 하 고 다음 hello Hdd를 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
  
4. <span data-ttu-id="df66b-131">Hello 사용 hello 랙에 장치 탑재 및 hello 구성 요소를 설치 하 고, 사용자 장치 toohello 적절 한 전원에 연결 하 고 hello 장치를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="df66b-132">자세한 내용은 [StorSimple 8100 장치 케이블 연결](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) 또는 [StorSimple 8600 장치 케이블 연결](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df66b-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="df66b-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df66b-133">Next steps</span></span>
<span data-ttu-id="df66b-134">[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="df66b-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

