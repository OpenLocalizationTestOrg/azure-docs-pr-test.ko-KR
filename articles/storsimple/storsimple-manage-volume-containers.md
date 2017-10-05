---
title: "StorSimple 볼륨 컨테이너 관리 | Microsoft Docs"
description: "StorSimple Manager 서비스 볼륨 컨테이너 페이지를 사용하여 볼륨 컨테이너를 추가, 수정 또는 삭제하는 방법을 설명합니다."
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
ms.openlocfilehash: bb55a7a4bff0fd4319de6f6ce958686ad8a4142b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="74734-103">StorSimple 관리자 서비스를 사용하여 StorSimple 볼륨 컨테이너 관리</span><span class="sxs-lookup"><span data-stu-id="74734-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="74734-104">개요</span><span class="sxs-lookup"><span data-stu-id="74734-104">Overview</span></span>
<span data-ttu-id="74734-105">이 자습서는 StorSimple 관리자 서비스를 사용하여 StorSimple 볼륨 컨테이너를 만들고 관리하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="74734-106">Microsoft Azure StorSimple 장치의 볼륨 컨테이너는 저장소 계정, 암호화 및 대역폭 소비 설정을 공유하는 하나 이상의 볼륨을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="74734-107">장치는 모든 볼륨에 대해 여러 볼륨 컨테이너가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="74734-108">볼륨 컨테이너에는 다음 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="74734-109">**볼륨** – 볼륨 컨테이너 내에 포함된 계층화되거나 로컬로 고정된 StorSimple 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="74734-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="74734-110">볼륨 컨테이너는 최대 256개의 StorSimple 볼륨을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="74734-111">**암호화** -각 볼륨 컨테이너에 대해 암호화 키를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="74734-112">이 키는 StorSimple 장치에서 클라우드로 전송되는 데이터를 암호화하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74734-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="74734-113">군사 등급 AES 256 비트 키는 사용자가 입력한 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74734-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="74734-114">데이터를 보호하려면 항상 클라우드 저장소 암호화를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="74734-115">**저장소 계정** – 클라우드 저장소 서비스 공급자에 연결된 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="74734-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="74734-116">볼륨 컨테이너에 있는 모든 볼륨은 이 저장소 계정을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="74734-117">기존 목록에서 저장소 계정을 선택하거나 볼륨 컨테이너를 만들고 해당 계정에 대한 액세스 자격 증명을 지정하는 경우 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="74734-118">**클라우드 대역폭** – 데이터가 장치에서 클라우드로 전송될 때 장치에서 소비되는 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="74734-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="74734-119">이 컨테이너를 정의하는 경우 1 ~ 1000mbps 사이의 값을 지정하여 대역폭 제어를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="74734-120">장치에서 사용 가능한 모든 대역폭 사용을 원하는 경우 이 필드를 무제한으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="74734-121">일정에 따라 대역폭을 할당하도록 대역폭 서식 파일을 만들어 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![볼륨 컨테이너 페이지](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="74734-123">다음 이 절차는 StorSimple **볼륨 컨테이너** 페이지를 사용하여 다음 일반적인 작업을 완료하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="74734-124">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="74734-124">Add a volume container</span></span> 
* <span data-ttu-id="74734-125">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="74734-125">Modify a volume container</span></span> 
* <span data-ttu-id="74734-126">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="74734-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="74734-127">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="74734-127">Add a volume container</span></span>
<span data-ttu-id="74734-128">볼륨 컨테이너를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="74734-129">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="74734-129">Modify a volume container</span></span>
<span data-ttu-id="74734-130">볼륨 컨테이너를 수정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="74734-131">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="74734-131">Delete a volume container</span></span>
<span data-ttu-id="74734-132">볼륨 컨테이너 내에 볼륨이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-132">A volume container has volumes within it.</span></span> <span data-ttu-id="74734-133">안에 포함된 모든 볼륨이 먼저 삭제되는 경우에만 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74734-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="74734-134">볼륨 컨테이너를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74734-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="74734-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74734-135">Next steps</span></span>
* <span data-ttu-id="74734-136">[StorSimple 볼륨 관리](storsimple-manage-volumes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74734-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="74734-137">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74734-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

