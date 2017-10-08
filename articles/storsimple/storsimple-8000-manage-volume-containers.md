---
title: "aaaManage hello StorSimple 8000 시리즈 장치에 StorSimple 볼륨 컨테이너 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 볼륨 컨테이너 페이지 tooadd, 수정 또는 볼륨 컨테이너 삭제 hello를 사용 하는 방법에 대해 설명 합니다."
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
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="06fbc-103">Hello StorSimple 장치 관리자 서비스 toomanage StorSimple 볼륨 컨테이너를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="06fbc-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="06fbc-104">개요</span><span class="sxs-lookup"><span data-stu-id="06fbc-104">Overview</span></span>
<span data-ttu-id="06fbc-105">이 자습서에서는 toouse StorSimple 장치 관리자 서비스 toocreate hello 하 및 StorSimple 볼륨 컨테이너를 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="06fbc-106">Microsoft Azure StorSimple 장치의 볼륨 컨테이너는 저장소 계정, 암호화 및 대역폭 소비 설정을 공유하는 하나 이상의 볼륨을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="06fbc-107">장치는 모든 볼륨에 대해 여러 볼륨 컨테이너가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="06fbc-108">볼륨 컨테이너에는 hello 특성 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="06fbc-109">**볼륨** – hello 계층 또는 로컬로 hello 볼륨 컨테이너에 포함 된 StorSimple 볼륨을 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="06fbc-110">**암호화** -각 볼륨 컨테이너에 대해 암호화 키를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="06fbc-111">이 키는 StorSimple 장치 toohello 클라우드 보내지는 hello 데이터 암호화에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="06fbc-112">에 군용 수준의 a e S-256 비트 키 hello 사용자가 입력 한 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="06fbc-113">toosecure 데이터 권장 항상 클라우드 저장소 암호화 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="06fbc-114">**저장소 계정** – Azure 저장소 계정으로 사용 되는 toostore hello 데이터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="06fbc-115">볼륨 컨테이너에 있는 모든 hello 볼륨에는이 저장소 계정을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="06fbc-116">기존 목록에서 저장소 계정을 선택 하거나 hello 볼륨 컨테이너를 만들고 해당 계정에 대 한 hello 액세스 자격 증명을 지정 하는 경우 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="06fbc-117">**클라우드 대역폭** – hello 대역폭 hello 장치가 hello hello 장치에서 전송 된 데이터 toohello 클라우드 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="06fbc-118">이 컨테이너를 만드는 경우 1Mbps ~ 1000Mbps 사이의 값을 지정하여 대역폭 제어를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="06fbc-119">사용 가능한 모든 대역폭 hello 장치 tooconsume 하려는 경우이 필드 설정 너무**무제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="06fbc-120">만들고 및 일정에 따라 대역폭 템플릿 tooallocate 대역폭을 적용 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="06fbc-121">hello 다음 절차에서는 설명 방법을 toouse hello StorSimple **볼륨 컨테이너** 블레이드 toocomplete hello 일반적인 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="06fbc-122">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="06fbc-122">Add a volume container</span></span>
* <span data-ttu-id="06fbc-123">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="06fbc-123">Modify a volume container</span></span>
* <span data-ttu-id="06fbc-124">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="06fbc-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="06fbc-125">볼륨 컨테이너 추가</span><span class="sxs-lookup"><span data-stu-id="06fbc-125">Add a volume container</span></span>
<span data-ttu-id="06fbc-126">Hello 단계 tooadd 볼륨 컨테이너를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="06fbc-127">볼륨 컨테이너 수정</span><span class="sxs-lookup"><span data-stu-id="06fbc-127">Modify a volume container</span></span>
<span data-ttu-id="06fbc-128">Hello 단계 toomodify 볼륨 컨테이너를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="06fbc-129">볼륨 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="06fbc-129">Delete a volume container</span></span>
<span data-ttu-id="06fbc-130">볼륨 컨테이너 내에 볼륨이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-130">A volume container has volumes within it.</span></span> <span data-ttu-id="06fbc-131">에 포함 된 모든 hello 볼륨을 먼저 삭제 되는 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="06fbc-132">Hello 단계 toodelete 볼륨 컨테이너를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="06fbc-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06fbc-133">Next steps</span></span>
* <span data-ttu-id="06fbc-134">[StorSimple 볼륨 관리](storsimple-8000-manage-volumes-u2.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="06fbc-135">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06fbc-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

