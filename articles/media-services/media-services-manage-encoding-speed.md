---
title: "Azure Media Services를 사용하여 인코딩의 속도 및 동시성 관리 | Microsoft Docs"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="fff3b-103">인코딩 속도 및 동시성 관리</span><span class="sxs-lookup"><span data-stu-id="fff3b-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="fff3b-104">이 문서에서는 인코딩 작업/태스크의 속도 및 동시성 관리하는 방법에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="fff3b-105">개요</span><span class="sxs-lookup"><span data-stu-id="fff3b-105">Overview</span></span>

<span data-ttu-id="fff3b-106">Media Services에서 **예약 단위 유형**은 미디어 처리 태스크를 처리하는 속도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="fff3b-107">**S1**, **S2**, **S3** 예약 단위 유형 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="fff3b-108">예를 들어 **S2** 예약 단위 유형을 사용하는 경우 **S1** 유형에 비해 동일한 인코딩 작업이 더 빠르게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="fff3b-109">[인코딩 단위 크기 조정](media-services-scale-media-processing-overview.md) 항목에서는 여러 인코딩 속도를 선택할 때 적절한 속도를 결정할 수 있도록 하는 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="fff3b-110">예약 단위 유형을 지정하는 것 외에도 계정에 **예약 단위**를 프로비전하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="fff3b-111">프로비전되는 예약 단위의 수에 따라 특정 계정에서 동시에 처리할 수 있는 미디어 작업의 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="fff3b-112">예를 들어 계정에 5개의 예약 단위가 있는 경우 처리할 작업이 있다면 5개의 미디어 작업이 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="fff3b-113">나머지 작업은 큐에 대기하다가 실행 중인 작업이 완료되면 순차적으로 처리를 위해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="fff3b-114">계정에 프로비전된 예약 단위가 없는 경우에는 작업이 순차적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="fff3b-115">이 경우 한 작업 완료와 다음 작업 시작 사이의 대기 시간은 시스템의 리소스 가용성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fff3b-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="fff3b-116">인코딩 단위의 크기를 조정하는 방법을 보여 주는 자세한 정보 및 예제는 [이](media-services-scale-media-processing-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fff3b-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="fff3b-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fff3b-117">Next step</span></span>

[<span data-ttu-id="fff3b-118">인코딩 단위 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fff3b-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="fff3b-119">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="fff3b-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fff3b-120">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="fff3b-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

