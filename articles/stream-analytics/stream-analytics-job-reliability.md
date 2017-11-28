---
title: "Azure Stream Analytics 작업과 관련한 서비스 중단 방지 | Microsoft Docs"
description: "Stream Analytics 작업 업그레이드의 복원력을 높이기 위한 지침."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8dc19e1b37082c87d2990ad910d1af786f8b9280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="f466d-103">서비스 업데이트 도중 Stream Analytics 작업 안정성 보장</span><span class="sxs-lookup"><span data-stu-id="f466d-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="f466d-104">완전히 관리되는 서비스가 되는 방법 중 하나는 새로운 서비스 기능 및 향상 기능을 빠른 속도로 도입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="f466d-105">따라서 Stream Analytics는 매주(또는 더 자주) 서비스 업데이트 배포가 이루어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="f466d-106">얼마나 많은 테스트를 수행하든 관계없이 기존에 실행 중인 작업은 버그의 도입으로 인해 중단될 수 있는 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span></span> <span data-ttu-id="f466d-107">중요한 스트리밍 처리 작업을 실행하는 고객은 이러한 위험을 방지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span></span> <span data-ttu-id="f466d-108">고객이 이러한 위험을 줄이는 데 사용할 수 있는 메커니즘은 Azure의 **[지역 쌍](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="f466d-109">Azure 지역 쌍은 이러한 문제를 어떻게 해결할까요?</span><span class="sxs-lookup"><span data-stu-id="f466d-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="f466d-110">Stream Analytics는 지역 쌍의 작업이 별도의 일괄 처리로 업데이트되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="f466d-111">따라서 잠재적인 주요 버그를 식별하고 재구성하기 위해 업데이트 간에 충분 한 간격을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="f466d-112">Stream Analytics 업데이트 배포는 지역 쌍 집합에서 동시에 발생하지 않습니다. 단, 인도 남부가 지역 쌍이지만 Stream Analytics 상태가 없는 _인도 중부는 예외_입니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span></span> <span data-ttu-id="f466d-113">**동일한 그룹에 속하는** 여러 지역에서는 배포가 **동시에** 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span></span>

<span data-ttu-id="f466d-114">쌍을 이루는 지역에 대한 최신 정보는 **[가용성 및 쌍을 이루는 지역](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**에 대한 문서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="f466d-115">고객은 두 지역 쌍 모두에 동일한 작업을 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-115">Customers are advised to deploy identical jobs to both paired regions.</span></span> <span data-ttu-id="f466d-116">또한 고객은 Stream Analytics의 내부 모니터링 기능 외에도 작업이 **둘 다** 프로덕션 작업인 것처럼 모니터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span></span> <span data-ttu-id="f466d-117">중단이 발생한 이유가 Stream Analytics 서비스 업데이트 때문이라면 적절히 에스컬레이션하고 다운스트림 소비자를 정상 작업 출력으로 장애 조치(failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span></span> <span data-ttu-id="f466d-118">지원으로 에스컬레이션하면 지역 쌍이 새 배포의 영향을 받지 않게 되고 지역 쌍의 무결성이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f466d-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span></span>
