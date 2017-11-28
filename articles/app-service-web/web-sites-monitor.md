---
title: "Azure 앱 서비스에서 앱 aaaMonitor | Microsoft Docs"
description: "방법을 사용 하 여 Azure 앱 서비스에서 toomonitor 앱 hello Azure 포털에 알아봅니다."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="afa6b-103">방법: Azure App Service에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="afa6b-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="afa6b-104">[앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) hello에 기본 제공된 모니터링 기능을 제공 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="afa6b-105">Hello 기능 tooreview 여기에 **할당량** 및 **메트릭** hello를 설정 하는 앱 서비스 계획 뿐만 아니라 응용 프로그램에 대 한 **경고** 및 심지어 **크기조정** 이러한 메트릭을 기반으로 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="afa6b-106">할당량 및 메트릭 이해</span><span class="sxs-lookup"><span data-stu-id="afa6b-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="afa6b-107">할당량</span><span class="sxs-lookup"><span data-stu-id="afa6b-107">Quotas</span></span>
<span data-ttu-id="afa6b-108">앱 서비스에서 호스팅되는 응용 프로그램은 주제 toocertain *제한* 에 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="afa6b-109">hello 제한에서 정의 된 hello **앱 서비스 계획** hello 앱과 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="afa6b-110">Hello 응용 프로그램에서 호스팅되는 경우는 **무료** 또는 **Shared** hello 앱 צ ְ ײ hello 리소스에 대 한 hello도 정의한 다음 계획 **할당량**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="afa6b-111">Hello 응용 프로그램에서 호스팅되는 경우는 **기본**, **표준** 또는 **프리미엄** hello 설정한 hello 제한을 사용 하 여 hello 리소스에 대 한 다음 계획 **크기** (소형, 중형, 대형) 및 **인스턴스 수를** (1, 2, 3,...)의 hello **앱 서비스 계획**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="afa6b-112">**무료** 또는 **공유** 앱에 대한 **할당량**은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="afa6b-113">**CPU(Short)**</span><span class="sxs-lookup"><span data-stu-id="afa6b-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="afa6b-114">5분 간격으로 이 응용 프로그램에 대해 허용되는 CPU의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="afa6b-115">이 할당량은 5분마다 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="afa6b-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="afa6b-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="afa6b-117">하루에 이 응용 프로그램에 대해 허용되는 총 CPU 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="afa6b-118">이 할당량은 자정 UTC에 24시간마다 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="afa6b-119">**메모리**</span><span class="sxs-lookup"><span data-stu-id="afa6b-119">**Memory**</span></span>
  * <span data-ttu-id="afa6b-120">이 응용 프로그램에 대해 허용되는 총 메모리 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="afa6b-121">**대역폭**</span><span class="sxs-lookup"><span data-stu-id="afa6b-121">**Bandwidth**</span></span>
  * <span data-ttu-id="afa6b-122">하루에 이 응용 프로그램에 대해 허용되는 나가는 총 대역폭 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="afa6b-123">이 할당량은 자정 UTC에 24시간마다 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="afa6b-124">**파일 시스템**</span><span class="sxs-lookup"><span data-stu-id="afa6b-124">**Filesystem**</span></span>
  * <span data-ttu-id="afa6b-125">허용되는 총 저장소 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="afa6b-126">만 할당량 적용 가능한 tooapps에 호스팅된 hello **기본**, **표준** 및 **프리미엄** 계획은 **Filesystem**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="afa6b-127">Hello 특정 할당량, 제한 및 다른 응용 프로그램 서비스 Sku hello를 사용할 수 있는 기능에 대 한 자세한 내용은 여기에서 찾을 수 있습니다: [Azure 구독 서비스 제한](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="afa6b-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="afa6b-128">할당량 적용</span><span class="sxs-lookup"><span data-stu-id="afa6b-128">Quota Enforcement</span></span>
<span data-ttu-id="afa6b-129">사용법에 응용 프로그램이 초과 hello **CPU (short)**, **CPU (일)**, 또는 **대역폭** hello 할당량이 다시 설정 될 때까지 할당량 다음 hello 응용 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="afa6b-130">이 시간 중에는 들어오는 모든 요청에서 **HTTP 403**이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="afa6b-131">하는 경우 응용 프로그램 hello **메모리** 할당량이 초과 되 면 다음 hello 응용 프로그램 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="afa6b-132">경우 hello **Filesystem** 할당량이 초과 되 면 다음 쓰기 toologs 작성을 포함 하 여 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="afa6b-133">App Service 계획을 업그레이드하여 앱에서 할당량을 증가 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="afa6b-134">메트릭</span><span class="sxs-lookup"><span data-stu-id="afa6b-134">Metrics</span></span>
<span data-ttu-id="afa6b-135">**메트릭** hello 앱 또는 앱 서비스 계획의 동작에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="afa6b-136">에 대 한 프로그램 **응용 프로그램**, 사용할 수 있는 메트릭을 hello:</span><span class="sxs-lookup"><span data-stu-id="afa6b-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="afa6b-137">**평균 응답 시간**</span><span class="sxs-lookup"><span data-stu-id="afa6b-137">**Average Response Time**</span></span>
  * <span data-ttu-id="afa6b-138">ms에서 hello 앱 tooserve 요청에 걸리는 평균 시간을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="afa6b-139">**평균 메모리 작업 집합**</span><span class="sxs-lookup"><span data-stu-id="afa6b-139">**Average memory working set**</span></span>
  * <span data-ttu-id="afa6b-140">hello hello 앱에서 사용 하는 Mib에는 메모리의 평균 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="afa6b-141">**CPU 시간**</span><span class="sxs-lookup"><span data-stu-id="afa6b-141">**CPU Time**</span></span>
  * <span data-ttu-id="afa6b-142">hello CPU 양이 hello 앱에서 사용 하는 시간 (초)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="afa6b-143">이 메트릭에 대한 자세한 내용은 [CPU 시간 및 CPU 비율](#cpu-time-vs-cpu-percentage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa6b-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="afa6b-144">**데이터 입력**</span><span class="sxs-lookup"><span data-stu-id="afa6b-144">**Data In**</span></span>
  * <span data-ttu-id="afa6b-145">hello Mib에는 앱에서 사용 하는 들어오는 대역폭의 hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="afa6b-146">**데이터 출력**</span><span class="sxs-lookup"><span data-stu-id="afa6b-146">**Data Out**</span></span>
  * <span data-ttu-id="afa6b-147">hello Mib에는 앱에서 사용 하는 나가는 대역폭의 hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="afa6b-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="afa6b-148">**Http 2xx**</span></span>
  * <span data-ttu-id="afa6b-149">결과로 나타나는 Http 상태 코드가 200 이상 300 미만인 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="afa6b-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="afa6b-150">**Http 3xx**</span></span>
  * <span data-ttu-id="afa6b-151">결과로 나타나는 Http 상태 코드가 300 이상 400 미만인 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="afa6b-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="afa6b-152">**Http 401**</span></span>
  * <span data-ttu-id="afa6b-153">결과로 HTTP 401 상태 코드가 나타나는 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="afa6b-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="afa6b-154">**Http 403**</span></span>
  * <span data-ttu-id="afa6b-155">결과로 HTTP 403 상태 코드가 나타나는 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="afa6b-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="afa6b-156">**Http 404**</span></span>
  * <span data-ttu-id="afa6b-157">결과로 HTTP 404 상태 코드가 나타나는 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="afa6b-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="afa6b-158">**Http 406**</span></span>
  * <span data-ttu-id="afa6b-159">결과로 HTTP 406 상태 코드가 나타나는 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="afa6b-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="afa6b-160">**Http 4xx**</span></span>
  * <span data-ttu-id="afa6b-161">결과로 나타나는 Http 상태 코드가 400 이상 500 미만인 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="afa6b-162">**Http 서버 오류**</span><span class="sxs-lookup"><span data-stu-id="afa6b-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="afa6b-163">결과로 나타나는 Http 상태 코드가 500 이상 600 미만인 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="afa6b-164">**메모리 작업 집합**</span><span class="sxs-lookup"><span data-stu-id="afa6b-164">**Memory working set**</span></span>
  * <span data-ttu-id="afa6b-165">현재 Mib에 hello 앱에서 사용 하는 메모리 양입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="afa6b-166">**요청**</span><span class="sxs-lookup"><span data-stu-id="afa6b-166">**Requests**</span></span>
  * <span data-ttu-id="afa6b-167">결과 HTTP 상태 코드에 관계 없이 총 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="afa6b-168">에 대 한 프로그램 **앱 서비스 계획**, 사용할 수 있는 메트릭을 hello:</span><span class="sxs-lookup"><span data-stu-id="afa6b-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="afa6b-169">App Service 계획 메트릭은 **기본**, **표준** 및 **프리미엄** SKU의 계획에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="afa6b-170">**CPU 비율**</span><span class="sxs-lookup"><span data-stu-id="afa6b-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="afa6b-171">hello 계획의 모든 인 스턴에서 사용 되는 평균 CPU hello입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="afa6b-172">**메모리 비율**</span><span class="sxs-lookup"><span data-stu-id="afa6b-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="afa6b-173">hello 평균 메모리 hello 계획의 모든 인 스턴에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="afa6b-174">**데이터 입력**</span><span class="sxs-lookup"><span data-stu-id="afa6b-174">**Data In**</span></span>
  * <span data-ttu-id="afa6b-175">hello 평균 들어오는 대역폭 hello 계획의 모든 인 스턴에서 사용 되는입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="afa6b-176">**데이터 출력**</span><span class="sxs-lookup"><span data-stu-id="afa6b-176">**Data Out**</span></span>
  * <span data-ttu-id="afa6b-177">hello 평균 나가는 hello 계획의 모든 인 스턴에서 사용 되는 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="afa6b-178">**디스크 큐 길이**</span><span class="sxs-lookup"><span data-stu-id="afa6b-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="afa6b-179">hello 평균 수 읽기 및 쓰기의 대기 중인 요청을 저장소에 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="afa6b-180">디스크 큐 길이 tooexcessive 디스크 I/O 인해 속도 저하 될 수 있는 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="afa6b-181">**Http 큐 길이**</span><span class="sxs-lookup"><span data-stu-id="afa6b-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="afa6b-182">hello 하기 전의 toosit hello 큐에 처리 되는 HTTP 요청의 평균 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="afa6b-183">HTTP 큐 길이 값이 높거나 증가하면 계획이 과부하 상태에 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="afa6b-184">CPU 시간 및 CPU 비율</span><span class="sxs-lookup"><span data-stu-id="afa6b-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="afa6b-185">CPU 사용량을 반영하는 두 가지 메트릭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="afa6b-186">**CPU 시간** 및 **CPU 비율**</span><span class="sxs-lookup"><span data-stu-id="afa6b-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="afa6b-187">**CPU 시간** 에서 호스트 되는 앱에 대해 유용 **무료** 또는 **Shared** 자신의 할당액 중 하나는 hello 앱에서 사용 하는 CPU 시간 (분)에 정의 되어 있으므로 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="afa6b-188">**CPU 백분율** hello에 다른 포인터는 유용한에서 호스트 되는 앱에 대해 **기본**, **표준** 및 **프리미엄** 확장할 수 있습니다 이후 계획 및이 메트릭은 상태 hello의 모든 인 스턴에서 전체 사용량.</span><span class="sxs-lookup"><span data-stu-id="afa6b-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="afa6b-189">메트릭 세분성 및 보존 정책</span><span class="sxs-lookup"><span data-stu-id="afa6b-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="afa6b-190">응용 프로그램 및 응용 프로그램 서비스 계획에 대 한 메트릭을 기록 되어 hello로 hello 서비스에 의해 집계 세분성 및 보존 정책에 따라:</span><span class="sxs-lookup"><span data-stu-id="afa6b-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="afa6b-191">**분** 세분성 메트릭은 **48시간** 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="afa6b-192">**시** 세분성 메트릭은 **30일** 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="afa6b-193">**일** 세분성 메트릭은 **90일** 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="afa6b-194">할당량 및 hello Azure 포털에서에서 메트릭을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="afa6b-195">다른 hello hello 상태를 검토할 수 **할당량** 및 **메트릭** hello에서 응용 프로그램에 영향을 주는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="afa6b-196">![][quotas]
**할당량**은 설정>**할당량** 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="afa6b-197">hello UX 검토할 수 있습니다. (1) hello 할당량 이름, (2)의 다시 설정 간격, (3)의 현재 한도 및 (4) 현재 값입니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="afa6b-198">![][metrics]
**메트릭** hello 리소스 블레이드에서 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="afa6b-199">하는 hello 차트를 사용자 지정할 수도 있습니다: (1) **클릭** ,을 선택 (2) **차트 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="afa6b-200">여기에서 hello (3)을 변경할 수 있습니다 **시간 범위**, (4) **차트 종류**, (5) 및 **메트릭** toodisplay 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="afa6b-201">[서비스 메트릭 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)에서 메트릭에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="afa6b-202">경고 및 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="afa6b-202">Alerts and Autoscale</span></span>
<span data-ttu-id="afa6b-203">메트릭 tooalerts,이 대 한 자세한 toolearn 연결할 수는 앱 또는 앱 서비스 계획에 대 한 참조 [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="afa6b-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="afa6b-204">기본, 표준 또는 프리미엄 App Service 계획에 호스팅된 앱 서비스 앱은 **자동 크기 조정**을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="afa6b-205">이렇게 하면 있습니다 tooconfigure 규칙을 앱 서비스 계획 메트릭을 모니터링 하 고 거 나 낮출 수 필요에 따라 추가 리소스를 제공 하는 hello 인스턴스 수 또는 저장 하는 중 money hello 응용 프로그램은 과도 하 게 프로 비전 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="afa6b-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="afa6b-206">여기에 자동 크기 조정에 대 한 자세히 알아볼 수 있습니다: [어떻게 tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) 및 여기 [Azure 모니터 자동 크기 조정에 대 한 유용한 정보](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="afa6b-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="afa6b-207">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="afa6b-208">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afa6b-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="afa6b-209">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="afa6b-209">What's changed</span></span>
* <span data-ttu-id="afa6b-210">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="afa6b-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
