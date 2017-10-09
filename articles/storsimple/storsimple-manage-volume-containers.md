---
title: "aaaManage StorSimple 볼륨 컨테이너 | Microsoft Docs"
description: "StorSimple Manager 서비스 볼륨 컨테이너 페이지 tooadd, 수정 또는 볼륨 컨테이너 삭제 hello를 사용 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="cedba-103">Hello StorSimple 관리자 서비스 toomanage StorSimple 볼륨 컨테이너를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cedba-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="cedba-104">개요</span><span class="sxs-lookup"><span data-stu-id="cedba-104">Overview</span></span>
<span data-ttu-id="cedba-105">이 자습서에서는 toouse StorSimple 관리자 서비스 toocreate hello 하 및 StorSimple 볼륨 컨테이너를 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="cedba-106">Microsoft Azure StorSimple 장치의 볼륨 컨테이너는 저장소 계정, 암호화 및 대역폭 소비 설정을 공유하는 하나 이상의 볼륨을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="cedba-107">장치는 모든 볼륨에 대해 여러 볼륨 컨테이너가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="cedba-108">볼륨 컨테이너에는 hello 특성 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="cedba-109">**볼륨** – hello 계층 또는 로컬로 hello 볼륨 컨테이너에 포함 된 StorSimple 볼륨을 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="cedba-110">볼륨 컨테이너는 too256 StorSimple 볼륨을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="cedba-111">**암호화** -각 볼륨 컨테이너에 대해 암호화 키를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="cedba-112">이 키는 StorSimple 장치 toohello 클라우드 보내지는 hello 데이터 암호화에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="cedba-113">에 군용 수준의 a e S-256 비트 키 hello 사용자가 입력 한 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="cedba-114">toosecure 데이터 권장 항상 클라우드 저장소 암호화 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="cedba-115">**저장소 계정** – 저장소 계정을 연결 된 tooyour 클라우드 저장소 서비스 공급자 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="cedba-116">볼륨 컨테이너에 있는 모든 hello 볼륨에는이 저장소 계정을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="cedba-117">기존 목록에서 저장소 계정을 선택 하거나 hello 볼륨 컨테이너를 만들고 해당 계정에 대 한 hello 액세스 자격 증명을 지정 하는 경우 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="cedba-118">**클라우드 대역폭** – hello 대역폭 hello 장치가 hello hello 장치에서 전송 된 데이터 toohello 클라우드 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="cedba-119">이 컨테이너를 정의하는 경우 1 ~ 1000mbps 사이의 값을 지정하여 대역폭 제어를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="cedba-120">사용 가능한 모든 대역폭 hello 장치 tooconsume 하려는 경우이 필드 tooUnlimited를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="cedba-121">만들고 및 일정에 따라 대역폭 템플릿 tooallocate 대역폭을 적용 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![볼륨 컨테이너 페이지](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="cedba-123">이 다음 절차에서는 toouse StorSimple hello 하는 방법을 설명 **볼륨 컨테이너** 페이지 toocomplete hello 일반적인 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="cedba-124">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="cedba-124">Add a volume container</span></span> 
* <span data-ttu-id="cedba-125">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="cedba-125">Modify a volume container</span></span> 
* <span data-ttu-id="cedba-126">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="cedba-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="cedba-127">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="cedba-127">Add a volume container</span></span>
<span data-ttu-id="cedba-128">Hello 단계 tooadd 볼륨 컨테이너를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="cedba-129">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="cedba-129">Modify a volume container</span></span>
<span data-ttu-id="cedba-130">Hello 단계 toomodify 볼륨 컨테이너를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="cedba-131">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="cedba-131">Delete a volume container</span></span>
<span data-ttu-id="cedba-132">볼륨 컨테이너 내에 볼륨이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-132">A volume container has volumes within it.</span></span> <span data-ttu-id="cedba-133">에 포함 된 모든 hello 볼륨을 먼저 삭제 되는 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="cedba-134">Hello 단계 toodelete 볼륨 컨테이너를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="cedba-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cedba-135">Next steps</span></span>
* <span data-ttu-id="cedba-136">[StorSimple 볼륨 관리](storsimple-manage-volumes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="cedba-137">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cedba-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

