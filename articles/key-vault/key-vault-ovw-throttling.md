---
ms.assetid: 
title: "키 자격 증명 모음 조정 지침 aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="ac5f0-102">Azure Key Vault 제한 지침</span><span class="sxs-lookup"><span data-stu-id="ac5f0-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="ac5f0-103">Hello 동시 호출 toohello Azure 서비스 tooprevent 과다 사용 리소스의 수를 제한 하는 프로세스 시작이 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="ac5f0-104">Azure 키 자격 증명 모음 (AKV)은 설계 된 toohandle 대용량의 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="ac5f0-105">요청 늘고 발생 하는 경우 클라이언트의 요청 hello AKV 서비스의 최적 성능 및 안정성을 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="ac5f0-106">스로틀 제한을 hello 시나리오에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="ac5f0-107">예를 들어, 대용량 쓰기를 수행 하는 경우 제한에 대 한 hello 가능성 보다 높습니다만 읽기를 수행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="ac5f0-108">Key Vault가 한도를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac5f0-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="ac5f0-109">키 자격 증명 모음의 서비스 제한 사항이 tooprevent 잘못 사용 하면 리소스 및 모든 주요 자격 증명 모음의 클라이언트에 대 한 서비스의 품질을 보장 하기.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="ac5f0-110">서비스 임계값이 초과되면 Key Vault가 해당 클라이언트에서 들어오는 추가 요청을 일정 시간 동안 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="ac5f0-111">이런 경우가 발생 하는 경우 키 자격 증명 모음 반환 HTTP 상태 코드 429 (너무 많은 요청), hello 요청 실패 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="ac5f0-112">또한 주요 자격 증명 모음에 의해 추적 hello 제한 위한 429 개수를 반환 하는 요청을 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="ac5f0-113">더 높은 제한 한도에 대한 유효한 비즈니스 사례가 있을 경우 Microsoft에 연락해 주세요.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="ac5f0-114">어떻게 toothrottle 응답 tooservice에서 응용 프로그램 제한</span><span class="sxs-lookup"><span data-stu-id="ac5f0-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="ac5f0-115">hello 다음은 **모범 사례** 앱 제한:</span><span class="sxs-lookup"><span data-stu-id="ac5f0-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="ac5f0-116">Hello 요청당 작업 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="ac5f0-117">요청의 hello 빈도를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="ac5f0-118">즉시 재시도를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="ac5f0-119">모든 요청은 사용량 한도에 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="ac5f0-120">응용 프로그램의 오류 처리를 구현할 때 사용 하 여 hello HTTP 오류 코드 429 toodetect hello 클라이언트 측 조정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="ac5f0-121">Hello 요청 HTTP 429 오류 코드로 다시 실패 하면 계속 발생 하는 Azure 서비스 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="ac5f0-122">Toouse hello 권장 성공할 때까지 hello 요청을 다시 시도 하는 클라이언트 쪽 제한 메서드를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="ac5f0-123">권장되는 클라이언트 측 제한 방법</span><span class="sxs-lookup"><span data-stu-id="ac5f0-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="ac5f0-124">HTTP 오류 코드 429가 발생할 경우 지수 백오프 접근법을 사용하여 클라이언트 제한을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="ac5f0-125">1초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="ac5f0-126">그래도 제한된 경우 2초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="ac5f0-127">그래도 제한된 경우 4초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="ac5f0-128">그래도 제한된 경우 8초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="ac5f0-129">그래도 제한된 경우 16초를 기다렸다가 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="ac5f0-130">이때 HTTP 429 응답 코드가 발생해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="ac5f0-131">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ac5f0-131">See also</span></span>

<span data-ttu-id="ac5f0-132">Microsoft 클라우드 hello에서 제한의 깊은 방향에 대 한 참조 [패턴 제한](https://docs.microsoft.com/azure/architecture/patterns/throttling)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5f0-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

