---
ms.assetid: 
title: "Azure Key Vault 제한 지침 | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="12bc4-102">Azure Key Vault 제한 지침</span><span class="sxs-lookup"><span data-stu-id="12bc4-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="12bc4-103">제한은 리소스의 과용을 방지하기 위해 Azure 서비스에 대한 동시 호출 수를 제한하는 사용자 시작 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="12bc4-104">Azure Key Vault(AKV)는 많은 양의 요청을 처리하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="12bc4-105">매우 많은 수의 요청이 발생할 경우 클라이언트의 요청을 제한하면 AKV 서비스의 최적의 성능 및 안정성을 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="12bc4-106">제한 한도는 시나리오에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="12bc4-107">예를 들어, 대용량 쓰기를 수행하는 경우 읽기만 수행하는 경우보다 제한 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="12bc4-108">Key Vault가 한도를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="12bc4-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="12bc4-109">Key Vault의 서비스 한도는 리소스의 오용을 방지하고 모든 Key Vault 클라이언트의 서비스 품질을 보장하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="12bc4-110">서비스 임계값이 초과되면 Key Vault가 해당 클라이언트에서 들어오는 추가 요청을 일정 시간 동안 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="12bc4-111">이 경우 Key Vault는 HTTP 상태 코드 429(너무 많은 요청)를 반환하고 요청은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="12bc4-112">또한 429를 반환한 실패한 요청은 Key Vault에서 추적하는 제한 한도에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="12bc4-113">더 높은 제한 한도에 대한 유효한 비즈니스 사례가 있을 경우 Microsoft에 연락해 주세요.</span><span class="sxs-lookup"><span data-stu-id="12bc4-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="12bc4-114">서비스 한도에 대응하여 앱을 제한하는 방법</span><span class="sxs-lookup"><span data-stu-id="12bc4-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="12bc4-115">다음은 앱 제한에 대한 **모범 사례**입니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="12bc4-116">요청당 작업 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="12bc4-117">요청의 빈도를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="12bc4-118">즉시 재시도를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="12bc4-119">모든 요청은 사용량 한도에 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="12bc4-120">앱의 오류 처리를 구현할 때는 HTTP 오류 코드 429를 사용하여 클라이언트 측 제한이 필요한지 감지하세요.</span><span class="sxs-lookup"><span data-stu-id="12bc4-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="12bc4-121">HTTP 429 오류 코드와 함께 요청이 다시 실패하더라도 Azure 서비스 한도에 도달하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="12bc4-122">권장되는 클라이언트 측 제한 방법을 계속 사용하여 성공할 때까지 요청을 다시 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="12bc4-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="12bc4-123">권장되는 클라이언트 측 제한 방법</span><span class="sxs-lookup"><span data-stu-id="12bc4-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="12bc4-124">HTTP 오류 코드 429가 발생할 경우 지수 백오프 접근법을 사용하여 클라이언트 제한을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="12bc4-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="12bc4-125">1초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="12bc4-126">그래도 제한된 경우 2초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="12bc4-127">그래도 제한된 경우 4초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="12bc4-128">그래도 제한된 경우 8초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="12bc4-129">그래도 제한된 경우 16초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="12bc4-130">이때 HTTP 429 응답 코드가 발생해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12bc4-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="12bc4-131">참고 항목</span><span class="sxs-lookup"><span data-stu-id="12bc4-131">See also</span></span>

<span data-ttu-id="12bc4-132">Microsoft 클라우드의 제한에 대한 더 자세한 소개는 [제한 패턴](https://docs.microsoft.com/azure/architecture/patterns/throttling)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12bc4-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

