---
title: "StorSimple 8000 시리즈 장치에서 StorSimple 볼륨 컨테이너 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 볼륨 컨테이너 페이지를 사용하여 볼륨 컨테이너를 추가, 수정 또는 삭제하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 0f8e00d6d07224f56625482f339e612e68914be2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="8cefb-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 볼륨 컨테이너 관리</span><span class="sxs-lookup"><span data-stu-id="8cefb-103">Use the StorSimple Device Manager service to manage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="8cefb-104">개요</span><span class="sxs-lookup"><span data-stu-id="8cefb-104">Overview</span></span>
<span data-ttu-id="8cefb-105">이 자습서는 StorSimple 장치 관리자 서비스를 사용하여 StorSimple 볼륨 컨테이너를 만들고 관리하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="8cefb-106">Microsoft Azure StorSimple 장치의 볼륨 컨테이너는 저장소 계정, 암호화 및 대역폭 소비 설정을 공유하는 하나 이상의 볼륨을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="8cefb-107">장치는 모든 볼륨에 대해 여러 볼륨 컨테이너가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="8cefb-108">볼륨 컨테이너에는 다음 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="8cefb-109">**볼륨** – 볼륨 컨테이너 내에 포함된 계층화되거나 로컬로 고정된 StorSimple 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> 
* <span data-ttu-id="8cefb-110">**암호화** -각 볼륨 컨테이너에 대해 암호화 키를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="8cefb-111">이 키는 StorSimple 장치에서 클라우드로 전송되는 데이터를 암호화하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-111">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="8cefb-112">군사 등급 AES 256 비트 키는 사용자가 입력한 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-112">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="8cefb-113">데이터를 보호하려면 항상 클라우드 저장소 암호화를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-113">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="8cefb-114">**저장소 계정** – 데이터를 저장하는 데 사용되는 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-114">**Storage account** – The Azure storage account that is used to store the data.</span></span> <span data-ttu-id="8cefb-115">볼륨 컨테이너에 있는 모든 볼륨은 이 저장소 계정을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-115">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="8cefb-116">기존 목록에서 저장소 계정을 선택하거나 볼륨 컨테이너를 만들고 해당 계정에 대한 액세스 자격 증명을 지정하는 경우 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-116">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="8cefb-117">**클라우드 대역폭** – 데이터가 장치에서 클라우드로 전송될 때 장치에서 소비되는 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-117">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="8cefb-118">이 컨테이너를 만드는 경우 1Mbps ~ 1000Mbps 사이의 값을 지정하여 대역폭 제어를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="8cefb-119">장치에서 사용 가능한 모든 대역폭 사용을 원하는 경우 이 필드를 **무제한**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-119">If you want the device to consume all available bandwidth, set this field to **Unlimited**.</span></span> <span data-ttu-id="8cefb-120">일정에 따라 대역폭을 할당하도록 대역폭 서식 파일을 만들어 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-120">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

<span data-ttu-id="8cefb-121">다음 이 절차는 StorSimple **볼륨 컨테이너** 블레이드를 사용하여 다음 일반적인 작업을 완료하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-121">The following procedures explain how to use the StorSimple **Volume containers** blade to complete the following common operations:</span></span>

* <span data-ttu-id="8cefb-122">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="8cefb-122">Add a volume container</span></span>
* <span data-ttu-id="8cefb-123">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="8cefb-123">Modify a volume container</span></span>
* <span data-ttu-id="8cefb-124">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="8cefb-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="8cefb-125">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="8cefb-125">Add a volume container</span></span>
<span data-ttu-id="8cefb-126">볼륨 컨테이너를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-126">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="8cefb-127">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="8cefb-127">Modify a volume container</span></span>
<span data-ttu-id="8cefb-128">볼륨 컨테이너를 수정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-128">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="8cefb-129">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="8cefb-129">Delete a volume container</span></span>
<span data-ttu-id="8cefb-130">볼륨 컨테이너 내에 볼륨이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-130">A volume container has volumes within it.</span></span> <span data-ttu-id="8cefb-131">안에 포함된 모든 볼륨이 먼저 삭제되는 경우에만 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-131">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="8cefb-132">볼륨 컨테이너를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-132">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="8cefb-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8cefb-133">Next steps</span></span>
* <span data-ttu-id="8cefb-134">[StorSimple 볼륨 관리](storsimple-8000-manage-volumes-u2.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="8cefb-135">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8cefb-135">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

