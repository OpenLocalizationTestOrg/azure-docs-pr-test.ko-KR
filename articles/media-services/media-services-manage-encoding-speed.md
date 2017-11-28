---
title: "aaa 관리 속도 및 동시성은 Azure 미디어 서비스로 인코딩 | Microsoft Docs"
description: "이 문서에서는 Azure Media Services를 사용하여 인코딩 작업/태스크의 속도 및 동시성을 관리하는 방법에 대해 간략하게 설명합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="549bb-103">인코딩 속도 및 동시성 관리</span><span class="sxs-lookup"><span data-stu-id="549bb-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="549bb-104">이 문서에서는 인코딩 작업/태스크의 속도 및 동시성 관리하는 방법에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="549bb-105">개요</span><span class="sxs-lookup"><span data-stu-id="549bb-105">Overview</span></span>

<span data-ttu-id="549bb-106">미디어 서비스에서는 **예약 단위 형식** 처리 되는 작업을 처리 하 여 미디어는 hello 속도 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="549bb-107">Hello 다음 중에서 선택할 수 예약 단위 형식: **S1**, **S2**, 또는 **S3**합니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="549bb-108">Hello를 사용할 때 동일한 인코딩 작업이 더 빠르게 실행 하는 hello 예를 들어 **S2** toohello 비교 하는 예약된 단위 형식 **S1** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="549bb-109">hello [인코딩 단위 배율](media-services-scale-media-processing-overview.md) 항목에서는 다양 한 인코딩 속도 선택할 때 결정을 내릴 수 있도록 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="549bb-110">또한 toospecifying hello 예약 단위 형식, tooprovision를 사용 하 여 계정을 지정할 수 있습니다 **예약 단위**합니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="549bb-111">제공된 된 예약된 단위 수가 hello hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="549bb-112">예를 들어 5 개의 미디어 작업이 동시에 실행 될 다음 사용자 계정에 5 명의 예약된 단위 같이 많은 경우 작업 toobe 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="549bb-113">hello 남은 작업이 hello 큐에서 대기 하 고 실행 중인 작업이 완료 되는 경우 순차적으로 처리 하도록 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="549bb-114">계정에 프로비전된 예약 단위가 없는 경우에는 작업이 순차적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="549bb-115">이 경우 hello 한 작업 완료 사이의 시간 기다렸다가 hello 다음 시작에 따라 달라 집니다 리소스의 hello 가용성 hello 시스템.</span><span class="sxs-lookup"><span data-stu-id="549bb-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="549bb-116">자세한 내용 및 예제에 대 한 tooscale 인코딩 단위 참조 하는 방법을 보여 주는 [이](media-services-scale-media-processing-overview.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="549bb-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="549bb-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="549bb-117">Next step</span></span>

[<span data-ttu-id="549bb-118">인코딩 단위 크기 조정</span><span class="sxs-lookup"><span data-stu-id="549bb-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="549bb-119">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="549bb-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="549bb-120">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="549bb-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

