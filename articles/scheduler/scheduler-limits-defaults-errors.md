---
title: "스케줄러 제한 및 기본값"
description: "스케줄러 제한 및 기본값"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="00b14-103">스케줄러 제한 및 기본값</span><span class="sxs-lookup"><span data-stu-id="00b14-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="00b14-104">스케줄러 할당량, 제한, 기본값 및 한계</span><span class="sxs-lookup"><span data-stu-id="00b14-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="00b14-105">x-ms-request-id 헤더</span><span class="sxs-lookup"><span data-stu-id="00b14-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="00b14-106">스케줄러 서비스에 대한 모든 요청에서는 이름이**x-ms-request-id**인 응답 헤더를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="00b14-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="00b14-107">이 헤더는 요청을 고유하게 식별하는 불투명 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00b14-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="00b14-108">요청이 계속 실패하고 해당 요청이 제대로 구성되었음을 확인한 경우 이 값을 사용하여 오류를 Microsoft에 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00b14-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="00b14-109">보고서에는 x-ms-request-id 값, 요청을 수행한 대략적인 시간, 구독 식별자, 작업 컬렉션 및/또는 작업, 요청이 시도한 작업 유형을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00b14-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="00b14-110">참고 항목</span><span class="sxs-lookup"><span data-stu-id="00b14-110">See Also</span></span>
 [<span data-ttu-id="00b14-111">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="00b14-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="00b14-112">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="00b14-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="00b14-113">Azure 포털에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="00b14-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="00b14-114">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="00b14-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="00b14-115">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="00b14-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="00b14-116">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="00b14-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="00b14-117">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="00b14-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="00b14-118">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="00b14-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

