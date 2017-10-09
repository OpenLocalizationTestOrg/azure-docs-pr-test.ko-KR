---
title: "Azure Vm tooan 기존 가용성 집합을 추가 하는 aaaSupportability | Microsoft Docs"
description: "Azure Vm tooan 기존 가용성 집합을 추가 하는 지원 가능성을 고려 합니다."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="5be80-103">Azure Vm tooan 기존 가용성 집합을 추가 하는 지원 가능성</span><span class="sxs-lookup"><span data-stu-id="5be80-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="5be80-104">제한 사항 새 가상 컴퓨터 (Vm) tooan 기존 가용성 집합을 추가 하는 경우에 가끔 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be80-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="5be80-105">다음 차트 세부 정보에서 혼합할 수 있는 VM 시리즈 hello 동일한 가용성 집합 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="5be80-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="5be80-106">Hello 지원 가능성 매트릭스 toomix 다양 한 유형의 Vm 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5be80-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="5be80-107">시리즈 및 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="5be80-107">Series & Availability Set</span></span>|<span data-ttu-id="5be80-108">두 번째 VM</span><span class="sxs-lookup"><span data-stu-id="5be80-108">Second VM</span></span>|<span data-ttu-id="5be80-109">A</span><span class="sxs-lookup"><span data-stu-id="5be80-109">A</span></span>|<span data-ttu-id="5be80-110">Av2</span><span class="sxs-lookup"><span data-stu-id="5be80-110">Av2</span></span>|<span data-ttu-id="5be80-111">D</span><span class="sxs-lookup"><span data-stu-id="5be80-111">D</span></span>|<span data-ttu-id="5be80-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="5be80-112">Dv2</span></span>|<span data-ttu-id="5be80-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="5be80-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="5be80-114">첫 번째 VM</span><span class="sxs-lookup"><span data-stu-id="5be80-114">First VM</span></span>|||||||
|<span data-ttu-id="5be80-115">A</span><span class="sxs-lookup"><span data-stu-id="5be80-115">A</span></span>||<span data-ttu-id="5be80-116">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-116">OK</span></span>|<span data-ttu-id="5be80-117">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-117">OK</span></span>|<span data-ttu-id="5be80-118">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-118">OK</span></span>|<span data-ttu-id="5be80-119">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-119">OK</span></span>|<span data-ttu-id="5be80-120">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-120">OK</span></span>|
|<span data-ttu-id="5be80-121">Av2</span><span class="sxs-lookup"><span data-stu-id="5be80-121">Av2</span></span>||<span data-ttu-id="5be80-122">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-122">OK</span></span>|<span data-ttu-id="5be80-123">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-123">OK</span></span>|<span data-ttu-id="5be80-124">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-124">OK</span></span>|<span data-ttu-id="5be80-125">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-125">OK</span></span>|<span data-ttu-id="5be80-126">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-126">OK</span></span>|
|<span data-ttu-id="5be80-127">D</span><span class="sxs-lookup"><span data-stu-id="5be80-127">D</span></span>||<span data-ttu-id="5be80-128">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-128">OK</span></span>|<span data-ttu-id="5be80-129">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-129">OK</span></span>|<span data-ttu-id="5be80-130">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-130">OK</span></span>|<span data-ttu-id="5be80-131">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-131">OK</span></span>|<span data-ttu-id="5be80-132">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-132">OK</span></span>|
|<span data-ttu-id="5be80-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="5be80-133">Dv2</span></span>||<span data-ttu-id="5be80-134">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-134">OK</span></span>|<span data-ttu-id="5be80-135">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-135">OK</span></span>|<span data-ttu-id="5be80-136">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-136">OK</span></span>|<span data-ttu-id="5be80-137">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-137">OK</span></span>|<span data-ttu-id="5be80-138">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-138">OK</span></span>|
|<span data-ttu-id="5be80-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="5be80-139">Dv3</span></span>||<span data-ttu-id="5be80-140">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-140">OK</span></span>|<span data-ttu-id="5be80-141">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-141">OK</span></span>|<span data-ttu-id="5be80-142">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-142">OK</span></span>|<span data-ttu-id="5be80-143">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-143">OK</span></span>|<span data-ttu-id="5be80-144">확인</span><span class="sxs-lookup"><span data-stu-id="5be80-144">OK</span></span>|

<span data-ttu-id="5be80-145">다른 모든 계열이 hello 특정 하드웨어 필요 하기 때문에 동일한 가용성 집합의 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5be80-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
