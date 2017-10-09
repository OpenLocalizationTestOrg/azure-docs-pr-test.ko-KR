---
title: "aaaScheduler 제한 및 기본값"
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
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="8dbed-103">스케줄러 제한 및 기본값</span><span class="sxs-lookup"><span data-stu-id="8dbed-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="8dbed-104">스케줄러 할당량, 제한, 기본값 및 한계</span><span class="sxs-lookup"><span data-stu-id="8dbed-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="8dbed-105">ms 요청 id x hello 헤더</span><span class="sxs-lookup"><span data-stu-id="8dbed-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="8dbed-106">라는 응답 헤더를 반환 하는 hello 스케줄러 서비스에 대 한 모든 요청**ms 요청 id x**합니다. 이 헤더는 hello 요청을 고유 하 게 식별 하는 불투명 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbed-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="8dbed-107">지속적으로 요청은 실패 하 고 hello 요청이 공식화 제대로 되,이 값 tooreport hello 오류 tooMicrosoft를 사용할 수 있습니다 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbed-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="8dbed-108">보고서에서 u e x-ms-id, hello 대략적인 시간 hello 값 hello 구독, 작업 컬렉션 및/또는 작업의 식별자를 hello 및 hello 시도 하는 요청 된 작업 유형을 hello에 해당 hello 요청이 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbed-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="8dbed-109">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8dbed-109">See Also</span></span>
 [<span data-ttu-id="8dbed-110">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="8dbed-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="8dbed-111">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="8dbed-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="8dbed-112">Hello Azure 포털에서에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="8dbed-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="8dbed-113">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="8dbed-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="8dbed-114">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="8dbed-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="8dbed-115">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="8dbed-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="8dbed-116">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="8dbed-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="8dbed-117">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="8dbed-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

